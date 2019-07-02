---
layout: post
title: "hook Windows API with Rust"
date:   2019-5-23
excerpt: "使用 Rust hook Windows API"
tags: [Rust, Windows]
comments: true
---

<center><h2>使用 Rust hook Windows API</h2></center>

<!--more-->

## hook 方式

这里采用编译成 dll 后注入，这里有两点需要注意：

1. 目标程序为 32/64 位 rust 编译工具链也需要对应 32/64 位
2. 编译需要用 release 模式，防止注入编译器在 debug 下为了调试附加的数据

Cargo.toml 中需要说明将其编译为库且类型为动态的，如果编译时显示找不到编译目标则手动添加一行路径:

```toml
[lib]
crate-type = ["dylib"]
path = "src/lib.rs"
```

当然你还可以通过创建远程线程来 hook，不过过程比较繁琐这里就提一下。

## hook 手段

**以下所有例子都以 hook MessageBoxW 为目标。**

#### IAT hook

IAT hook 即为导入表 hook，原理是 PE 文件中有个导入表，其中记录了该模块调用了哪些外部API，模块被加载到内存后，PE 加载器会修改该表，地址改成外部 API 重定位后的真实地址，我们只要直接把里面的地址改成我们新函数的地址，就可以完成对相应 API 的 Hook。

直接上代码，特别提醒一点所有的字符串结尾是没有 `\0` 的，要想像 C 一样正常工作需要自己添加：

```rust
extern crate libc;
extern crate winapi;

// 代表 c 中的 nullptr，只不过 rust 中分为可变和不可变两种
use std::ptr::{null, null_mut};
// 这几个东西是什么也不多说了，熟悉 Windows.h 的应该都知道：
use winapi::shared::{
    minwindef::LPVOID,
    ntdef::LPCWSTR,
    windef::HWND,
};

// 定义一个别名，省的后面类型转换的时候写一大堆
type MessageBoxWHook = *const unsafe extern "system" fn(HWND, LPCWSTR, LPCWSTR, u32) -> i32;

// 保存原函数地址，当然这里可以用指针具体写法后面单独介绍
static mut MESSAGE_BOX_W_HOOK_ADDRESS: u64 = 0;

// for Debug
unsafe fn clear_last_error() {
    use winapi::um::errhandlingapi::SetLastError;
    SetLastError(0);
}

// for Debug
unsafe fn show_last_error() {
    use winapi::um::{
        errhandlingapi::GetLastError,
        winuser::{MB_OK, MessageBoxA},
    };

    let e = GetLastError();
    let e = format!("{}\0", e.to_string());
    MessageBoxA(null_mut(), e.as_ptr() as _, "\0".as_ptr() as _, MB_OK);
}

// 我们自己的 MessageBoxW
unsafe extern "system" fn hook_message_box_w(h_wnd: HWND, _: LPCWSTR, _: LPCWSTR, u_type: u32) -> i32 {
    (*(&MESSAGE_BOX_W_HOOK_ADDRESS as *const _ as MessageBoxWHook))(
        h_wnd,
        "Ops hooked by Xavier!\0".encode_utf16().collect::<Vec<_>>().as_ptr(),
        "Ops hooked by Xavier!\0".encode_utf16().collect::<Vec<_>>().as_ptr(),
        u_type,
    )
}

// 遍历表找到 MessageBoxW
unsafe fn detour(module_name: *const i8, old_func_offset: u64, new_func_address: u64) -> u64 {
    use std::mem::size_of;
    use libc::strcmp;
    use winapi::{
        um::{
            libloaderapi::GetModuleHandleA,
            memoryapi::VirtualProtect,
            winnt::{PAGE_EXECUTE_READWRITE, PIMAGE_DOS_HEADER, PIMAGE_IMPORT_DESCRIPTOR, PIMAGE_NT_HEADERS},
            winuser::{MB_OK, MessageBoxA},
        },
    };

    let module_address = GetModuleHandleA(module_name) as u64;
    let old_func_address = module_address + old_func_offset;

    let image_base = GetModuleHandleA(null()) as u64;
    let p_dos_header = image_base as PIMAGE_DOS_HEADER;
    let p_nt_headers = (image_base + (*p_dos_header).e_lfanew as u64) as PIMAGE_NT_HEADERS;
    let mut p_import_descriptor = (image_base + (*p_nt_headers).OptionalHeader.DataDirectory[1].VirtualAddress as u64) as PIMAGE_IMPORT_DESCRIPTOR;

    while (*p_import_descriptor).FirstThunk != 0 {
//        MessageBoxA(null_mut(), (image_base + (*p_import_descriptor).Name as u64) as _, "\0".as_ptr() as _, MB_OK);
        if strcmp(module_name, (image_base + (*p_import_descriptor).Name as u64) as *const i8) != 0 {
            p_import_descriptor = p_import_descriptor.offset(1);
            continue;
        }
        MessageBoxA(null_mut(), (image_base + (*p_import_descriptor).Name as u64) as _, "\0".as_ptr() as _, MB_OK);

        let mut p_func = (image_base + (*p_import_descriptor).FirstThunk as u64) as *mut u64;
        for i in 0.. {
            if p_func.is_null() { return 0; }

//            MessageBoxA(null_mut(), (image_base + (*((image_base + *(*p_import_descriptor).u.OriginalFirstThunk() as u64) as *const u64).offset(i)) + 2) as _, "\0".as_ptr() as _, MB_OK);
            if old_func_address == *p_func {
                MessageBoxA(null_mut(), (image_base + (*((image_base + *(*p_import_descriptor).u.OriginalFirstThunk() as u64) as *const u64).offset(i)) + 2) as _, "\0".as_ptr() as _, MB_OK);

                let mut old_protection = 0u32;
                VirtualProtect(p_func as _, size_of::<LPVOID>(), PAGE_EXECUTE_READWRITE, &mut old_protection as _);
                *p_func = new_func_address;
                VirtualProtect(p_func as _, size_of::<LPVOID>(), old_protection, &mut old_protection as _);

                return old_func_address;
            }

            p_func = p_func.offset(1);
        }

        return 0;
    }

    0
}

unsafe extern "system" fn init_hook(_: LPVOID) -> u32 {
    MESSAGE_BOX_W_HOOK_ADDRESS = detour("USER32.dll\0".as_ptr() as _, 0x72AD0, hook_message_box_w as _);

    0
}

// 告诉编译器不要对函数名进行混淆，使得能被 cffi 调用
#[no_mangle]
#[allow(non_snake_case)]
pub extern "system" fn DllMain(_: winapi::shared::minwindef::HINSTANCE, reason: u32, _: LPVOID) -> i32 {
    use winapi::um::processthreadsapi::CreateThread;

    // 1 实际上就是 DLL_PROCESS_ATTACH 的值
    match reason {
        1 => unsafe { CreateThread(null_mut(), 0, Some(init_hook), null_mut(), 0, null_mut()); }
        0 => (),
        _ => (),
    }

    // Windows 编程中的 BOOL TRUE 实际上就是 i32 1
    1
}
```

编译后可注入记事本，然后搜索，搜索结果的对话框会被 hook。

![messageboxw-hook](https://raw.githubusercontent.com/AurevoirXavier/hook-in-rust/master/demo.jpg)

[github](https://github.com/AurevoirXavier/hook-in-rust/blob/master/messagebox-iat-hook)

#### EAT hook

EAT hook 即为导出表 hook，但是一般用的不多。原理是调用模块 IAT 中的函数地址是通过被调用模块 EAT 获取的，等于变相修改了 IAT，只要修改了被调用模块 EAT 中的函数地址，就可以 hook 到了。但是在我反复测试多次后得出，就是 EAT hook 要足够早最好是在程序启动前，前面说到这是变相修改 IAT 所以要在 IAT 使用它之前修改。

[github](https://github.com/AurevoirXavier/hook-in-rust/blob/master/messagebox-eat-hook)

#### inline hook

这个是最难的但是没有它不能 hook 到的函数，原理很简单，在需要 hook 的函数执行前把当前参数入栈备份，写入跳转指令，跳转到我们函数执行完后跳转回去，出栈参数还原跳转前的寄存器状态，以上所有操作都是在汇编层面。这里有两个难点，第一是找到 hook 函数的地址，第二则是跳转指令的写入，这里需要破坏部分原有的指令，如果目标是 64 位的，那么寻址空间变大又分为长跳短跳，C 的 MSVC 编译器不能编译 64 位的 ASM，要么安装 intel 的编译器要么先反汇编成字节码，Rust 中的 asm! 宏我也只尝试过 32 位的。所以很多人会选择使用库，比如 minihook，easyhook，plyhook 还有微软的 detours。Rust 的选择则较少，本例使用 [detour-rs](https://github.com/darfink/detour-rs)。关于第一个难点由于本例 hook 的 MessageBoxW 在 USER.DLL 中，这个系统模块在所有程序的地址都是一样的，所以找到它的地址没什么难度。

[github](https://github.com/AurevoirXavier/hook-in-rust/tree/master/messagebox-inline-hook)

#### VMT hook

VMT hook 即为虚函数表 hook，原理需要大家复习一下 C 的内容了。这里特别提一点，有类的对象会共用一张虚表但是有的类的对象各自拥有一张虚表，有时候修改自己创建出来的类对象的虚表是没用的。但是尽管虚表不同，虚表里面存的地址一定是一样的，所以不修改这个地址而修改这个地址的内容即可达到 hook 的目的，这样实际上就是 VMT hook 和 inline hook 的结合。接下来这个 D3D11 hook 的例子作为补充，刚好 `ID3D11Device` 就是每个对象单独拥有一张虚表的情况。

[github](https://github.com/AurevoirXavier/dauntless-helper/tree/master/rust-ver)

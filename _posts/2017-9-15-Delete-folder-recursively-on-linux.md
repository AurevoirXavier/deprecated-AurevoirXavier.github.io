---
layout: post
title: "Delete folder recursively on Linux"
date:   2017-09-15
excerpt: "Linux 下递归删除文件"
project:    true
tags: [Linux, shell]
comments: true
---

```shell
find  .  -name  '*.exe'  -type  f  -print  -exec  rm  -rf  {} \;
```

* `.` 表示从当前目录开始递归查找。
* `-name '*.exe'`根据名称来查找，要查找所有以 **.exe** 结尾的文件夹或者文件。
* ``-type f`查找的类型为文件。
* `-print` 输出查找的文件目录名。
* `-exec`，选项后边跟所要执行的命令，表示将 `find` 出来的文件或目录执行该命令。
* 最后是 `{}`， (空格)，`\` 和 `;`。`find` 需要知道 `exec` 的参数何时终止。因为要终止 **shell** 命令，所以要用 `;`。同时因为 **shell** 也使用这个字符，所以这样的字符在通过 **shell** 插入时需要转义。


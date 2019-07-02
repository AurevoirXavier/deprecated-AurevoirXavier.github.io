---
layout: post
title: "how to sign transaction in Rust"
date:   2018-11-26
excerpt: "如何在 Rust 中签名交易"
tags: [BlockChain, Ethereum, Rust, Web3]
comments: true
---

<center><h2>如何在 Rust 中签名交易</h2></center>

<!--more-->



最近玩了一下中国特色~~实名制~~区块链——[链克](https://www.lianxiangcloud.com/coin/coin/)，其表面上为了不被政府枪毙对外称封闭的，但事实上套现方法总是有滴，就是兑换完物品后将其折现，比如你兑换了一个月迅雷会员然后出手这个兑换码。吐槽就到这里了，下面进入正题。



最近写了个抢兑程序(不得不说用 Rust 写并发还是非常舒心的)，但是创建订单后一定时间内不交易就会取消，于是就进一步研究了一下交易。不过截至目前 Rust 签名交易的 lib 还没有什么进展，详见[讨论](https://ethereum.stackexchange.com/questions/46490/how-to-sign-a-transaction-in-rust)。



那么只好使用 [cpython](https://github.com/dgrunwald/rust-cpython) 曲线救国了:

```rust
let gil = Python::acquire_gil();
let py = gil.python();
let web3 = py.import("web3").unwrap();

let transaction = {
    let transaction = PyDict::new(py);
    transaction.set_item(py, "gas", gas_limit).unwrap();
    transaction.set_item(py, "gasPrice", gas_price).unwrap();
    transaction.set_item(py, "nonce", nonce).unwrap();
    transaction.set_item(py, "data", data).unwrap();

    let web3 = web3.get(py, "Web3").unwrap();
    let to = web3.call_method(py, "toChecksumAddress", (to, ), None).unwrap();

    transaction.set_item(py, "to", to).unwrap();
    transaction.set_item(py, "value", value).unwrap();

    transaction
};

let account = web3.get(py, "Account").unwrap();
let signed_transaction = account.call_method(py, "signTransaction", (transaction, private_key), None).unwrap();

let raw_transaction: String = signed_transaction.getattr(py, "rawTransaction")
    .unwrap()
    .call_method(py, "hex", NoArgs, None)
    .unwrap()
    .extract(py)
    .unwrap();
```

实际上就是使用了 python 的 web3 库，提供了一个变通的方法。


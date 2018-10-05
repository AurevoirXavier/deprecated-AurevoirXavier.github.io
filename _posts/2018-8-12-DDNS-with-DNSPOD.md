---
layout: post
title: "DDNS with DNSPOD"
date:   2018-8-12
excerpt: "通过 DNSPOD 实现动态域名解析"
tags: [Web]
comments: true
---

<center><h2>通过 DNSPOD 实现动态域名解析</h2></center>

<!--more-->



最近申请了一个公网 ip 用于做智能家居，不过发现这玩意儿 24 小时变动一次。这样按平常的套路来解析过一天就域名解析到别人 ip 上去了。所以需要动态解析，看了一下国内外的几个出名的提供动态解析的服务商大概有下面几个问题：

1. 需要安装他的软件，既没有提供 linux 版安装包也没有给出 api
2. 有 api 但不给使用自己的域名
3. 可以使用自己的域名，但是要转入他旗下并每年缴纳维护费用
4. 钱到位，上面都不是问题

就自己家庭使用而已，交那个钱没什么必要。于是我想，大不了自己写一个脚本定时更改万网的解析算了，学习一番之后发现万网还提供了不少 api 可以操作，但是要用他的 sdk 让我觉得有些繁琐，不过也比我原本打算用爬虫的方式做简单不少。正要着手开始之际，又看到了 [DNSPOD](https://www.dnspod.cn)，文档中关于更新解析的说明只需要 curl 一下对应 api 就行了，这可是方便的不能在方便了。下面讲一下 curl 之前要做的一些准备工作：



#### 添加域名

1. 注册登录后
2. 左边一栏选择 **域名解析**
3. 在打开的页面中选择 **添加域名**
4. 接着输入你自己的域名后确定

#### 修改 NS 地址

这里就是修改 DNS 服务器的意思，这里我以阿里云万网域名为例子：

1. 进入阿里云控制台
2. 选择域名服务，会看到你所持有的域名
3. 点击你想要用的域名，会打开该域名的基本信息，其中有一项 DNS 服务器，而且有两个默认值 `dns15.hichina.com`，`dns16.hichina.com`
4. 点击修改 DNS，将两个默认值分别修改为 `f1g1ns1.dnspod.net`，`f1g1ns2.dnspod.net`

接下来需要等待生效，最多需要 3 天，我的是用了 1 天就生效了。

*以上 DNS 服务器的值可能未来会发生变化，需要自行核对最新文档 8/12/2018*



#### 动态解析

**此步骤需要等待前一步骤完成，如何判断修改生效，打开 DNSPOD 控制台域名<font color="red">不再提示</font> “域名 NS 地址还未修改” 即为生效**



[文档](https://www.dnspod.cn/docs/records.html#dns)中指出，需要以下几个参数：

- 公共参数
- `domain_id` 或 `domain`, 分别对应域名ID和域名, 提交其中一个即可
- `record_id` 记录ID，必选
- `sub_domain` 主机记录，如 www
- `record_line` 记录线路，通过API记录线路获得，中文，比如：默认，必选
- `record_line_id` 线路的ID，通过API记录线路获得，英文字符串，比如：‘10=1’ 【`record_line` 和 `record_line_id` 二者传其一即可，系统优先取 `record_line_id`】
- `value` IP地址，例如：6.6.6.6，可选

精简一点的话只需这样就可以了（`value` 可以不写，默认直接使用你发起请求的地址）：



`curl -X POST https://dnsapi.cn/Record.Ddns -d 'login_token={}&format=json&domain_id={}&record_id={}&record_line_id=0&sub_domain=@'`



不过这几个参数也需要单独获取一下：

1.  `login_token` 需要你在左边一栏点击 **安全设置** 中生成（注意生成的 token 中有逗号传参的时候要保留），这里也可以用户名密码但是参数名不同，这种方法不安全不建议使用，所以不作更多说明
2. `domain_id` 需要填写上一步中生成的 `login_token` 到 `curl 'https://dnsapi.cn/Domain.List' -d 'login_token={}&format=json'` 中来获取，返回的 json 数据中 domains 项中对应域名 id 项的值就是你需要的 `domain_id` 了
3. `record_id` 需要填写前两步中获取的 `login_token`，`domain_id` 到 `curl 'https://dnsapi.cn/Record.List' -d 'login_token={}&format=json&domain_id={}'` 中来获取，返回的 json 数据中 records 项中对应记录 id 项的值就是你需要的 `record_id` 了

*以上所有 {} 仅作占位符方便教程，最后填写好对应项执行时的版本不应出现*

*返回的 json 没有格式化很难看，最好有一个 json 格式化工具*

#### 定时更新

实现方法多种多样，这里我用 `crontab`。个人习惯，新建 `/usr/bin/local/ddns.sh` 然后在其中放入需要 curl 也就是需要更新的所有记录。然后 `crontab -e` 在其中加入一行 `* */1 * * * /usr/bin/local/ddns.sh` 就可以每小时更新一次了。可以参考 [crontab 说明](http://man.linuxde.net/crontab) 定制你自己的更新方式。

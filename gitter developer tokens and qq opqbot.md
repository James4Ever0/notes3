---
title: gitter developer tokens and qq opqbot
created: '2022-08-13T00:54:17.441Z'
modified: '2022-08-13T07:13:15.727Z'
---

# gitter developer tokens and qq opqbot

现在有两个标准[onebot]() [nonebot](https://nb2.baka.icu/)

onebot有大量的[qq适配器]() 而nonebot有[大量的插件和除了qq以外的连接器](https://nb2.baka.icu/store)

在onebot的qq适配器中 [oicq]()这个适配器提供了一些用于逆向qq协议的程序：

也可以考虑逆向opqbot的go编译好了的程序 或者逆向分析opqbot的网络请求数据

to get the token, login first, then visit [here](https://developer.gitter.im/apps) or click "sign in" [here](https://developer.gitter.im/)

据说扫码登录只支持同一个ip下面的登陆 不知道为什么这个opqbot登陆失败

it seems the login issue of opqbot is related to the account itself, not gitter token, software version or proxy

by the way we could always use go-cqhttp, without the ability to collect red packet and add group/friends.

qq add group/friends may be enabled by our windows virtual machines. without opq, it is very memory intensive.

tokens:
```
74eb7eb14aa36d1b9c2c663bc49335e8becd5318
```
```
2d391bd7639362032d09abfc5a9cc6368b7664d5
```
```
bdf52599d992665509ee5b0b533d5eed08452def
```

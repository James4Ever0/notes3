---
title: QQ 微信 信息提取 bot搭建
created: 2022-05-24T13:30:47+08:00
modified: 2022-07-14T23:54:02+08:00
---

# QQ 微信 信息提取 bot搭建

would it be a lot easier if we can send those article/video links to external (out of gfw) social media platforms in their native language? still censorship will be applied.

## qq号码注册规则

qq群最多可以添加500个群 1500个好友 其中群可加的数量 = max(0,500 - 已加入群数量 - 好友数量)
可以退出一些安静的群 不发红包的群 删除好友

屏蔽别人加我为好友 允许别人拉我进群 自动退出广告群 退出不活跃的群

群一天只能加两三个 或者手机上可以加十个
好友一天可以加三十几个

如何获取进群验证问题？记得可以拦截PC端搜索QQ群接收的数据包获取验证问题 或许不行 总之可以获取到一些参数 也可以考虑拦截opqqq的通信 或者发送一些通用的加群验证信息 比如“加群学习” “小伙伴一起玩” 之类的 或者用ai模型生成

一个手机号码可以申请10个qq号，一个手机号绑定的QQ帐号名额上限为10个，但一天一个手机号只能成功注册两到三个

WeChat needs serious reverse engineering like frida.

https://github.com/cixingguangming55555/wechat-bot
有webapi的微信机器人 注入dll到pc

https://github.com/mrsanshui/WeChatPYAPI
可以加好友的python wechat pc hook

https://github.com/snlie/WeChat-Hook
易语言的wechat hook 功能非常全 搜索 加人 有教程链接 教学代码

https://github.com/TonyChen56/WeChatRobot
比较老的wechat逆向模块 wechatapis.dll半天获得不了 有教程链接

https://github.com/wechaty/puppet-xp
frida 驱动的wechat puppet 暂时没有加人 搜索人 在windows上运行

wechat reverse engineering tutorials:
https://github.com/hedada-hc/pc_wechat_hook
https://github.com/zmrbak/PcWeChatHooK

wechaty base framework:
https://github.com/Wechaty/python-wechaty/ (puppet support might be incomplete)
https://github.com/Wechaty/wechaty/

botoy opqbot api for python
https://botoy.opqbot.com/zh_CN/latest/action/

qq opqbot (for wechat it has rstbot) download and install (need gitter.im api token):
https://docs.opqbot.com/guide/manual.html#启动失败

opqbot needs to be reverse engineered or we won't know what is going on inside.

unofficial opqbot wiki:
https://mcenjoy.cn/opqbotwiki/

wechat bot(non-free wechat puppets):
wechaty

quoted content are controversial and highly viral. must be filtered and classified before proceeding.
quotes are like comments.

---
title: QQ 微信 信息提取 bot搭建
created: '2022-05-24T05:30:47.000Z'
modified: '2022-07-14T14:02:39.281Z'
---

# QQ 微信 信息提取 bot搭建

would it be a lot easier if we can send those article/video links to external (out of gfw) social media platforms in their native language? still censorship will be applied.

## qq
qq群最多可以添加500个群 1500个好友 其中群可加的数量 = max(0,500 - 已加入群数量 - 好友数量)
可以退出一些安静的群 不发红包的群 删除好友



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

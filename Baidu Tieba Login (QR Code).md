---
tags: [autologin, freelancer, reverse engineering, tieba]
title: Baidu Tieba Login (QR Code)
created: '2021-12-19T21:56:45.000Z'
modified: '2022-08-18T13:47:06.071Z'
---

# Baidu Tieba Login (QR Code)

Assigned a job.

Cloud Phone:
`http://www.ddyun.com/sem/pcddybdyunkong/?bd_vid=7609174489837191328
17756220843:fsfs5214`

QR Link:
https://wappass.baidu.com/wp/?qrlogin&t=1640006201&error=0&sign=v1_13fa5a31cf31fa864475cbf3fd2fc&cmd=login&lp=pc&tpl=tb&adapter=3&logPage=traceId%3Apc_loginv4_1640006201%2ClogPage%3Aloginv4&qrloginfrom=pc&local=%E5%8D%97%E4%BA%AC

This job has no public data to refer. we need to monitor the tieba app.
mitmproxy --mode socks5 --listen-port 8050 --save-stream-file logs
Run mitmproxy without options to generate the mitm certificate. Install the certificate (usually ~/.mitmproxy/mitmproxy-ca-cert.cer) in the Android phone. It may be needed to change the extension to .crt to install it.

frida is needed to disable certificate-pinning, or if this is somehow possible. (also via justtrustme, xposed)
https://hub.fastgit.org/httptoolkit/frida-android-unpinning
https://httptoolkit.tech/blog/frida-certificate-pinning/

setenforce 0
to disable stack errors

to connect to frida-server:

https://github.com/15872998154/frida_termux

./frida_server -l 0.0.0.0:27042 

frida -H 127.0.0.1:27042 --codeshare sowdust/universal-android-ssl-pinning-bypass-2  -f com.baidu.tieba --no-pause

i will not know if the client will be satisfied or not. i only know this would be very hard to solve. if not good i will quit.


to read flow:
mitmproxy -n --showhost -r logs.log

print xxd line and ascii parse only:
cat logs2.log | xxd | awk '{print $1" "$NF}'

cat logs2.log | xxd | awk '{print $1" "$NF}' | grep -C 5 http://wap
0012f020: ss-Control-Allow
0012f030: -Methods,18:GET,
0012f040: OPTIONS,]
0012f050: 59:27:Access-Con
0012f060: trol-Allow-Origi
0012f070: n,24:http://wapp
0012f080: ass.baidu.com,]2
0012f090: 8:10:Connection,
0012f0a0: 10:keep-alive,]2
0012f0b0: 7:16:Content-Enc
0012f0c0: oding,4:gzip,]44

cat logs2.log | xxd | awk '{print $1" "$NF}' | grep -C 5 https://wap
001190e0: ite,]28:14:sec-f
001190f0: etch-mode,7:no-c
00119100: ors,]26:14:sec-f
00119110: etch-dest,5:styl
00119120: e,]40:7:referer,
00119130: 26:https://wappa
00119140: ss.baidu.com/,]3
00119150: 6:15:accept-enco
00119160: de
00119170: flate,]37:15:acc
00119180: ept-language,14:
--
0011aed0: ite,]28:14:sec-f
0011aee0: etch-mode,7:no-c
0011aef0: ors,]27:14:sec-f
0011af00: etch-dest,6:scri
0011af10: pt,]40:7:referer
0011af20: ,26:https://wapp
0011af30: ass.baidu.com/,]
0011af40: 36:15:accept-enc
0011af50: d
0011af60: eflate,]37:15:ac
0011af70: cept-language,14
--
0011ccd0: -site,]28:14:sec
0011cce0: -fetch-mode,7:no
0011ccf0: -cors,]26:14:sec
0011cd00: -fetch-dest,5:st
0011cd10: yle,]40:7:refere
0011cd20: r,26:https://wap
0011cd30: pass.baidu.com/,
0011cd40: ]36:15:accept-en
0011cd50: coding,13:gzip,
0011cd60: deflate,]37:15:a
0011cd70: ccept-language,1
--
00121f40: -site,]28:14:Sec
00121f50: -Fetch-Mode,7:no
00121f60: -cors,]26:14:Sec
00121f70: -Fetch-Dest,5:im
00121f80: age,]40:7:Refere
00121f90: r,26:https://wap
00121fa0: pass.baidu.com/,
00121fb0: ]36:15:Accept-En
00121fc0: coding,13:gzip,
00121fd0: deflate,]37:15:A
00121fe0: ccept-Language,1
--
0012f550: in,]28:14:Sec-Fe
0012f560: tch-Mode,7:no-co
0012f570: rs,]27:14:Sec-Fe
0012f580: tch-Dest,6:scrip
0012f590: t,]256:7:Referer
0012f5a0: ,241:https://wap
0012f5b0: pass.baidu.com/w
0012f5c0: p/?qrlogin&t=163
0012f5d0: 9980306&error=0&
0012f5e0: sign=v1_f3b74f3a
0012f5f0: 21e355010985e711
--
00139700: ,]28:14:Sec-Fetc
00139710: h-Mode,7:no-cors
00139720: ,]26:14:Sec-Fetc
00139730: h-Dest,5:image,]
00139740: 40:7:Referer,26:
00139750: https://wappass.
00139760: baidu.com/,]36:1
00139770: 5:Accept-Encodin
00139780: defla
00139790: te,]37:15:Accept
001397a0: -Language,14:en-
--
0013db70: 39997136312&tpl=
0013db80: tb&auto_statisti
0013db90: c=e2V2ZW50VHlwZT
0013dba0: p0b3VjaC1qcy1lcn
0013dbb0: Jvcn0=&extrajson
0013dbc0: =https://wappass
0013dbd0: .baidu.com/wp/?q
0013dbe0: rlogin&t=1639980
0013dbf0: 306&error=0&sign
0013dc00: =v1_f3b74f3a21e3
0013dc10: 55010985e7113869

https://blog.csdn.net/qq_27644127/article/details/112987332

with a plugin to collect statistics:
http://file.taotaoya.top/load/TT.rar

that guy wants me to discover barcode first.

i may paste cookies here:
https://termbin.com/lq5e

use ccrypt, xxd and nc to do transport. (do you have these?)

cat cookies.log.cpt | xxd | nc termbin.com 9999
xxd -r
ccrypt -c cookies.log.cpt

passwd:abcdefg


a typical QR login link on android:
https://wappass.baidu.com/wp/?qrlogin&t=1639929144&error=0&sign=v1_3b3e89197877163a12614a9a7f519&cmd=login&lp=pc&tpl=tb&adapter=3&clientfrom=native&qrloginfrom=native&local=%E9%93%9C%E9%99%B5

parsed with elinks copied with termux-clipboard-set:

   Link: [1]canonical
   Link: [2]alternate (handheld)

                         ???????????????????????????--python??????

   [3]lxguang_tao 2021-01-22 18:11:49 547 ??????
   ??????????????? [4]python ??????????????? [5]python
   ??????????????????????????????????????????????????? [6]CC 4.0 BY-SA ?????????????????????????????????
   ??????????????????????????????
   ???????????????[7]https://blog.csdn.net/qq_27644127/article/details/112987332
   ??????
   [8][IMG] [9]python ?????????????????????
   1 ????????? 0 ??????
   ????????????

  ???????????????????????????--python??????

     ?????
          ?????[10]????????????
          ?????
               ?????[11]????????????
               ?????[12]????????????

          ?????[13]????????????
          ?????
               ?????
                    ?????[14]????????????
                    ?????[15]??????

          ?????[16]??????

????????????

     ????????????????????????????????????????????????????????????????????????????????????????????????????????????
     ??????????????????????????????????????????????????????????????????Cookie BDUSS????????????????????????
     ?????????????????????BDUSS??????????????????????????????????????????????????????????????????????????????
     ???????????????????????????????????????????????????????????????????????????????????????BDUSS????????????
     ????????????????????????????????????????????????????????????????????????????????????????????????????????????
     ??????????????????BDUSS??????????????????????????????????????????BDUSS?????????????????????????????????
     ???BDUSS????????????????????????????????????????????????????????????????????????????????????????????????
     ??????

  ????????????

   [17]?????????

   ??1.???????????????????????????????????????????????????????????????????????????????????????????????????????????
       ?????????????????????????????????????????????????????????????????????

   ??2.???????????????????????????????????????????????????????????????????????????????????????????????????????????
       ?????????????????????????????????????????????????????????????????????????????????????????????????????????
       ?????????????????????????????????????????????????????????????????????

   ??3.???????????????????????F12????????????Network?????????????????????????????????????????????png??????
       ???????????????????????????????????????????????????
       [18]?????????????????????

   ??4.????????????????????????????????????????????????????????Get?????????????????????????????????sign,lp
       ???qrloginfrom????????????????????????????????????pc?????????????????????????????????pc(??????
       ???)??????????????????????????????????????????????????????????????????sign???
       [19]???????????????????????????

   ??5.??????????????????????????????????????????????????sign???????????????????????????????????????????????????
       ?????????????????????????????????????????????????????????????????????????????????
       ??????https://passport.baidu.com/v2/api/getqrcode?lp=pc&qrloginfrom=pc&gid=1527EF2-1333-475F-BA75-319AF40E53E7&callback=tangram_guid_1611304323880&apiver=v3&tt=1611304324028&tpl=tb&_=1611304324032???
       ?????????????????????sign??????????????????????????????????????????

   ??6.???????????????????????????????????????????????????????????????????????????????????????????????????????????
       ??????????????????tt???_??????????????????????????????????????????????????????????????????????????????
       ???????????????????????????????????????????????????????????????gid???callback?????????????????????
       ??????gid??????????????????????????????????????????gid????????????????????????python??????uuid???
       ????????????????????????????????????????????????????????????????????????????????????????????????js??????
       ?????????????????????????????????????????????F12 Source?????? Ctrl+Shift+F?????????
       ??????v2/api/getqrcode??????
       [20]??????

   ??7.???????????????????????????????????????????????????????????????????????????????????????????????????????????
       ????????????????????????????????????????????????????????????????????????callback?????????????????????
       ???????????????????????????????????????????????????????????????????????????tmd????????????????????????
       ?????????????????????????????????????????????????????????????????????????????????????????????????????????
       ????????????????????????????????????????????????????????????????????????????????????????????????
       [21]???????????????????????????

   ??8.??????????????????????????????????????1?????????????????????????????????????????????2?????????????????????
       ?????????????????????????????????????????????BDUSS????????????????????????????????????

   ??9.????????????????????????????????????????????????????????????????????

     ????????????????????????????????????????????????????????????????????????????????????????????????????????????
     ?????????
     ????????????????????????????????????????????????????????????????????????????????????????????????????????????
     ???????????????????????????????????????????????????????????????????????????????????????????????????

   10.????????Network???????????????????????????????????????????????????????????????????????????????????????
       ??????????????????????????????channel_id????????????????????????????????????????????????????????????
       ????????????????????????
       [22]??????
   11.???????????????????????????????????????????????????????????????????????????????????????????????????????????
       ????????????????????????
       **tangram_guid_1611307815857({"errno":0,"channel_id":"v1_cf81fb2823935db841b5395152de2","channel_v":"{\"status\":0,\"v\":\"3f1a8f93cca689cead144ad405b03945\",\"u\":\"\"}"})
       ** ???????????????????????????????????????????????????????????????????????????????????????????????????
       ???????????????
   12.??/v3/login/main/qrbdusslogin
       [23]??????????????????
   13.????????????????????bduss??????????????????????????????????????????????????????????????????????????????
       ???????????????????????????????????????????????????????????????JSON????????????????????????BDUSS
       ???tmd????????????????????????BDUSS???????????????????????????????????????Cookie??????????????????
       ????????????????????????????????????Cookie???
       [24]cookie
   14.??????????????????????????????????????BDUSS????????????????????????????????????????????????????????????
       ?????????????????????????????????????????????????????????????????????????????????????????????????????????
       ?????????????????????????????????

  ????????????

   ??????????????? ?????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ????????????????????????????????????????????????????????????????????????????????????????????????????????????

????????????

    ????????????

   python request?????????json?????????re?????????time, uuid

    ??????

 """
 QrCodeLogin.py ???????????????
 """
 """
 1?????????????????????????????????
 2?????????????????????
 3???????????????
 """

 import requests, re, time, json, uuid

 class qrcodeLogin:
     def __init__(self):
         self.get_qrcode_url = "https://passport.baidu.com/v2/api/getqrcode"
         self.unicast_url = "https://passport.baidu.com/channel/unicast"
         self.login_url = "https://passport.baidu.com/v3/login/main/qrbdusslogin"
         self.qrcode = ""
         self.gid = str(uuid.uuid4()).upper()
         self.callback = ""
         self.sign = ""
         self.bduss = ""
         self.headers = {
             "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:74.0) Gecko/20100101 Firefox/74.0"
         }

     def get_qrcode(self):
         self.callback = "tangram_guid_{}".format(str(int(round(time.time() * 1000))))
         parms = {
             "lp":"pc",
             "qrloginfrom": "pc",
             "gid": self.gid,
             "callback": self.callback,
             "apiver": "v3",
             "tt": int(round(time.time() * 1000)),
             "tpl": "tb",
             "-": int(round(time.time() * 1000))
         }
         html = requests.get(url=self.get_qrcode_url, params=parms, headers=self.headers, verify=False).content.decode('utf-8', errors='ignore')
         # print(html)
         p = re.compile('"imgurl":"(.*?)"')
         p2 = re.compile('"sign":"(.*?)"')


         qrcode = p.findall(html)
         self.sign = p2.findall(html)
         if len(qrcode) == 0:
             return None
         else:
             print("https://"+qrcode[0].replace("\\", ""))
             self.qrcode = "https://"+qrcode[0].replace("\\", "")

     def unicast(self):
         start = time.time()
         errno = 1
         status = 1
         flag = True
         pattern = re.compile('({.*})')
         while(True):
             end = time.time()
             if (end - start) > 300:
                 break
             parms = {
                 "channel_id": self.sign,
                 "qrloginfrom": "pc",
                 "gid": self.gid,
                 "callback": self.callback,
                 "apiver": "v3",
                 "tt": int(round(time.time() * 1000)),
                 "tpl": "tb",
                 "-": int(round(time.time() * 1000))
             }
             jsons = requests.get(url=self.unicast_url, params=parms, headers=self.headers, verify=False)
             html = jsons.content.decode('utf-8', errors="ignore").replace('\\', '').replace('"{', "{").replace('}"', "}")
             try:
                 if errno or status:
                     message = json.loads(re.search(pattern, html).group())
                     errno = message['errno']
                     if errno == 0 and flag:
                         flag = False
                     elif errno == 0:
                         status = message['channel_v']['status']
                 if not errno and not status:
                     message = json.loads(re.search(pattern, html).group())
                     self.bduss = message['channel_v']['v']
                     BDUSS = self.login()
                     print(BDUSS)
                     return BDUSS
             except Exception as e:
                 print(e)
                 break
         return None

     def login(self):
         parm = {
             'v': int(round(time.time() * 1000)),
             'u': 'https://tieba.baidu.com/index.html',
             'bduss': self.bduss,
             'loginVersion': 'v4',
             'qrcode': '1',
             'tpl': 'tb',
             'apiver': 'v3',
             'tt': int(round(time.time() * 1000)),
             'traceid': None,
             'time': round(time.time()),
             'alg': 'v3',
             'sig': 'EsdgfadNMU5rQVl4NWhSDFSDCVSDGFSdfsdfsf8xcVEveFNqanFGK2ZRdDBiejdXQXVhK1ZlRDZKMzsdfDSES==',
             'elapsed': 3,
             'shaOne': '00edf2343d07csdf23478b6ccd34f9a92290d3tg',
             'callback': 'bd__cbs__o5224l',
         }

         login_r = requests.get(self.login_url, headers=self.headers, params=parm, verify=False)
         str_html = login_r.content.decode('utf-8')
         # print(str_html)
         for i in login_r.cookies:
             if i.name == "BDUSS":
                 print('????????????')
                 pname = re.compile('"displayName": "(.*?)"')
                 name_list = pname.findall(str_html)
                 # print(name_list)
                 if len(name_list) > 0:
                     name = name_list[0]
                     return (i.value, name)
                 return (i.value, '')
         return None


     def getImg(self):
         img = requests.get(url=self.qrcode, headers=self.headers, verify=False)
         # print(img.content)
         # with open("tieba.gif", 'wb') as w:
         #     w.write(img.content)
         return img.content



 if __name__ == '__main__':
     s = qrcodeLogin()
     s.get_qrcode()
     s.getImg()
     s.unicast()





??????

   ???????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ????????????????????????
   ?????????????????????[25]??????
   [26]???????????????????????????[27]???????????????????????????

   [28][IMG][29]lxguang_tao
   [30]?????? ??????

     ?????2
       ??????
     ?????
       ???
     ?????[31][IMG] [32]1
       ??????
     ?????[33][IMG] [34][IMG] [35][IMG] [36]0
       ??????
     ?????[37]????????????
       ????????????
     ?????

     ?????[38][IMG]

       ????????????????????????

   ????????????
   [39]tieba_sign::mobile_phone: ????????????????????????????????? ???????????? ????????????-???
   ???
   05-07
   [40]Tieba_Sign ????????????????????????????????? / ???????????? / ???????????? ?????????????????????
   ???????????????207???????????????????????????????????????????????????5s?????????(Cookies???????????????)
   Use???Python3.6?????? ?????? ???????????? 1.???????????? pip install -r
   requirements.txt # Centos yum install zbar -y # Ubuntu sudo apt-get
   install libzbar-dev -y 2.?????????????????? (tieba_sign.py) user_lists = ['??????
   ???'] # ?????????,??????['??????1', '??????2', '??????3'] ??????3????????? # ?????????????????????
   ?????????????????????????????? ?????? python tieba_sign.py # ????????????????????? ???????????????
   ?????????????????????????????????????????????????????????????????????????????????????????????
   [41]python?????????????????????????????????????????????
   [42]weixin_34236869?????????
   06-29 222
   [43]?????????????????????????????????????????????????????? ????????????????????????????????????????????????
   ????????????????????????????????????????????????????????????????????? ???????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ????????????????????????????????????error=257 ????????????????????????????????????????????????????????????
   ?????????????????? ?????????????????????????????? ?????????????????? ...
   ??????1
   [44][IMG]
   [45]
   _____________________
   ???????????? ???????????????~
   [46]????????? ????????????
   [47]????????? ?????????

     ?????HTML/XML
     ?????objective-c
     ?????Ruby
     ?????PHP
     ?????C
     ?????C++
     ?????JavaScript
     ?????Python
     ?????Java
     ?????CSS
     ?????SQL
     ???????????

   [48][??????????] [49][??????????]
   [50]Python?????????????????????????????????
   [51]Packager
   11-28 176
   [52]?????????????????????????????????????????????????????????????????????????????????????????????????????????
   ??????????????? ?????????????????????????????? ??????????????????????????????Beautiful Soup????????????
   ?????????????????????????????????????????????????????? ??????????????????????????????????????????????????????
   ?????????????????????????????????????????????????????????????????????requests??????????????????????????????
   ?????????????????????????????????????????????????????????????????????????????? ????????????????????? #
   -*-...
   [53]Python ???????????????????????????????????????????????????
   ????????????
   [54]???????????????????????????
   11-15 654
   [55]??????????????????????????????????????????????????????????????????????????? ???????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ????????????????????????????????????????????????????????????????????? ????????????????????? ???????????? ???
   ??????????????? ?????????????????????????????? 1. ???????????? ??????????????????????????????
   https://tieba.baidu.com/p/6516084831 ??? ????????? url ???????????????????????????
   6516084831 ???????????? id ??? ??? ??????????????????????????? ???????????????????????????????????????
   ?????? ht

   [56]Python???????????????????????????
   [57]ljc545w?????????
   12-11 872
   [58]????????????????????????????????????????????????????????????????????????????????????gid???????????????
   ??????????????????????????????cookie???????????????????????? ???????????? ????????????????????????BDUSS
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????python
   ???requests????????????Chrome???????????????????????????????????????????????????????????????????????????
   ????????????????????????????????????????????? ???????????? ??????????????? ??????Chrome??????????????????
   ???baidu.com????????????co
   [59]python??????????????????
   [60]kaerbuka?????????
   07-02 786
   [61]??????????????? ?????? ?????? ???????????? ?????????????????? ???????????????????????? ???????????????
   ?????? ???????????????????????????????????????????????????????????????????????????????????????????????????1???
   ????????????????????????????????????????????????????????????cookie??????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ?????????????????????????????????????????????????????????????????????????????????????????? ???????????? ???
   ???python...
   [62]Python??????????????????????????????????????????????????????http?????????
   [63]??????????????????
   01-03 368
   [64]?????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ?????????1%??????????????????????????? ?????????????????????????????????????????????????????????????????????
   ????????????????????????????????????????????? ...
   [65]17-???python????????????????????????
   [66]bigzql?????????
   10-13 1???+
   [67]?????????????????????????????? https://huaban.com/ ??????????????????????????????!????????????
   ????????????????????????,?????????????????????????????? ??????????????? requests ????????????????????????
   ????????????????????????json??????????????????????????????????????????????????? ??????????????? ??? ??????
   ????????? python ?????? requests ??????????????????session??????????????????????????? ????????????
   ??? ??????????????????????????? json???????????????????????? ?????? ????????????
   https://huaban.com/search/?q=??????&catego
   [68]????????????|Python????????????????????????????????????????????????--20190925???????????????
   [69]??????????????????????????????????????????
   09-25 4719
   [70]????????????|Python???????????????????????????????????????????????? ??????????????????
   ???http://www.360doc.com/content/18/0801/00/2990557_774796873.shtml????????????
   ??????python?????????????????? ???????????????????????? 7???16???????????? Python?????????????????????
   ??????????????????????????????????????????????????? ??????????????????...
   [71]python????????????????????????_python?????????????????????????????????????????????
   [72]weixin_39974223?????????
   12-03 166
   [73]?????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ??????????????????????????????error=257??????????????????????????????????????????????????????????????????
   ???????????? ?????????????????????????????? ??????????????????????????????????????????????????????????????????
   ??????????????????post??????...
   [74]python??????-qpython??????
   [75]q6q6q?????????
   10-28 250
   [76]????????????????????????11?????????????????????????????????????????????????????????????????????88??????
   ??????????????????????????????????????????5000????????????1. url????????? 2. ????????????2.1. ??????
   ???????????????2.2. ??????????????????????????? 3. get???post?????????3.1. get??????3.2. post
   ??????3.3. ????????????????????????post??????...wd=%e7%bc%96%e7%a8%8b%e5%90%a7????????????
   ??????pyth...
   [77]????????????????????????????????????
   [78]?????????
   08-19 161
   [79]??????????????????????????????????????????????????? ???????????????????????????????????????????????????
   ????????? ???????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????? ????????????????????????????????????????????????????????????????????????????????????
   ????????????????????????????????? 1????????????????????????2?????????????????????????????????????????????3???
   ??????????????????????????? 3????????????????????????????????? 4?????????????????????????????????????????????
   ???????????????????????????????????????...
   [80]???HTTP???????????????WEB?????????????????????
   [81]???????????????
   01-03 542
   [82]?????????????????????????????????????????????????????????????????????????????????Cookie???????????????
   ????????????????????? ????????? ????????????????????? ??????????????? Url
   ???https://passport.baidu.com/v2/api/getqrcode ???????????????Get ????????????
   ???lp=pc ??????????????????????????????????????????????????????????????????????????????lp??????????????????
   ????????????????????????????????? ??????????????? { ???imgurl???:...
   [83]??????????????????????????????
   [84]??????????????????
   11-07 2898
   [85]??????????????????????????????????????? ????????? ????????? ???????????? ??????????????????????????????
   ???????????????????????????????????????????????????????????? ?????????????????? ??????????????????????????????
   ??????
   https://tieba.baidu.com/f?ie=utf-8&kw=%E8%AF%9A%E6%8B%9B%E4%BB%A3%E7%90%86&fr=search
   ????????????????????????????????????????????????????????????????????????...
   [86]??????????????????????????????????????????????????????
   [87]????????????
   03-07 5039
   [88]?????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ????????????????????????????????????????????????????????????????????????????????????????????? ???????????????
   ??????????????????????????????????????????????????????????????????????????????????????????????????????csdn???
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ??????????????????????????????????????????...
   [89]Golang ?????????????????????
   [90]ALakers?????????
   12-24 262
   [91]??????????????? http_client.go??????????????? package client import ( "bytes"
   "fmt" "io" "io/ioutil" "net/http" "net/http/cookiejar" "net/url" "strings"
   "time" ) // HTTPClient http client type HTTPClient struct { *http.Client
   UserAgent string } var ( UserAgen
   [92]1.????????????????????????html&???????????????
   [93]python??????????????????
   10-10 3141
   [94]??????????????????????????????????????????????????????????????????????????????html??????????????????
   ???html?????????????????????????????????JAVA???JAVA????????????????????????Python???Python?????????
   ????????????????????????????????????html????????????????????????????????????html???????????????????????????
   ???????????????????????? ??????????????? ???1 ???2 ????????????????????????????????????????????????
   ???https://www.baidu.com/????????????????????????...
   [95]???????????????????????????????????????????????????
   ????????????
   [96]kimol????????????
   10-03 2???+
   [97]?????????????????????????????????????????????????????????????????????????????????????????????ID1.??????
   ?????????URL2.??????????????????UUID3.??????????????????????????????????????????????????? ?????? ??????
   ???????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ??????????????????????????? ?????????????????????????????????????????????~ ???ps.???????????????????????????
   ???????????????????????? ????????????????????????????????????????????? ?????????????????? ??????????????????
   ????????????????????????????????????????????????????????????????????????????????????????????????????????????
   ???????????????xxxxxx???????????????UUID??? h
   ?????2021 CSDN ????????????: ??????-??? ?????????:????????? [98]????????????
   [99][IMG]
   [100]lxguang_tao  CSDN?????????????????? CSDN??????????????????
   ??????7??? [101][IMG] [102]????????????

   3
   ??????

   27???+
   ?????????

   25???+
   ?????????

   2242
   ??????

   [103][IMG]
   ??????

   44
   ??????

   14
   ??????

   6
   ??????

   1
   ??????

   7
   ??????
   [104]GitHub
   [105]????????????
   [106]????????????
   [107]????????????Lv1
   [108]????????????
   [109]??????
   ??????
   [110]_____________________

  ????????????

     ?????[111]???????????????????????????--python?????? [112][IMG] [113]539
     ?????[114]C# ?????????visual studio???????????????????????? [115][IMG] [116]122
     ?????[117]windows???????????????docker????????????????????????????????? [118][IMG] [119]69

  ????????????

     ?????[120][IMG] [121]python 1???
     ?????[122][IMG] [123]C# 1???

  ????????????

     ?????[124]???????????????????????????--python??????

       [125]??????: ??????????????????????????????????????????????????????

  ???????????????????????????????????????????????????

     ?????
       ???????????????
     ?????
       ?????????
     ?????
       ?????????
     ?????
       ??????
     ?????
       ????????????

   [126]_____________________ ??????

  ????????????

     ?????[127]windows???????????????docker?????????????????????????????????
     ?????[128]C# ?????????visual studio????????????????????????

   [129]2021???2???
   [130]2020???1???

   [131]IFrame

  ??????

  ??????

   [132]IFrame

  ????????????

     ?????[133][IMG] [134]python 1???
     ?????[135][IMG] [136]C# 1???

   ?????????
   [137]??????????????????
   ??????????????????
   ????????????
   [138](??) ???????????? 0

   ???????????????

   1.?????????????????????????????????????????????1:1???????????????????????????????????????
   2.?????????????????????????????????????????????VIP???C????????????????????????????????????

   [139][IMG][140]????????????

References

   Visible links
   1. https://blog.csdn.net/qq_27644127/article/details/112987332
   2. file:///data/data/com.termux/files/home/works/tieba_job/content.html#
   3. https://blog.csdn.net/qq_27644127
   4. https://blog.csdn.net/qq_27644127/category_10614803.html
   5. https://so.csdn.net/so/search/s.do?q=python&t=blog&o=vip&s=&l=&f=&viparticle=
   6. http://creativecommons.org/licenses/by-sa/4.0/
   7. https://blog.csdn.net/qq_27644127/article/details/112987332
   8. https://blog.csdn.net/qq_27644127/category_10614803.html
   9. python
	https://blog.csdn.net/qq_27644127/category_10614803.html
  10. file:///data/data/com.termux/files/home/works/tieba_job/content.html#_1
  11. file:///data/data/com.termux/files/home/works/tieba_job/content.html#_5
  12. file:///data/data/com.termux/files/home/works/tieba_job/content.html#_37
  13. file:///data/data/com.termux/files/home/works/tieba_job/content.html#_39
  14. file:///data/data/com.termux/files/home/works/tieba_job/content.html#_40
  15. file:///data/data/com.termux/files/home/works/tieba_job/content.html#_42
  16. file:///data/data/com.termux/files/home/works/tieba_job/content.html#_192
  25. http://file.taotaoya.top/load/TT.rar
  28. https://blog.csdn.net/qq_27644127
  29. https://blog.csdn.net/qq_27644127
  30. javascript:;
  31. file:///data/data/com.termux/files/home/works/tieba_job/content.html#commentBox
  32. file:///data/data/com.termux/files/home/works/tieba_job/content.html#commentBox
  33. javascript:;
  34. javascript:;
  35. javascript:;
  36. javascript:;
  37. javascript:;
  38. javascript:;
  39. https://download.csdn.net/download/weixin_42122432/18441287
  40. https://download.csdn.net/download/weixin_42122432/18441287
  41. https://blog.csdn.net/weixin_34236869/article/details/86453208
  42. https://blog.csdn.net/weixin_34236869
  43. https://blog.csdn.net/weixin_34236869/article/details/86453208
  44. javascript:void(0);
  50. https://lmsoft.blog.csdn.net/article/details/84582372
  51. https://blog.csdn.net/qq_41287993
  52. https://lmsoft.blog.csdn.net/article/details/84582372
  53. https://smartcrane.blog.csdn.net/article/details/121341944
  54. https://blog.csdn.net/wenxuhonghe
  55. https://smartcrane.blog.csdn.net/article/details/121341944
  56. https://blog.csdn.net/ljc545w/article/details/111054624
  57. https://blog.csdn.net/ljc545w
  58. https://blog.csdn.net/ljc545w/article/details/111054624
  59. https://blog.csdn.net/kaerbuka/article/details/94471507
  60. https://blog.csdn.net/kaerbuka
  61. https://blog.csdn.net/kaerbuka/article/details/94471507
  62. https://blog.csdn.net/cxcjoker7894/article/details/85685115
  63. https://blog.csdn.net/cxcjoker7894
  64. https://blog.csdn.net/cxcjoker7894/article/details/85685115
  65. https://cpython.blog.csdn.net/article/details/109063267
  66. https://blog.csdn.net/bigzql
  67. https://cpython.blog.csdn.net/article/details/109063267
  68. https://blog.csdn.net/qq_32670879/article/details/101391892
  69. https://blog.csdn.net/qq_32670879
  70. https://blog.csdn.net/qq_32670879/article/details/101391892
  71. https://blog.csdn.net/weixin_39974223/article/details/110545065
  72. https://blog.csdn.net/weixin_39974223
  73. https://blog.csdn.net/weixin_39974223/article/details/110545065
  74. https://blog.csdn.net/q6q6q/article/details/109346811
  75. https://blog.csdn.net/q6q6q
  76. https://blog.csdn.net/q6q6q/article/details/109346811
  77. https://blog.csdn.net/u013177154/article/details/99288349
  78. https://blog.csdn.net/u013177154
  79. https://blog.csdn.net/u013177154/article/details/99288349
  80. https://blog.csdn.net/d745282469/article/details/103819585
  81. https://blog.csdn.net/d745282469
  82. https://blog.csdn.net/d745282469/article/details/103819585
  83. https://blog.csdn.net/weixin_44027887/article/details/102948182
  84. https://blog.csdn.net/weixin_44027887
  85. https://blog.csdn.net/weixin_44027887/article/details/102948182
  86. https://blog.csdn.net/qq_15159657/article/details/104721232
  87. https://blog.csdn.net/qq_15159657
  88. https://blog.csdn.net/qq_15159657/article/details/104721232
  89. https://blog.csdn.net/ALakers/article/details/111619137
  90. https://blog.csdn.net/ALakers
  91. https://blog.csdn.net/ALakers/article/details/111619137
  92. https://blog.csdn.net/weixin_42830697/article/details/102474659
  93. https://blog.csdn.net/weixin_42830697
  94. https://blog.csdn.net/weixin_42830697/article/details/102474659
  95. https://blog.csdn.net/kimol_justdo/article/details/108912073
  96. https://blog.csdn.net/kimol_justdo
  97. https://blog.csdn.net/kimol_justdo/article/details/108912073
  98. https://blog.csdn.net/
  99. https://blog.csdn.net/qq_27644127
 100. lxguang_tao
	https://blog.csdn.net/qq_27644127
 101. https://i.csdn.net/#/uc/profile?utm_source=14998968
 102. ????????????
	https://i.csdn.net/#/uc/profile?utm_source=14998968
 103. https://blog.csdn.net/blogdevteam/article/details/103478461
 109. https://im.csdn.net/chat/qq_27644127
 111. https://blog.csdn.net/qq_27644127/article/details/112987332
 112. https://blog.csdn.net/qq_27644127/article/details/112987332
 113. https://blog.csdn.net/qq_27644127/article/details/112987332
 114. https://blog.csdn.net/qq_27644127/article/details/111566657
 115. https://blog.csdn.net/qq_27644127/article/details/111566657
 116. https://blog.csdn.net/qq_27644127/article/details/111566657
 117. https://blog.csdn.net/qq_27644127/article/details/118380655
 118. https://blog.csdn.net/qq_27644127/article/details/118380655
 119. https://blog.csdn.net/qq_27644127/article/details/118380655
 120. https://blog.csdn.net/qq_27644127/category_10614803.html
 121. https://blog.csdn.net/qq_27644127/category_10614803.html
 122. https://blog.csdn.net/qq_27644127/category_10685120.html
 123. https://blog.csdn.net/qq_27644127/category_10685120.html
 124. https://blog.csdn.net/qq_27644127/article/details/112987332#comments_14757654
 125. https://blog.csdn.net/m0_50944918
 127. https://blog.csdn.net/qq_27644127/article/details/118380655
 128. https://blog.csdn.net/qq_27644127/article/details/111566657
 129. https://blog.csdn.net/qq_27644127/article/month/2021/07
 130. https://blog.csdn.net/qq_27644127/article/month/2020/12
 131. https://kunpeng-sc.csdnimg.cn/?timestamp=1623163941/#/preview/8608?positionId=57&queryWord=&spm=1001.2101.3001.5001
 132. https://kunpeng-sc.csdnimg.cn/?timestamp=1623163941/#/preview/8608?positionId=479&queryWord=&spm=1001.2101.3001.4834
 133. https://blog.csdn.net/qq_27644127/category_10614803.html
 134. https://blog.csdn.net/qq_27644127/category_10614803.html
 135. https://blog.csdn.net/qq_27644127/category_10685120.html
 136. https://blog.csdn.net/qq_27644127/category_10685120.html
 137. javascript:;
 139. https://i.csdn.net/#/wallet/balance/recharge
 140. https://i.csdn.net/#/wallet/balance/recharge![Image](./187fd2da45fcb4448f060830c830f812.png)![Image](./187fd2da45fcb4448f060830c830f812.png)

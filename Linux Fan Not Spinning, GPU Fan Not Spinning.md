---
tags: [fan, hardware, linux, security, system manage, thermal]
title: 'Linux Fan Not Spinning, GPU Fan Not Spinning'
created: '2022-08-11T04:25:28.086Z'
modified: '2022-08-29T06:11:41.491Z'
---

# Linux Fan Not Spinning, GPU Fan Not Spinning

i have install something other than that. like i8kctl, some thermal controllers by intel (thermald)? but still gpu fan not spinning till now.

```bash
apt install -y lm-sensors fancontrol
sensors-detect
pwmconfig
```
already have cpu frequency under control by running temp_throttle.sh

---
tags: [hardware, system manage]
title: Linux Fan Not Spinning
created: '2022-08-11T04:25:28.086Z'
modified: '2022-08-18T07:41:59.817Z'
---

# Linux Fan Not Spinning

i have install something other than that. like i8kctl, some thermal controllers by intel (thermald)? but still gpu fan not spinning till now.

```bash
apt install -y lm-sensors fancontrol
sensors-detect
pwmconfig
```
already have cpu frequency under control by running temp_throttle.sh


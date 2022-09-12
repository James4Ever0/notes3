---
title: 'song recognition, music recognition api'
created: '2022-09-12T15:40:57.656Z'
modified: '2022-09-12T16:30:44.224Z'
---

# song recognition, music recognition api

## self-hosted

## audiotag.info

[wav_to_info.py](https://github.com/whuds/song-classifier/blob/7c6771312e45a0f72f966a77506317d5cc98212a/metadata/code/wav_to_info.py)



## 

## midomi houndify soundhound

to get track info from soundhound (no cookie):
https://www.midomi.com/api/track?trackID=100282107076607645

the houndify music recognition api:
wss://houndify.midomi.com/

some lib for midomi found over [here](https://github.com/Azarattum/AmadeusCore/blob/3bbb39e4d92508f036dd7be68b66681013866cba/src/components/app/models/recognizers/midomi.recognizer.ts)
it can also bridge yandex music recognition api

houndify also have api for that, but requires credit

free credits per day: 100

[soundhound now](https://docs.houndify.com/reference/SoundHoundNowCommand#field_SingleTrackResult) requires 1 credit

[soundhound python sdk](https://pypi.org/project/Houndify)

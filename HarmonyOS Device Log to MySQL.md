---
title: HarmonyOS Device Log to MySQL
created: '2022-07-14T07:47:35.702Z'
modified: '2022-07-14T08:01:17.784Z'
---

# HarmonyOS Device Log to MySQL

Logs Path:
/data/data/Local/DeviceTest/20220406163617_hts_project/resources/HTS/android-hts/logs

under logs:
%Y.%m.%d_%H.%M.%S

under selected folder:
device_logcat-

Tables:

Performance_Baseline_Info
testValue date(%Y-%m-%d) hmsVersion(HMSCore660319) baselineId_id deviceId_id(1,2,4,3,5) deviceType(phone<-1|wearable<-2|car<-4|tv<-3|ecodevice<-5)

Performance_Daily_Data
id features indicators baseValue

Performance_Device_Info
id(to the deviceId_id) model type sn cpu





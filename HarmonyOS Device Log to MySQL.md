---
title: HarmonyOS Device Log to MySQL
created: '2022-07-14T07:47:35.702Z'
modified: '2022-07-14T08:44:26.825Z'
---

# HarmonyOS Device Log to MySQL

Logs Path:
/data/data/Local/DeviceTest/20220406163617_hts_project/resources/HTS/android-hts/logs

under logs:
%Y.%m.%d_%H.%M.%S_<serial_number>
select the latest folder

under selected folder:
device_logcat_test_<serial_number>_<unknownInteger>.txt.gz

decompress using:
gzip -d 

does the decompression remove the .gz file?
it will.

log format:

A1test1..4
A2test5
A3test1..2
B1test1


Tables:

Performance_Baseline_Info
testValue date(%Y-%m-%d) hmsVersion(HMSCore660319) baselineId_id deviceId_id(1,2,4,3,5) deviceType(phone<-1|wearable<-2|car<-4|tv<-3|ecodevice<-5)

Performance_Daily_Data
id features indicators baseValue

Performance_Device_Info
id(to the deviceId_id) model type sn cpu





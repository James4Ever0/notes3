---
title: vapoursynth 光流算法 补帧
created: '2022-09-07T03:59:21.000Z'
modified: '2022-09-07T04:27:52.370Z'
---

# vapoursynth 光流算法 补帧

补帧算法可适用于我们的动态水印追踪系统 但是可能需要优化 才能做到比较快速的补帧 因为水印所在位置的区间实际上只是白色的 不需要过于复杂的网络 同时这种补出来的水印需要逐帧处理 或者两帧一处理 生成的区间数量会非常的多

[python opencv 光流算法详解](https://learnopencv.com/optical-flow-in-opencv/)



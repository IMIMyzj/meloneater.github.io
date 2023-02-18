---
title: 「音频引擎」 基于PulseAudio的Linux音频功能解析
date: 2023-2-18
tags:  [音频引擎, RTC, Linux, PulseAudio]
---

# 一、背景
　　PulseAudio是Linux系统中通用的音频服务器，预装于大部分的Linux发行版中，因此系统兼容性较好。其位于Linux内核级的ALSA (Advanced Linux Sound Architecture)之上，设计目标包括硬件抽象、易于调用、灵活性好、可拓展等，整体框图如下所示：

<img src="https://raw.githubusercontent.com/MelonEater/blog-pic/raw/main/audioEngine_pulseAudio/chapter_1-struct.png" alt="chapter-1-struct" width="50%">

　　在[Webrtc的开源代码库](https://webrtc.googlesource.com/src/+/refs/heads/main)中，linux端设备采集播放实现有两套方案，即ALSA和PulseAudio。本文将基于webrtc的audio_device框架以及实践过程中总结的经验，重点阐述以下两个方面：
  1. 如何实现音频采集和播放功能；
  2. 如何实现设备枚举、音量控制和音频事件监听这三种设备控制功能

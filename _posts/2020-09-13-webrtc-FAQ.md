---
layout: post
title: webrtc技术探讨
categories: RTC
description: webrtc技术探讨
keywords: webrtc, RTC
# topmost: true
---

# webrtc技术探讨

## 怎么确定是Webrtc的 rtp 首包seqNumber?

  因为没有像tcp那样三次握手来同步序列号SeqNumber。

  协议上webrtc的首个rtp包seqNumber是随机生成的。只是mediasoup 通过plainRtp发出的是从seqNummber=1开始的。
 
  判断不了首包？
  
  通过收到h264的SPS，PPS来确定有效的包；之前的包丢弃。
  
  【注】这样RTP包与视频帧IDR强相关。这个问题问了很多人了，还是很困惑。

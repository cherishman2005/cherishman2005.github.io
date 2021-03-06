---
layout: post
title: 基于开源项目搭建CSDN直播服务
categories: RTC
description: 基于开源项目搭建CSDN直播服务
keywords: RTC, RTM, CDN
# topmost: true
---

# 基于开源项目搭建CSDN直播服务

利用开源平台，CSDN采用5个人，不到2个月时间开发出万人直播平台。

![CSDN直播架构](/images/posts/rtc/csdn-live-architecture.png)

支持万人并发。之所以这么快，是充分利用了开源和API。


【注】CSDN创始人 蒋涛 在《RTE2020实时互联网大会》上分享的CSDN直播系统架构。

# 小结

* 以后音视频会成为每款app的标配或附带功能。

* 多利用和借鉴开源项目 搭建RTC直播系统。快速开发、上线，运行稳定；并不断迭代。

* 在华为视频PaaS平台部门时，当时部门也准备做RTC连麦互动直播系统，我充分利用开源kurento（webrtc），nginx-rtmp快速搭建原型demo。

* 积极拥抱开源。
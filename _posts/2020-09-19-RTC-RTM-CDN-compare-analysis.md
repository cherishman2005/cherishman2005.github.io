---
layout: post
title: RTC-RTM-CDN设计比较分析
categories: RTC
description: RTC-RTM-CDN设计比较分析
keywords: RTC, RTM, CDN
# topmost: true
---

# RTC和RTM设计比较分析

* 客户端SDK与后端之间的配合:

  在设计时尽量让SDK做薄，简单易用; 后端 高可靠，高可用，容灾等。
  
  * 在定时机制方面，尽量遵循分布式系统设计原则；

## 调度（RTC/RTM、CDN）

* RTM与RTC的调度对比

  * webjs SDK与native sdk调度的区别
  
    js是需要支持https域名调度，一般不支持httpDNS。
  
  * RTC高并发，耗流量；—— 需要考虑更精准的就近调度

  * RTM调度：

    在国内，采用BGP/多线机房 基本就能满足即时信令传输；

    随着网络质量越来越好， 调度不用精准；—— 除非体量大。
  
  * 对RTC/RTM CDN的调度： 追求极致用户体验，可以考虑深度优化。

## 分发

  * CDN:

    一般采用 分级分发架构；
  
  * RTM:

    一般采用 分级分发架构；
  
  * RTC:

    一般不会采用 分级架构；—— 选路非常关键。

# 小结

* IM和RTM即时信令场景

  * IM: 

    不丢消息非常关键，可以借鉴webrtc NACK重传机制 让包收齐；

    sdk层可借鉴下jitter-buffer来重消息重排； 在展示时 前端可以再进行 重传包 重排修正。

  * RTM即时信令：
    
    即时信令一般配合RTC做控制信令，更加强调实时：即时消费，即时销毁。—— 设置不用做历史缓存。

  * CDN
    如果将RTM配合到CDN系统，应该可以更好的应对突发流量；即时感知突发，调整调度策略，及时分流。

# Author

zhangbiwu

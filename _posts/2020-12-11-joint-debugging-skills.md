---
layout: post
title: rpc联调技巧
categories: RPC
description: rpc联调技巧
keywords: RPC
# topmost: true
---

# rpc联调技巧

**rpc链路**

client ==>  channel（通道：前端接入，路由选择，负载均衡） ==》 业务后端（service）


调试确定sdk发送是否打包ok。然后 后端 确认，再可以让channel通道跟踪下。

**调试诀窍：**

（1）前端业务开发人员：前端业务（或sdk）开发  应用层协议是否封装符合要求？（保证数据发送出去） —— 前端业务开发必备技能；

（2）对应后端业务开发人员： 通过traceId分析 是否接收到请求；然后请求是否符合要求？

（3）channel通道同事: 最后让channel同事通过traceId协助排查。

（4）最终的杀手锏： 各个环节抓包。

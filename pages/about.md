---
layout: page
title: About
description: nginx，RTC/RTM即时通信，CDN技术交流
keywords: Biwu Zhang, 张必武
comments: true
menu: 关于
permalink: /about/
---

我是阿武，欢迎进行nginx(openresty)，RTC/RTM即时通信，CDN技术交流。

* nginx(openresty): 成熟的优秀开源服务器；

* RTC: Real-Time Communication；

* RTM: Real-Time Message;

* CDN: Content Delivery Network;


## 华为工作经历

* 基于nginx(openresty)的即时转封装框架设计与开发；

* 基于nginx(openresty)的直播cache缓存服务器(CDN)设计与开发；

* RTC连麦互动直播系统预研与设计，RTC-demo(webrtc)实现第一人。


## 其他

* 作为技术和项目负责人：（主导设计后端，前端，console控制台；并上线商用）
  * 设计并开发微商城公众号，微商城小程序；
  * 设计并开发一物一码商品跟踪溯源系统；


## 主要技术栈

* 后端研发
  * nginx/openresty
  * C/C++
  * nodejs
  * js-sdk
  * RTM/RTC


## 联系

<ul>
{% for website in site.data.social %}
<li>{{website.sitename }}：<a href="{{ website.url }}" target="_blank">@{{ website.name }}</a></li>
{% endfor %}
{% if site.url contains 'https://cherishman2005.github.io' %}
{% endif %}
</ul>


## Skill Keywords

{% for skill in site.data.skills %}
### {{ skill.name }}
<div class="btn-inline">
{% for keyword in skill.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}

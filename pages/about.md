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


华为工作经历：

* 基于nginx(openresty)的即时转封装框架设计与开发；

* 基于nginx(openresty)的直播cache缓存服务器(CDN)设计与开发；

* RTC连麦互动直播系统预研与设计，RTC-demo实现第一人。

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

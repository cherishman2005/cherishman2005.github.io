---
layout: post
title: nginx开发心得
categories: nginx
description: nginx开发心得
keywords: nginx, CDN
# topmost: true
---

# nginx

* HTTP/HTTPS API网关

* 反向代理，负载均衡

* http proxy-cache CDN

* web容器


## nginx c module 开发注意事项

* handler阶段不要耗时太长

* 基于nginx框架的开发建议

  * 业务逻辑控制采用lua脚本；经典、基础的功能开发采用C/C++ module。

     —— 这样尽可能保证代码质量高：高内聚，低耦合；


## nginx API网关优势

nginx轻量级，稳定的web服务器；

* http七层静态负载均衡

* tcp四层负载均衡

* udp四层负载均衡

* 通过 c module或lua二次开发支持七层/四层动态负载均衡；
  —— 完全可以做到不重启nginx就可以添加或摘掉后端服务。

* access接入控制

* 速率控制

* 支持http2

## nginx CDN

* nginx cdn控制接入层

  —— 各CDN厂商均会采用nginx做控制接入层

* nignx http proxy-cache 缓存加速

  —— 自建CDN web静态小文件加速，初始阶段可直接采用nginx proxy-cache模块做缓存加速；

# FAQ

## openresty+lua开发后端业务逻辑心得

  `openresty适合做接入控制层、API网关`

  曾经负责过一个（openresty + lua + mysql）+ vue的商城购物小程序/公众号项目。

  所有的商品列表，订单，支付，均采用lua-API对接mysql。

  * 好处： 

    技术栈单一，技术栈可以做精；

  * 坏处： 

    * lua-API对接mysql，后续系统扩展升级不方便；特别是针对后面的微服务架构升级。


   如果重新选择技术栈，我会采用openresty做接入API网关；后端业务选择nodejs，开发小程序购物商城 效率太高了。

   —— 不会再选择openresty + mysql做后端业务。

   如果是团队作战，最好选择大家熟悉的技术栈，如nodejs/go/java等写后端业务逻辑。


## nginx http-range

RFC2616规范中定义了range协议： 一次请求只下载完整文件的某一部分。


在基于nginx做即时转封装时遇到range的一个大坑。

* 需要采用subrequest拉取完整分片，然后转封装后再执行range；

* 如果采用upstream + filter，在body-filter做转封装的设计； nginx执行流程就会出现先range，后转封装；——达不到预期。

## nginx.conf增加配置项时，nginx c/c++ module做好异常保护

   —— 可以观察nginx  worker进程PID是否在不断变化。如果不断变化，说明程序里面有bug。

## 注意写权限

拷贝时权限有变化。如： cp njs_shared_dict.db  share_dict.db
```
-rwxrwxrwx 1 zhangbiwu zhangbiwu   26 Nov  2 09:48 njs_shared_dict.db
-rwxrwxr-x 1 zhangbiwu zhangbiwu   26 Nov  2 09:48 share_dict.db
```
注意写权限的变化

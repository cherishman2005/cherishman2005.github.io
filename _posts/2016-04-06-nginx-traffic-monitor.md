---
layout: post
title:  nginx监控模块部分功能开发
categories: nginx
description: nginx监控模块部分功能开发
keywords: nginx,lua,openresty
# topmost: true
---

# nginx监控模块部分功能开发

监控系统的开发是linux后台系统的必备技术，应用于接入控制层，CDN节点，微服务架构系统。本文介绍Nginx监控系统开发的部分功能。实现如下功能：

（1）请求次数统计；

（2）响应状态次数统计；

（3）请求和响应报文的流量统计；

这里只是粗略实现功能，需要根据实际需求，添加时间维度进行统计，并进行测试调优；同时结合前端开发将统计信息以各种方式呈现。另外还可扩充proxy_pass，proxy_cache以及redis_pass内存缓存的流量统计。

Ngx_lua（Openresty）开发可以提高开发效率，并通过reload时，实现无缝更新，之前的数据不丢失；Nginx C Module运行效率更高，采用Nginx C开发，能够更好驾驭Nginx，掌握Nginx的精髓。

## Ngx_lua实现

充分利用ngx_lua的API进行开发。并通过shared_dict进行共享。

（1）在http{}段配置共享内存traffic_data

lua_shared_dict traffic_data 10m;

 

（2）在server{}段配置log_ly_lua_file

（3）在location /mytraffic_ua配置 content_by_lua_file

       log_by_lua_file /usr/local/nginx/lua/traffic/get_traffic_info.lua;

       location /mytraffic_lua {

           default_type "text/html";

           content_by_lua_file /usr/local/nginx/lua/traffic/show_traffic_info.lua;

       }

 

【注】详见gitHub。

## Nginx C Module实现

开发Nginx C 模块ngx_http_traffic_status_module。详见gitHub。

nginx.conf配置如下：

       location /mytraffic {

           traffic_statistics request_times packet_bytes status_codes;

       }

 

       location /mytraffic1 {

           traffic_statistics request_times;

       }

 

       location /mytraffic2 {

           traffic_statistics packet_bytes;

       }

 

       location /mytraffic3 {

           traffic_statistics status_codes;

       }

 

运行示例如下：

root@ubuntu:/usr/local/nginx/sbin# curl -k http://192.168.137.134:8080/mytraffic

http request times: 5

recevie packet bytes: 467

send packet bytes: 1423

---- http status ----

---------------------

200: 4

404: 1

---------------------


## 提交代码到gitHub

- [https://github.com/cherishman2005/ngx_http_traffic_status_module](https://github.com/cherishman2005/ngx_http_traffic_status_module)

# 参考资料

- [http://tengine.taobao.org/book/](http://tengine.taobao.org/book/)

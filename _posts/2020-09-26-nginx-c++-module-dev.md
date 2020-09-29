---
layout: post
title: nginx c++ module开发
categories: nginx
description: nginx c++ module开发
keywords: nginx, openresty
# topmost: true
---

# 开发nginx c module时的一些调试技巧

* CPP/H文件添加extern "C"

  ```
  extern "C" {
  #include <ngx_config.h>
  #include <ngx_core.h>
  #include <ngx_http.h>
  }
  ```

* 修改Makefile支持CPP编译和链接

  build/nginx-1.13.6/objs/Makefile
  ```
  CXX = g++
  LINK = $(CXX)
  CXXFLAGS =  -pipe  -O -W -Wall -std=c++11 -Wpointer-arith -Wno-unused-parameter -Werror
  ```
  
  待细化。。。
---
layout: post
title: IM API设计分析
categories: RTM
description: IM API设计分析
keywords: IM, RTM
# topmost: true
---

<!-- TOC -->

- [topmost: true](#topmost-true)
- [IM API设计分析](#im-api设计分析)
    - [腾讯 IM API](#腾讯-im-api)
        - [登录相关](#登录相关)
        - [消息](#消息)
        - [会话](#会话)
        - [资料](#资料)
        - [群组](#群组)
        - [群成员](#群成员)
        - [其他](#其他)
    - [声网RTM API](#声网rtm-api)
        - [登录状态管理](#登录状态管理)
    - [环信IM API](#环信im-api)
- [FAQ](#faq)
    - [命名对应关系](#命名对应关系)
    - [文件存储功能](#文件存储功能)
- [参考链接](#参考链接)

<!-- /TOC -->

# IM API设计分析

本文主要针对业界RTM/IM标杆企业（腾讯、声网、环信等）的API简单分析。

| 公司（产品）     | 比较分析    |
| -------- | ------- |
| 腾讯IM         | 功能非常完善（值的借鉴）；API接口异步回调；|
| 声网RTM         | 从即时信令RTM发展起来，已加入上传图片功能（没有会话管理功能）；API接口也非常规范，值的借鉴 |
| 环信IM         | 功能较全。API接口异步返回还是采用传统的回调函数；|

## 腾讯 IM API


### 登录相关

| API                      | 描述                                  |
|:--------------------------|:--------------------------------------|
| login     | 登录。                      |
| logout	| 登录。                      |

### 消息

| API                      | 描述                                  |
|:--------------------------|:--------------------------------------|
| createTextMessage     | 创建文本消息。                      |
| createImageMessage	| 创建图片消息。                      |
| createAudioMessage	| 创建音频消息。                      |
| createVideoMessage	| 创建视频消息。                      |
| createCustomMessage	| 创建自定义消息。                    |
| createFaceMessage	    | 创建表情消息。                      |
| createFileMessage	    | 创建文件消息。                      |
| sendMessage	        | 发送消息。                          |
| revokeMessage	        | 撤回消息。                          |
| resendMessage	        | 重发消息。                          |
| getMessageList	    | 获取消息列表。                      |
| setMessageRead	    | 设置消息已读。                      |


### 会话

| API                      | 描述                                  |
|:--------------------------|:--------------------------------------|
| getConversationList       | 获取会话列表。                      |
| getConversationProfile    | 获取会话资料。                      |
| deleteConversation        | 删除会话。                          |

### 资料

| API                      | 描述                                  |
|:--------------------------|:--------------------------------------|
| getMyProfile          | 获取个人资料。                             |
| getUserProfile        | 获取其他用户资料。                          |
| updateMyProfile       | 更新个人资料。                              |
| getBlacklist          | 获取我的黑名单列表。                         |
| addToBlacklist        | 添加用户到黑名单列表。                       |
| removeFromBlacklist   | 将用户从黑名单中移除。                       |

### 群组

| API                      | 描述                                  |
|:--------------------------|:--------------------------------------|
| getGroupList           | 获取群组列表。                             |
| getGroupProfile        | 获取群详细资料。                          |
| createGroup            | 创建群组。                          |
| dismissGroup           | 解散群组。                          |
| updateGroupProfile     | 修改群组资料。                          |
| joinGroup              | 申请加群。                          |
| quitGroup              | 退出群组。                          |
| searchGroupByID        | 搜索群组。                          |
| changeGroupOwner       | 转让群组。                          |
| handleGroupApplication | 处理申请加群。                       |
| setMessageRemindType   | 设置群消息提示类型。                  |

### 群成员

| API                      | 描述                                  |
|:--------------------------|:--------------------------------------|
| getGroupMemberList        | 获取群成员列表。                       |
| getGroupMemberProfile     | 获取群成员资料。                       |
| addGroupMember            | 添加群成员。                           |
| deleteGroupMember         | 删除群成员。                           |
| setGroupMemberMuteTime    | 设置群成员的禁言时间。                  |
| setGroupMemberRole        | 修改群成员角色。                       |
| setGroupMemberNameCard    | 设置群成员名片。                       |
| setGroupMemberCustomField | 设置群成员自定义字段。                  |

### 其他

| API                      | 描述                                  |
|:--------------------------|:--------------------------------------|
| on                        | 监听事件。                             |
| off                       | 取消监听事件。                         |
| registerPlugin            | 注册插件。                             |
| setLogLevel               | 设置日志级别。                         |


## 声网RTM API

上传或下载文件或图片

| 方法     | 描述    |
| -------- | ------- |
| createMediaMessageByUploading         | 上传一个文件或图片到 Agora 服务器以获取 RtmFileMessage 实例或 RtmImageMessage 实例，可用于发送频道消息和点对点消息。|
| createMessage         | 创建一个消息实例。对于文件消息和图片消息，如果对应的文件或图片已经上传且 media ID 仍然有效，你无需再次上传文件或图片，可以直接调用此方法获取消息实例用来发送点对点消息或频道消息。|
| downloadMedia         | 通过 media ID 从 Agora 服务器下载文件或图片。|

### 登录状态管理
![connection-state-change](/images/posts/rtm/connection-state-change.png)


## 环信IM API

与腾讯IM类似，返回还是采用传统的回调函数。

# FAQ

## 命名对应关系

* 腾讯API命名“资料”（Profile） 对应声网API命名 “属性”（Attribute）。

## 文件存储功能

* 腾讯QQ 会采用文件助手暂存7天。

# 参考链接

- [腾讯即时通信IM](https://cloud.tencent.com/document/product/269/37411)

- [声网RTM](https://docs.agora.io/cn/Real-time-Messaging/API%20Reference/RTM_web/index.html)

- [环信IM](http://webim-h5.easemob.com/jsdoc/out/connection.html#deleteChatRoomSharedFile)

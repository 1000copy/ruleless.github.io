---
layout: post
title: "TCP/IP协议分层"
description: ""
category: network
tags: [tcp/ip]
---
{% include JB/setup %}

![](/images/network/ProtocolLayer.png)

当 A 主机上的用户进程需要向 B 主机上的用户进程发送数据 i 时，
假如用户进程是基于 TCP 的应用程序：i 先经过 TCP 协议模块，被填入 20 字节 TCP 首部字段，
此时装入 TCP 首部字段的 i 被称为 TCP 报文；然后，经过 IP 层，被填入 20 字节 IP 首部字段，此时的 i 被称为 IP 数据报；
之后 i 经由以太网驱动程序的处理，被填入 14 字节的以太网首部字段，此时的 i 被称为以太网数据帧，之后再被发送到物理链路上。
当 B 主机收到已被封装为以太网数据帧的 i 时：其以太网驱动程序先取出 i 的以太网首部数据，判断其协议类型是 IP 数据报，
于是就将拆分后的 IP 数据报 i 传给 IP 协议模块；IP 层同样也从 i 中取出 IP首部字段，判断其协议类型是 TCP，
于是就将 剩余的 TCP 数据报传输给 TCP 协议模块；TCP 协议模块根据端口号将去除 TCP 首部字段的数据 i 分发给相应的用户进程。

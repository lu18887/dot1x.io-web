+++
title = "IEEE-802.1X-2001-brief"
description = ""
date = 2019-06-28T15:22:39+08:00
weight = 20
draft = false
+++

# IEEE-802.1X-2001-brief
[TOC]
##  0.前言
802.1X是802系列标准中的一员，相关的有802.3局域网以及802.11无线局域网等等。本文是针对IEEE-802.1X-2001文档的一个梳理。本文从原文档的目录顺序进行梳理，目录中的1~10点均与源文档的目录保持一致。
##  1.总览
### 1.1范围
基于端口的网络访问控制利用LAN网络的特性,在认证与授权通过的情况放开网络，认证失败的情况下阻断网络访问。这里的端口可以指LAN端口也可以是WLAN的连接。
### 1.2目的
整个802.1X标准包含以下内容
1. 认证等一系列动作在哪些设备或系统中进行
2. 访问控制机制中的操作原理
3. 定义不同级别的访问控制以及对应访问控制级别下的端口对网络帧的收发行为
4. 网络设备与终端之间的认证协议要求
5. 网络设备与认证服务器之间的认证协议要求
6. 明确了使用认证与授权协议进行访问控制的机制与过程
7. 明确认证与授权协议数据单元在协议交换下的封装
8. 基于端口访问控制的管理方面的说明，包括管理的对象以及管理的操作
9. 使用SNMP实现管理
10. 明确设备遵从此标准需要满足的条件
##  2.相关引用
- 802.1d  1998 MAC Bridges
- 802.1q  1998  VLAN
- 802.1t-2001 802.1d的修正
- 802.3-2000 以太网
- 802.5-1998 令牌环网
- 802.11-1999 WLAN
- [RFC 1155 SMI](https://www.ietf.org/rfc/rfc1155.txt)
- [RFC 1157 SNMP](https://www.ietf.org/rfc/rfc1157.txt)
- [RFC 1212](https://www.ietf.org/rfc/rfc1212.txt)
- [RFC 1213](https://www.ietf.org/rfc/rfc1212.txt)
- [RFC 1215](https://www.ietf.org/rfc/rfc1215.txt)
- [RFC 1305  NTP V3](https://www.ietf.org/rfc/rfc1305.txt)
- [RFC 1901 Community-based SNMPv2](https://www.ietf.org/rfc/rfc1901.txt)
- [RFC 1905 Protocol Operations for SNMPv2](https://www.ietf.org/rfc/rfc1905.txt)
- [RFC 1906 Transport Mappings for SNMPv2](https://www.ietf.org/rfc/rfc1906.txt)
- [RFC 2104 HMAC](https://www.ietf.org/rfc/rfc2104.txt)
- [RFC 2284 PPP EAP](https://www.ietf.org/rfc/rfc2284.txt)
- [RFC 2570](https://www.ietf.org/rfc/rfc2570.txt)
- [RFC 2571](https://www.ietf.org/rfc/rfc2571.txt)
- [RFC 2572](https://www.ietf.org/rfc/rfc2572.txt)
- [RFC 2573](https://www.ietf.org/rfc/rfc2573.txt)
- [RFC 2574](https://www.ietf.org/rfc/rfc2574.txt)
- [RFC 2575](https://www.ietf.org/rfc/rfc2575.txt)
- [RFC 2578](https://www.ietf.org/rfc/rfc2578.txt)
- [RFC 2579](https://www.ietf.org/rfc/rfc2579.txt)
- [RFC 2580](https://www.ietf.org/rfc/rfc2580.txt)
- [RFC 2716 PPP EAP TLS Authentication Protocol](https://www.ietf.org/rfc/rfc2716.txt)
- [RFC 2863 IF-MMIB](https://tools.ietf.org/html/rfc2863)
- [RFC 2865 RADIUS](https://www.ietf.org/rfc/rfc2865.txt)
- [RFC 2866 RADIUS Accounting](https://www.ietf.org/rfc/rfc2866.txt)
- [RFC 2867](https://www.ietf.org/rfc/rfc2867.txt)
- [RFC 2868](https://www.ietf.org/rfc/rfc2868.txt)
- [RFC 2869](https://www.ietf.org/rfc/rfc2869.txt)
- ISO/IEC 8824:1990 Information technologyOpen Systems InterconnectionSpecification of Abstract
Syntax Notation One (ASN.1) (Provisionally retained edition).
- ISO/IEC 8825:1990 Information technologyOpen Systems InterconnectionSpecification of Basic
Encoding Rules for Abstract Syntax Notation One (ASN.1) (Provisionally retained edition).







##  3.定义
1. **authenticator** 认证者 LAN中协助另一端完成认证的实体(编者注：普遍意义上的网络设备)
2. **authentication  server** 对authenticator提供认证服务的实体。根据supplicant提供的凭据决定supplicant是否能通过认证与授权(可以与authenticator为同一设备)
3. **network  access  port** 接入LAN的入口。可以是物理端口(Port)也可以是逻辑端口，如802.11无线连接
4. **port  access  entity  (PAE)** 与Port关联的协议，可以是authenticator侧的也可以是supplicant侧的，也可以是双方都具备的
5. **supplicant** 接入LAN的被authenticator认证的实体(编者注：普遍意义上的终端设备，别名还有peer )
6. **system** 接入LAN的具有一个或者多个端口的实体，如无线终端、服务器、MAC桥、路由器
##  4.Acronyms and abbreviations
一些简称
- EAP    extensible authentication protocol
- EAPOL    EAP over LANs
- PAE   port access entity
- Port    network access port
- RADIUS    remote authentication dial in user service
##  5.Conformance(标准顺从)
### 5.1 静态顺从要求
设备声明顺从IEEE-802.1X-2001应对其所有的端口支持以下特性
1. 支持通过uncontrolled port 操作PAE,包括Supplicant PAE或者Authenticator PAE 或者两者兼备
2. ==支持表格9.6.1列出的==系统配置功能
3. Authenticator PAE需要支持以下特性
    - 3.1 ==支持表格9.4.1列出的功能==
    - 3.2 ==支持获取与维护表格9.4.2列出的统计信息==
    - 3.3 ==支持controlled Port 的几种设置Force Unauthorized、Auto、Force Authorized以及对应的表格6.3定义的行为==
    - 3.4 ==支持通过管理将AuthControlledPortControl设置为Force Unauthorized、Auto、Force Authorized 见表6.3==
    - 3.5 ==controlled port 支持AdminControlledDirections以及OperControlledDirections相关的参数，见表6.4==
    - 3.6 支持对supplicant进行重认证，实现重认证周期状态机，支持设置重认证周期以及重认证开关
4. Supplicant PAE支持以下特性
    - 4.1 ==支持表9.5.1定义的操作==
    - 4.2 ==支持获取与维护表9.5.2定义的统计信息==
### 5.2 可选项
以下特性为可选支持项
1. 支持通过操作除了PAE之外的协议
2. Authenticator PAE支持以下操作
    - 2.1 ==支持维护与获取表9.4.3定义的诊断信息==
    - 2.2 ==支持维护与获取表9.4.4定义的会话统计信息==
    - 2.3 ==支持通过AdminControlledDirections以及OperControlledDirections参数控制controlled port，并且可以通过表6.4说明的方法管理AdminControlledDirections参数==
    - 2.4 ==Support the ability to transmit key information to the Supplicant following successful
authentication, and support the ability to modify the KeyTransmissionEnabled parameter by
management action (8.4.9, 8.5.5, and 9.4.1)==
3. Supplicant PAE支持以下操作
    - ==Support the ability to transmit key information to the Authenticator following successful
authentication, and support the ability to modify the KeyTransmissionEnabled parameter by
management action (8.4.9, 8.5.6, and 9.4.1)==
## 6.Principles of operation
## 7.EAPOL
## 8.Port Access Control
## 9.Management of port access control
## 10.Management protocol

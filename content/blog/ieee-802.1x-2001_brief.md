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
### 6.1 System,Ports, and system roles
接入LAN的设备对应此标准的System,接入LAN的点对应此标准的Ports。
为了完成访问控制，分为3种角色，Authenticator Port、Supplicant Port、Authentication  server。
1. Authenticator Port角色 需要认证通过之后才能允许提供服务
2. Supplicant Port角色 需要使用Authenticator提供服务
3. Authentication  server 根据Supplicant以及Authenticator提供的信息判断是否认证通过

### 6.2 PAE
1. Supplicant PAE：在认证过程中为Supplicant Port角色，响应Authenticator的认证请求
2. Authenticator PAE:在认证过程中为Authenticator Port角色，与Supplicant通讯并将Supplicant提供的认证数据提交给Authentication Server，以及维护Supplicant的认证状态


## 6.3 Controlled and uncontrolled access
为了完成端口级别的访问控制，在实体接入点上虚拟出2个不同的虚拟接入点，一个接入点在任何认证状态下都允许数据包通过称为uncontrolled Port,另一个接入点只有在认证通过的前提下才能放通数据包称为controlled  Port。uncontrolled port能收到实体接入点收到的所有数据帧，controlled port则只能在认证通过的情况下收到。

图示如下：

![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f6-1.png?raw=true)

下方为LAN，上方为Authenticator System通常为交换机等</br>

下图展示在端口在不同认证状态下的情况(假定OperControlledDirections设置为both),
AuthControlledPortStatus是controlled port的认证状态，可能的值为unauthorized以及authorized
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f6-2.png?raw=true)

AuthControlledPortControl参数：取值为ForceUnauthorized、ForceAuthorized、Auto，当此参数为ForceUnauthorized时Authenticator PAE状态机将controlled port设置成unauthorized状态,当此参数为ForceAuthorized时Authenticator PAE状态机将controlled port设置成authorized,当此参数为Auto时Authenticator PAE状态机根据具体的认证状态设置。

SystemAuthControl参数：认证的总开关,当为Enable时端口的认证状态根据AuthControlledPortControl参数的值决定，当为Diabled时端口的状态与AuthControlledPortControl设置为ForceAuthorized效果一样。

访问LAN受到MAC状态（包括管理状态以及操作状态)以及AuthControlledPortStatus的制约，如果MAC状态不正常则没有任何数据包可以通过包括controlled port以及uncontrolled port。当MAC状态为Disabled时，端口的状态也会变成unauthorized。如下图:</br>
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f6-3.png?raw=true)

**Authenticator PAE与untrolled port的结合**</br>
Authenticator PAE可以使用controlled port或者uncontrolled port完成认证，使用controlled port需要额外的端口或者网卡,使用uncontrolled port是不错的选择，如下图：</br>
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f6-4.png?raw=true)

更复杂的结构如下：</br>
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f6-5.png?raw=true)
终端在桥接网络中，网络设备在桥接网络的边缘，Authenticator PAE通过桥接网络与Supplicant PAE使用EAPOL进行交互，Authenticator PAE使用EAP或者EAP封装在其他协议中与Authentication Server进行交互

更更复杂的结构如下：</br>
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f6-6.png?raw=true)

Authenticator System A需要使用 Authenticator System B提供的服务，Authenticator System B需要使用Authenticator System A使用的服务，比如2个网桥，则端口需要同时具备Authenticator PAE与Supplicant PAE角色

### 6.4 单向控制与双向控制
contolled port 在unauthorized状态下会阻断哪些方向的数据包受到AdminControlledDirections以及OperationalControlledDirections的控制，这两个参数的值为both 或者in ，both 代表发送和接收都受到控制，in代表接收受到控制。声明满足此标准的设备需要支持针对每个端口设置AdminControlledDirections为both，支持针对单个端口设置AdminControlledDirections参数为in是可选项。OperationalControlledDirections由Controlled Directions状态机维护。</br>
**Question**: Why we need this?</br>
**Answer**: Wake-on-lan等功能需要网络设备给终端发包，但是不需要终端回包等场景

### 6.5 802.1X与802.3AD
802.1X应用在物理端口上，处于Unauthorized状态的端口不可加入聚合端口。加入聚合端口的物理端口在变成Unauthorized状态之前应撤销聚合端口


## 7.EAPOL
本部分包含EAP在LAN环境(包括802.3以太网以及环令牌网以及FDDI)下的封装以及传输。
这里只介绍802.3以太网下的EAPOL结构。

### 7.1 EAPOL以太网帧结构
包结构如下图：</br>
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/eapol_packet_f1.png?raw=true)


            


字段名称 | 字段说明|
---------|---------|
PAE以太网类型|0x888E|
协议版本|802.1X-2001为0x01</br>802.1X-2004为0x02</br>802.1X-2010为0x03</br>|
包类型|0x00 EAP-PACKET</br> 0x01 EAPOL-START</br>0x02 EAPOL-LOGOFF</br>0x03 EAPOL-KEY</br>0x04 EAPOL-Encapsulated-ASF-Alert|


### 7.2 EAPOL与tagging
EAPOL帧不进行VLAN标记，但支持802.1Q优先级标记。

### 7.3 EAPOL帧的校验以及版本号处理
1. 校验规则
    - 1.1 目的MAC地址是01-80-C2-00-00-03或==单播MAC地址==
    - 1.2 PAE以太网帧类型字段是0x888e
    - 1.3 包类型是EAP-Packet, EAPOL-Start, EAPOL-Logoff, or
EAPOL-Key
2. 协议版本校验规则
    - 2.1 向下兼容原则
    - 2.2 包含低版本未定义的包类型的数据包会被忽略
    - 2.3 字段大小以及类型超过低版本定义的字段大小和类型的会被忽略

### 7.4 EAP-KEY BODY格式
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/eapol_packet_f2.png?raw=true)

具体的包字段解析这里暂不展开

### 7.5 EAP-PACKET BODY格式
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/EAP-PACKET-f1.png?raw=true)

#### 7.5.1 Code取值及含义
code的取值与含义如下:</br>
值|含义|
----|---|
1|EAP请求包|
2|EAP应答包|
3|EAP认证成功包|
4|EAP认证失败包|

#### 7.5.2 ID的取值范围及用途
ID的长度是1字节，最大值是256，端口+ID用于标志报文的唯一性，同一次EAP交互中请求与应答共用一个ID

#### 7.5.3 长度
长度计算包含整个BODY，EAPOL工作在数据链路层，包大小受到MTU的限制，在不允许分片的情况下请注意不要超过网络环节中的最小MTU。

#### 7.6 EAPOL的源目MAC地址
1. EAPOL帧在Supplicant以及Authenticator中传输
2. EAP包在Authenticator与Authentication Server之间传输

EAPOL帧的目的MAC地址有以下情况：</br>
1. 知道对端MAC地址的情况目的MAC地址为对端的MAC地址
2. 不知道对端MAC地址的情况目的MAC地址为01-80-C2-00-00-03

EAPOL帧的源MAC地址为本端的MAC地址

## 8.Port Access Control
## 9.Management of port access control
## 10.Management protocol

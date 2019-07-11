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
4. **port  access  entity  (PAE)** 与Port关联的协议。可以支持authenticator认证相关的功能，也可以支持supplicant认证相关的功能，也可以同时支持。
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
1. 支持通过uncontrolled port 完成包括Supplicant PAE或者Authenticator PAE或者集两者与一体的功能
2. 支持9.3章节列出的系统配置功能
3. Authenticator PAE需要支持以下特性
    - 3.1 支持9.1.1章节列出的功能
    - 3.2 支持获取与维护9.1.2章节列出的统计信息
    - 3.3 将AuthControlledPortControl参数分别设置为Force Unauthorized\Auto\Force Authorized三种情况下controlled port的行为与此标准的定义一致
    - 3.4 支持通过管理将AuthControlledPortControl设置为Force Unauthorized、Auto、Force Authorized
    - 3.5  将参数AdminControlledDirections以及OperControlledDirections设置为both的时,controlled port的行为与此标准的定义一致
    - 3.6 实现本标准定义的重认证定时器状态机，并根据状态机的状态对Supplicant进行重认证，并且可以调整reAuthTimer以及reAuthEnabled参数
4. Supplicant PAE支持以下特性
    - 4.1 支持9.2.1章节定义的操作
    - 4.2 支持获取与维护9.2.2章节定义的统计信息
### 5.2 可选项
以下特性为可选支持项
1. 支持通过操作除了PAE之外的协议实体
2. Authenticator PAE支持以下操作
    - 2.1 支持维护与获取9.1.3章节定义的诊断信息
    - 2.2 支持维护与获取9.1.4章节定义的会话统计信息
    - 2.3 将AdminControlledDirections以及OperControlledDirections参数设置为IN时controlled  port的行为与此标准的定义一致，并且支持调整AdminControlledDirections参数为both
    - 2.4 支持在认证成功之后传送密钥，并且支持调整KeyTransmissionEnabled参数
3. Supplicant PAE支持以下操作
    - 支持在认证成功之后传送密钥,并且支持调整KeyTransmissionEnabled参数
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
AuthControlledPortStatus是controlled port的认证状态，取值为unauthorized或者authorized之一
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
### 8.1 PAE相关行为
在802.1X认证过程中，PAE可以是Supplicant的角色或者Authenticator的角色或者二者同时兼备
#### 8.1.1 Authenticator 角色
负责对Supplicant发起认证，根据认证的结果调整controlled port的认证状态。认证过程需要Supplicant PAE以及Authentication Server一起完成。
#### 8.1.2 Supplicant角色
负责向Authenticator PAE发送认证凭证以及响应Authenticator PAE的认证请求。也可以发送EAPOL-Logoff
#### 8.1.3 登出机制
以下原因会导致controlled port的状态变成unauthorized
1.  认证失败
2.  端口被设置成force unauthorized 
3.  MAC不可用(硬件原因或者交换机限定MAC不可用)
4.  Supplicant与Authenticator连接失败
5.  重认证周期到了但是重认证失败
6.  Supplicant不响应Authenticator的认证请求
7.  Supplicant发送EAPOL-Logoff请求

### 8.2 相关的协议
#### 8.2.1 概括
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/802.1X_wired_protocols.png?raw=true)

#### 8.2.2 发起认证
可以由Supplicant发起，也可以由Authenticator发起。在Authenticator端口上启用802.1X，当Authenticator探测到MAC可用,Authenticator发起认证。Supplicant通过发送EAPOL-Start帧尝试发起认证。

##### 8.2.2.1  Authenticator发起认证
未开始认证时，端口处于unauthorized状态。Authenticator向Supplicant发送EAP-Request/Identity包，Supplicant进行回应。Authenticator还可用支持对Supplicant进行周期重认证。
##### 8.2.2.2   Supplicant发起认证
Supplicant发送EAPOL-Start帧，Authenticator PAE收到之后向Supplicant PAE发送EAP-Request/Identity包。

#### 8.2.3 EAPOL-Logoff
当Supplicant希望Authenticator PAE将controlled port设置为unauthorized状态时可用发送EAPOL-Logoff帧给Authenticator PAE。

#### 8.2.4 认证状态的超时
认证状态是否超时定期由重认证时间状态机决定。重认证可以选择开启或者关闭，重认证周期也可以根据实际情况调整。
#### 8.2.5 重传
Authenticator PAE负责和Supplicant之间的EAP-Packet的重传。EAPOL-Start由Supplicant进行重传，EAP-Success以及EAP-Failure不会重传（因为Supplicant不会回应这2种包，Authencticator无法知道什么情况需要重传)，如果EAP-Failure或者EAP-Success丢包会导致Supplicant PAE状态机变成CONNECTING状态。Authenticator以及Authentication Server之间的报文重传由具体使用的其他协议确定。
#### 8.2.6 移植性考虑
我们希望终端在接入需要认证的端口与不需要认证的端口体验尽可能的平滑。当支持认证的终端接入未启用认证的端口，终端发送的EAPOL-Start帧不会得到回应，经过几次的超时终端可以认为是接入了认证的端口。当不支持认证的终端接入启用认证的端口，终端忽略网络设备发来的EAP请求，最终端口在unauthorized状态。

#### 8.2.7 EAP中继
EAPOL-Start以及EAPOL-Logoff只由Supplicant发给Authenticator之间传输，不应被中继。</br>
EAPOL-Key只由Authenticator发送给Supplicant，不应被中继。</br>
EAP-Request/Identity由Authenticator  发给Supplicant，不会出现在Authenticator与Authentication Server之间。</br>
其余类型的由Supplicant发出的EAP包，由Authenticator将其由EAPOL帧转换成RADIUS等协议转发给Authentication Server。</br>
 所有Authentication Server发送给Authenticator的EAP包由Authenticator转换成EAPOL帧发送给Supplicant。


#### 8.2.8 密钥传输
EAPOL支持Supplicant与Authenticator之间在认证完成之后传输全局密钥。KeyTransmissionEnabled参数使能密钥传输，在不支持密钥传输的设备上此参数是FALSE且只读。

### 8.3 EAPOL状态机
1. 端口定时器状态机
2. Authenticator PAE状态机
3. Authenticator密钥传输状态机
4. Supplicant密钥传输状态机
4. 重认证定时器状态机
5. 后端认证状态机
6. Controlled Directions 状态机
7. Supplicant PAE状态机
8. 密钥接收状态机

这些状态机都是端口独立的，这些状态机是针对具体的角色而言的，以下表格列出了状态机适用的端口角色（X代表必须支持，O代表可选支持)</br>
状态机名称|Authenticator|Supplicant|Both|
------|-----|----|---|
端口定时器状态机|X|X|X|
Authenticator PAE状态机|X||X|
Authenticator 密钥传输状态机|O||O|
Supplicant 密钥传输状态机||O|O|
重认证定时器状态机|X||X|
 后端认证状态机|X||X|
 Controlled Directions状态机|X||X|
 Supplicant PAE状态机||X|X|
 密钥接收状态机|X|X|X|
 
 
#### 8.3.1 状态机中用到的计时器以及全局变量
</br>
状态机中的时间时间精度精确到秒。</br>
用到的一些计时器如下：</br>

1. **authWhile** Supplicant PAE用于判断Authenticator响应超时的计时器。
2. **aWhile** 后端认证状态机用于判断Authenticator与Supplicant或者Authentication Server之间的认证报文交互超时计时器
3. **heldWhile** Supplicant 状态机用于静默请求Authenticator的计时器
4. **quietWhile** Authenticator状态机用于静默请求Supplicant的计时器
5. **reAuthWhen** 重认证定时器状态机用于判断是否对Supplicant发起重认证的计时器
6. **startWhen** Supplicant PAE状态机用于判断发送EAPOL-Start的计时器
7. **txWhen** Authenticator PAE状态机用于判断EAPOL PDU发送的定时器


全局变量如下：</br>
1. **authAbort** Authenticator PAE可以将此变量设置成TRUE以便让后端认证状态机停止认证过程。当后端认证状态机停止了认证，此值会被置为FALSE。
2. **authFail** 后端认证状态机发现认证失败则此值设置为TRUE。Authenticator PAE状态机在未发起认证之前将此置为FALSE。
3. **authStart** Authenticator PAE将此置为TRUE以便通知后端认证状态机开始认证。一旦后端认证状态机开始认证，则此值被其置为FALSE。
4. **authTimeout** 后端认证状态机没有收到Supplicant的认证响应则此值被置为TRUE。Authenticator PAE可以将此值置为FALSE。
5. **authSuccess** 后端认证状态机在认证成功时将此值置为TRUE。Authenticator PAE状态机在认证开始之前将此值置为FALSE。
6. **currentId** 值在0~255之间，用于区分认证会话。'
7. **initialize** 外部控制的变量，用于控制EAPOL状态机是否可以离开初始状态。
8. **portControl** 由AuthControlledPortControl以及SystemAuthControl推导而来，有ForceUnauthorized、ForceAuthorized、Auto 这3种。
9. **portEnabled** 外部控制变量，如果端口的MAC可用则此值为TRUE，其他为FALSE。
10. **portStatus** 端口的认证状态,Unauthorized或者Authorized。
11. **reAuthenticate** 重认证定时器状态机根据reAuthWhen计时器超时则将此值置为TRUE，也可用通过管理方式设置为TRUE。Authenticator PAE状态机可将此值置为FALSE。
12. **receivedId** Supplicant收到的EAP请求ID。
13. **suppStatus** Supplicant PAE状态机根据与Authenticator的认证结果设置此值，可能的值为Unauthorized以及Authorized。此值影响Supplicant 密钥传输状态机。

一些标记和规则：</br>
1. UCT无条件的TRUE。
2. 全局状态转变，满足条件的且不限定前一状态的状态转变，优先级大于UCT。
3. 全局状态转变的条件判断在每个状态的出口(即状态的操作全部完成)都会进行判断。


#### 8.3.2 端口定时器状态机
```
dec(x): {if (x != 0) then x = x-1;}
inc(x): {x = x + 1; if (x > 255) then x = 0;}
```
![avatar](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-7.png?raw=true)

**tick**是外部系统变量，每秒将此值设置成TRUE。

#### 8.3.3 Authenticator PAE状态机
Authenticator PAE有以下9种状态：</br>
1. INITIALIZE
2. DISCONNECTED
3. CONNECTING
4. AUTHENTICATING
5. AUTHENTICATED
6. ABORTING
7. HELD
8. FORCE_AUTH
9. FORCE_UNAUTH

![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-8-1.png?raw=true)
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-8-2.png?raw=true)

**变量**：</br>
1. **eapLogoff**收到EAPOL-Logoff帧
2. **eapStart**收到EAPOL-Start帧
3. **portMode** ForceUnauthorized、ForceAuthorized、Auto三种
4. **reAuthCount** 重入CONNECTING的次数，当此变量超过**reAuthMax**时端口变成Unauthorized状态。
5. **rxRespId** 当收到Supplicant的EAP Response/Identity中包含的用户名与当前会话的用户名一致时值为TRUE。

**常量**:</br>
1. **quietPeriod** 用于初始化**quietWhile**，默认值是60秒，取值范围是0~65535
2. **reAuthMax** 允许的最大重认证尝试次数。默认值2。
3. **txPeriod** 用于初始化**txWhen**，默认值30秒，范围是1~65535

++常量的值不会被状态机修改，但是可以被外部修改，如交换机管理命令等。++

**函数**:</br>
1. **txCannedFail(x)** 发送EAP失败消息给Supplicant,EAP ID为x
2. **txCannedSuccess(x)** 发送EAP成功消息给Supplicant
3. **txReqId(x)** 发送EAP请求用户名消息给Supplicant

**说明**：</br>
1. 因为重认证或者EAPOL-Start从AUTHENTICATED状态到CONNECTING状态时端口的认证状态可以是Authorized
2. AUTHENTICATING状态将authStart设置为TRUE，后端认证状态机检测到authStart为TRUE则开始工作。根据后端认证状态机的结果有三种情况，authTimeout、authFail、authSuccess。
3. 

Authenticator PAE状态机维护的一些数据:</br>
变量名|解释|
---|---|
authEntersConnecting|进入CONNECTING状态的次数|
authEapLogoffsWhileConnecting|由于收到EAP-LOGOFF从CONNECTING转到DISCONNECTED的次数|
authEntersAuthenticating|由于收到EAP-Response/Identity从CONNECTING转到AUTHENTICATING的次数|
authAuthSuccessesWhileAuthenticating|AUTHENTICATING转到AUTHENTICATED的次数|
authAuthTimeoutsWhileAuthenticating|由于超时从AUTHENTICATING转到ABORTING的次数|
authAuthFailWhileAuthenticating|因为authFail从AUTHENTICATING转到HELD的次数|
authAuthReauthsWhileAuthenticating|由于重认证触发的从AUTHENTICATING转到ABORTING的次数|
authAuthEapStartsWhileAuthenticating|由于收到EAPOL-Start从AUTHENTICATING转到ABORTING的次数|
authAuthEapLogoffWhileAuthenticating|由于收到EAPOL-Logoff从AUTHENTICATING转到ABORTING的次数|
authAuthReauthsWhileAuthenticated|由于重认证触发的从AUTHENTICATED转到CONNECTING的次数|
authAuthEapStartsWhileAuthenticated|由于收到EAPOL-Start从AUTHENTICATED转到CONNECTING的次数|
authAuthEapLogoffWhileAuthenticated|由于收到EAPOL-Logoff从AUTHENTICATED转到DISCONNECTED的次数|



#### 8.3.4 Authenticator 密钥传输状态机
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-9.png?raw=true)

#### 8.3.5 Supplicant 密钥传输状态机
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-10.png?raw=true)

#### 8.3.6 重认证计时器状态机
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-11.png?raw=true)

#### 8.3.7 后端认证状态机
后端认证状态机有以下状态：</br>
1. REQUEST
2. RESPONSE
3. SUCCESS
4. FAIL
5. TIMEOUT
6. IDLE
7. INITIALIZE

![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-12.png?raw=true)

**变量**:</br>
1. **reqCount** 统计发送给Supplicant且没有回应的EAP请求包数量
2. **rxResp** 收到除了PDU为EAP-Response/Identity之外的EAP包的EAPOL帧，则此值为TRUE
3. **aSuccess** 收到Authentication Server返回的认证成功消息则此值为TRUE
4. **aFail** 收到Authentication Server返回的认证失败消息则此值为TRUE
5. **aReq** 收到Authentication Server发来的EAP请求包则此值为TRUE
6. **idFromServer** 收到来自Authentication Server的最近一个EAP-SUCCESS或者EAP-FAIL或者EAP请求包中的ID

**函数**:</br>
1. **txReq(x)** 发送EAP请求给Supplicant
2. **sendRespToServer()** 将Supplicant的EAP响应发送给Authentication Server
3. **txCannedSuccess(x)** 给Supplicant发送EAP-SUCCESS
4. **txCannedFail(x)** 给Supplicant发送EAP-FAILURE
5. **abortAuth** 后端认证状态机释放资源等动作

后端认证状态机维护的一些数据:</br>
变量名|解释|
---|---|
backendResponses|后端认证状态机发送给Authentication Server的Access-Request包的次数|
backendAccessChallenges|后端认证状态机收到来自Authentication Server的Access-Challenge包的次数|
backendOtherRequestsToSupplicant|统计后端认证状态机发送给Supplicant(除了Identity、Notification、Failure、Success之外)的EAP包的次数|
backendNonNakResponsesFromSupplicant|统计来自Supplicant的非EAP-NAK之外的EAP包的次数|
backendAuthSuccesses|统计从Authentication Server收到的Accept包的次数|
backendAuthFails|统计从Authentication Server收到的Rejcet包的次数|

#### 8.3.8 Controlled Directions状态机
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-13.png?raw=true)

#### 8.3.9 Supplicant PAE状态机
Supplicant PAE状态机有以下几种状态：</br>
1. LOGOFF
2. DISCONNECTD
3. CONNECTING
4. ACQUIRED
5. AUTHENTICATING
6. HELD
7. AUTHENTICATED

![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-14.png?raw=true)

**变量**:</br>
1. **userLogoff** 外部变量，当外部系统认为用户登陆系统时此变量为FALSE，当外部系统认为用户登出时此变量为TRUE。此值的取值差异较大，当设备是无人登陆设备如桥则认为永远是登陆的，当设备是终端PC则由操作系统决定用户是否登陆。
2. **logoffSent** 在LOGOFF状态中是否已经发送EAPOL Logoff包。在LOGOFF中被设置为TRUE以防止一直进入LOGOFF状态导致重复发送EAPOL-LOGOFF。
3. **reqId** 收到Authenticator发送的EAP Request/Identity 包则为TRUE
4. **reqAuth** 收到Authenticator发送的除了EAP Request/Identity之外的EAP-Packet则此变量为TRUE
5. **eapSuccess** 从Authenticator收到EAP-SUCCESS则为TRUE
6. **eapFail** 从Authenticator收到EAP-FAIL则为TRUE
7. **startCount** 统计没有收到回复的EAPOL-START包数量
8. **previousId** 当Supplicant发送EAP请求的响应包则将**receivedId**拷贝到**previousId**，用于防止重复发送回包


**函数**:</br>
1. **txStart** 发送EAPOL-Start给Authenticator
2. **txLogoff** 发送EAPOL-Logoff给Authenticator
3. **txRspId(receivedId,  previousId)** 发送EAP Response/Identity packet给Authenticator 如果receivedId与previousId相同则发送前一次发送的报文
4. **txRspAuth(receivedId,  previousId)** 向Authenticator发送除了EAP Response/Identity之外的EAP响应包,如果receivedId与previousId相同则发送前一次发送的报文    


#### 8.3.10 密钥接收状态机
![](https://github.com/lu18887/dot1x.io-web/blob/master/resources/img/ieee-802.1x-2001-f8-15.png?raw=true)



## 9.Management of port access control
### 9.1 Authenticator PAE配置与管理对象
#### 9.1.1 Authenticator配置对象
- 读取Authenticator配置包括以下：
    - Port  number.
    - Authenticator PAE state
    - Backend  Authentication  state
    - AdminControlledDirections
    - OperControlledDirections
    - AuthControlledPortControl
    - AuthControlledPortStatus
    - quietPeriod
    - txPeriod
    - suppTimeout
    - serverTimeout
    - maxReq
    - reAuthPeriod
    - reAuthEnabled
    - KeyTransmissionEnabled
- 修改Authenticator配置包括以下：
    - Port  number
    - AdminControlledDirections(optional)
    - AuthControlledPortControl (optional)
    - quietPeriod (optional)
    - txPeriod (optional)
    - suppTimeout (optional) 
    - serverTimeout (optional)
    - maxReq (optional).
    - reAuthPeriod (optional)
    - reAuthEnabled (optional)
    - KeyTransmissionEnabled (optional)
- 重认证
    - Port  number将指定的端口触发重认证

#### 9.1.2 Authenticator统计管理对象
- 读取Authenticator统计管理对象
    - Port  number
    - EAPOL frames received.
    - EAPOL frames received.
    - EAPOL frames transmitted
    - EAPOL Start frames received
    - EAPOL Logoff frames received.
    - EAP Resp/Id frames received
    - EAP Response frames received.
    - EAP Req/Id frames transmitted.
    - EAP Req frames transmitted.
    - Invalid EAPOL frames received.
    - EAP length error frames received.
    - Last EAPOL frame version.
    - Last  EAPOL  frame  source. 
#### 9.1.3 Authenticator诊断管理对象
- 读取Authenticator诊断信息
    - Port  number. 
    - authEntersConnecting
    - authEapLogoffsWhileConnecting
    - authEntersAuthenticating
    - authAuthSuccessWhileAuthenticating
    - authAuthTimeoutsWhileAuthenticating
    - authAuthFailWhileAuthenticating
    - authAuthReauthsWhileAuthenticating
    - authAuthEapStartsWhileAuthenticating
    - authAuthEapLogoffWhileAuthenticating
    - authAuthReauthsWhileAuthenticated
    - authAuthEapStartsWhileAuthenticated
    - authAuthEapLogoffWhileAuthenticated
    - backendResponses
    - backendAccessChallenges
    - backendOtherRequestsToSupplicant
    - backendNonNakResponsesFromSupplicant
    - backendAuthSuccesses
    - backendAuthFails
#### 9.1.4 Authenticator会话统计管理对象
- 读取Authenticator会话统计信息
    - Port  number. 
    - Session Octets Received.
    - Session Octets  Transmitted. 
    - Session Frames Received.
    - Session Frames Transmitted. 
    - Session  Identifier. 
    - Session  Authentication  Method.
        - local authentication server
        - remote authentication server
    - Session Time.
    - Session  Terminate Cause.
    - Session User Name
### 9.2 Supplicant PAE配置与管理对象
#### 9.2.1. Supplicant配置
- 读取Supplicant配置
    - Port  number. 
    - Supplicant  PAE  state. 
    - heldPeriod.
    - authPeriod. 
    - startPeriod. 
    - maxStart.
- 修改Supplicant配置
    - heldPeriod (optional).
    - authPeriod (optional).
    - startPeriod (optional).
    - maxStart (optional).
#### 9.2.2. Supplicant统计
- 读取Supplicant统计信息
    - EAPOL frames received. 
    - EAPOL frames transmitted.
    - EAPOL Start frames transmitted.
    - EAPOL Logoff frames transmitted. 
    - EAP Resp/Id frames transmitted.
    - EAP Response frames transmitted.
    - EAP Req/Id frames received.
    - EAP Request frames received.
    - Invalid EAPOL frames received. 
    - EAP length error frames received.
    - Last EAPOL frame version.
    - Last  EAPOL  frame  source. 

### 9.3 系统配置
#### 9.3.1. 读取系统配置
- SystemAuthControl
- 针对每个端口的数据如下：
    - Port number.
    - Protocol version
    - PAE Capabilities
#### 9.3.2. 修改系统配置
- SystemAuthControl
#### 9.3.3. 初始化端口



## 10.Management protocol
### 10.1 SNMP管理

[mib文件](http://oidref.com/1.0.8802.1.1.1)


这里的Port number对应RFC 2863中的IFINDEX
管理对象与MIB节点的对应关系如下：</br>

**本文中列举的管理对象**|**MIB节点**|
---|---|
**9.3系统配置**|**dot1xPaeSystem**|
Port number |dot1xPaePortNumber (table index)|
SystemAuthControl |dot1xPaeSystemAuthControl|
Protocol version |dot1xPaePortProtocolVersion|
PAE capabilities |dot1xPaePortCapabilities|
Initialize Port |dot1xPaePortInitialize|
**9.1.1 Authenticator PAE配置与管理对象**|**dot1xAuthConfigTable**|
Port number |dot1xPaePortNumber (table index)|
Authenticator PAE State| dot1xAuthPaeState|
Backend Authentication State|dot1xAuthBackendAuthState|
AdminControlledDirections |dot1xAuthAdminControlledDirections|
OperControlledDirections |dot1xAuthOperControlledDirections|
AuthControlledPortStatus |dot1xAuthAuthControlledPortStatus|
AuthControlledPortControl |dot1xAuthAuthControlledPortControl|
quietPeriod |dot1xAuthQuietPeriod|
txPeriod |dot1xAuthTxPeriod|
suppTimeout |dot1xAuthSuppTimeout|
serverTimeout |dot1xAuthServerTimeout|
maxReq |dot1xAuthMaxReq|
reAuthPeriod |dot1xAuthReAuthPeriod|
reAuthEnabled |dot1xAuthReAuthEnabled|
KeyTransmissionEnabled |dot1xAuthKeyTxEnabled|
Reauthenticate |dot1xPaePortReauthenticate|
**Authenticator统计管理对象**|**dot1xAuthStatsTable**|
Port number |dot1xPaePortNumber (table index)|
EAPOL frames received |dot1xAuthEapolFramesRx|
EAPOL frames transmitted |dot1xAuthEapolFramesTx|
EAPOL Start frames received |dot1xAuthEapolStartFramesRx|
EAPOL Logoff frames received |dot1xAuthEapolLogoffFramesRx|
EAP Resp/Id frames received |dot1xAuthEapolRespIdFramesRx|
EAP Response frames received |dot1xAuthEapolRespFramesRx|
EAP Req/Id frames transmitted |dot1xAuthEapolReqIdFramesTx|
EAP Request frames transmitted |dot1xAuthEapolReqFramesTx|
Invalid EAPOL frames received |dot1xAuthInvalidEapolFramesRx|
EAP length error frames received |dot1xAuthEapLengthErrorFramesRx|
Last EAPOL frame version |dot1xAuthLastEapolFrameVersion|
Last EAPOL frame source |dot1xAuthLastEapolFrameSource|
**Authenticator诊断管理对象**|**dot1xAuthDiagTable**|
authEntersConnecting |dot1xAuthEntersConnecting|
authEapLogoffsWhileConnecting |dot1xAuthEapLogoffsWhileConnecting|
authEntersAutheniticating |dot1xAuthEntersAuthenticating|
authAuthSuccessWhileAuthenticating |dot1xAuthAuthSuccessWhileAuthenticating|
authAuthTimeoutsWhileAuthenticating |dot1xAuthAuthTimeoutsWhileAuthenticating|
authAuthFailWhileAuthenticating |dot1xAuthAuthFailWhileAuthenticating|
authAuthReauthsWhileAuthenticating |dot1xAuthAuthReauthsWhileAuthenticating|
authAuthEapStartsWhileAuthenticating |dot1xAuthAuthEapStartsWhileAuthenticating|
authAuthLogoffWhileAuthenticating |dot1xAuthAuthEapLogoffWhileAuthenticating|
authAuthReauthsWhileAuthenticated |dot1xAuthAuthReauthsWhileAuthenticated|
authAuthEapStartsWhileAuthenticated |dot1xAuthAuthEapStartsWhileAuthenticated|
authAuthLogoffWhileAuthenticated |dot1xAuthAuthEapLogoffWhileAuthenticated|
backendResponses |dot1xAuthBackendResponses|
backendAccessChallenges |dot1xAuthBackendAccessChallenges|
backendOtherRequestsToSupplicant |dot1xAuthBackendOtherRequestsToSupplicant|
backendNonNakResponsesFromSupplicant |dot1xAuthBackendNonNakResponsesFromSupplicant|
backendAuthSuccesses |dot1xAuthBackendAuthSuccesses|
backendAuthFails |dot1xAuthBackendAuthFails|
**Authenticator会话统计管理对象**|**dot1xAuthSessionStatsTable**|
Port number |dot1xPaePortNumber (table index)|
Session Octets Received |dot1xAuthSessionOctetsRx|
Session Octets Transmitted |dot1xAuthSessionOctetsTx|
Session Frames Received |dot1xAuthSessionFramesRx|
Session Frames Transmitted |dot1xAuthSessionFramesTx|
Session Identifier |dot1xAuthSessionId|
Session Authentication Method |dot1xAuthSessionAuthenticMethod|
Session Time |dot1xAuthSessionTime|
Session Terminate Cause |dot1xAuthSessionTerminateCause|
Session User Name |dot1xAuthSessionUserName|
**Supplicant配置**|**dot1xSuppConfigTable**|
Port number |dot1xPaePortNumber (table index)|
Supplicant PAE State |dot1xSuppPaeState|
heldPeriod |dot1xSuppHeldPeriod|
authPeriod |dot1xSuppAuthPeriod|
startPeriod |dot1xSuppStartPeriod|
maxStart |dot1xSuppMaxStart|
**Supplicant统计**|**dot1xSuppStatsTable**|
Port number |dot1xPaePortNumber (table index)|
EAPOL frames received |dot1xSuppEapolFramesRx|
EAPOL frames transmitted |dot1xSuppEapolFramesTx|
EAPOL Start frames transmitted |dot1xSuppEapolStartFramesTx|
EAPOL Logoff frames transmitted |dot1xSuppEapolLogoffFramesTx|
EAP Resp/Id frames transmitted |dot1xSuppEapolRespIdFramesTx|
EAP Response frames transmitted |dot1xSuppEapolRespFramesTx|
EAP Req/Id frames received |dot1xSuppEapolReqIdFramesRx|
EAP Request frames received |dot1xSuppEapolReqFramesRx|
Invalid EAPOL frames received |dot1xSuppInvalidEapolFramesRx|
EAP length error frames received |dot1xSuppEapLengthErrorFramesRx|
Last EAPOL frame version |dot1xSuppLastEapolFrameVersion|
Last EAPOL frame source |dot1xSuppLastEapolFrameSource|

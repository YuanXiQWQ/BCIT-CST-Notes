# Data Communications 数据通信
-  **Communication 通信**：信息交换
- **Telecommunication 电信**：远距离通信（电话、电报、电视）
- **Data 数据**：原始事实或信息，需要收发双方约定好形式，如文本、数字、图像、音频、视频
- **Data Communications 数据通信**：两个设备之间的数据交换，通过某种介质（如铜线）
- **Data Communication System 数据通信系统**：由硬件和软件组成的网络，支持不同设备通过各种介质交换数据
---
# 数据通信类型
- **Digital Communication 数字通信**：通过通信线路以数字信号（二进制位）传输信息的过程
	- 如数据、文本、音频、视频等
	- 所有数字通信信息都以比特的形式表示和运输
- **Analog Communication 模拟通信**：通过使用幅度、频率或相位不断变化的连续信号来传输信息，以此来表示数据
---
# 数据通信的有效性衡量
数据通信效果取决于四个指标
- **Delivery 传送**：能否送达正确的目标
- **Accuracy 准确性**：数据是否无误
- **Timeliness 时效性**：是否及时传输
- **Jitter 抖动**：音视频传输中延迟是否均匀
---
# 数据通信系统的五大组成部分
![[Pasted image 20250911234614.png]]
1. **Message 信息**：要传递的信息
2. **Sender 发送方**：发出数据的设备（电脑、电视、手机）
3. **Receiver 接收方**：接收数据的设备（电脑、电视、手机）
4. **Transmission Medium 传输介质**：消息传递的路径（电缆、光纤、空气）
5. **Protocol 协议**：通信双方约定的规则
---
# Data flow 数据流模式
1. **Simplex 单向通信**：只能单方向发送（如键盘 → 电脑）
2. **Half-duplex 双向交替**：双方均可发送，但必须轮流（如对讲机）
3. **Full-duplex 双向同时**：双方可同时通信（如电话）
---
# Network 网络
## 定义
由节点（Node）和边（Edge）组成的系统
- **Node 节点**：网络中的个体实体或点，如火车站
- **Edge 边**：链接方式，表示网络中节点之间关系或相互作用的方式，如铁轨
### 计算机网络
一组能进行通信的设备之间的相互连接
- 设备（节点）
	- 主机（终端设备）：大型计算机、台式机、笔记本电脑、工作站、手机等
	- 连接、联网、通信设备：路由器、交换机、调制解调器🐱等
- 设备之间的连接（边）
	- 有限或无线传输介质，例如电缆或空气
## 评判标准
- **Performance 性能**：Throughput 吞吐量、Delay 延迟
- **Reliability 可靠性**：Accuracy of delivery 准确性、Failure rate 故障率、Recovery Time 恢复能力、Robustness 耐操性
- **Security 安全性**：数据防护、防止未授权访问，并指定恢复政策
## 连接类型
- **Point-to-Point (P2P)  点对点**：两个设备之间的专用连接
	- 该链路的 Capacity 容量（带宽）专门用于两台设备之间的数据传输
- **Multipoint 多点**：多于两台设备共用一条链路
	- 该链路的容量是共享的。由于只有一条链路，因此有两种共享方式
		- **Spatially shared 空间共享**：多台设备可以同时使用该连接，但需要物理分开信道，或互相不会干扰
		- **Timeshared 时间共享**：用户必须轮流使用该线路以确保不会干扰
## Physical Topology 物理拓扑结构
### 定义
Topology 拓扑是用几何图形的方式表示网络中节点和链路之间的连接关系。它描述的不是地理位置，而是连接关系和结构
### 基本网络拓扑
#### Mesh 全连接拓扑
- 每个设备都与其它所有设备有一条专用链路
- 优点：高可靠性，容易隔离故障
- 缺点：布线复杂，成本高
- 需要的链路数：
$$
C^{n}_{2} = \frac{n(n-1)}{2}
$$
- 常见应用：较少见，常用于高可靠专网
#### Star 星形拓扑
- 每个设备只与一个中心节点（交换机/集线器等）相连
- 优点：布线简单，容易扩展，问题易定位
- 缺点：中心节点故障会导致全网瘫痪
- 常见应用：家庭/企业局域网
#### Bus 总线拓扑
- 所有设备共享一根主干线
- 优点：布线简单，安装容易
- 缺点：扩展性差，故障排查困难
- 常见应用：早期以太网
#### Ring 环形拓扑
- 每个设备只连接相邻的两个设备，形成一个闭环
- 优点：布线比全连接少，故障易隔离
- 缺点：单点故障可能导致全环中断
## 网络类型
### LAN （Local Area Network） 局域网
- 通常为私有，用于连接某一区域内的部分设备
- 局域网中的每个主机都有一个 Unique Identifier 唯一标识符
- 如果通过无线方式连接，则成为 WLAN（Wireless LAN）
- 现在的 LAN 每台主机通过交换机连接
### WAN（Wide Area Network）广域网
- 具有更大的地理范围，涵盖一个城镇、省、国、甚至全世界
- 将网络设备（如交换机、路由器和调制解调器🐱）相互连接
- 由通信公司创建并运营，然后由使用该服务的机构租赁
- 包含两种类型：
	- P2P WAN 点对点广域网：只连接两个设备，如两个城市间的专线
	- Switched WAN 交换式广域网：多个设备共享互联，能灵活切换连接对象，如互联网的骨干网
	- 如今的全球互联网骨干网就是基于交换式广域网搭建的
# Internet 互联网
### Internetwork 互联网络
当两个或更多网络相互连接，就興城路一个互联网络
- 如公司不同分支机构的局域网互联
### Internet 互联网
全球最大的互联网络，由成千上万个网络互联组成
#### 本质
网络的网络，各个小网络（LAN/WAN）互联后形成 Internet
#### 结构
- End systems 终端系统：运行应用程序的设备
- Access network 接入网：终端到第一个路由器之间的连接
- Core network 核心网：由路由器、交换机和调制解调器🐱组成，负责长距离传输
#### Internet Service Providers (ISPs) 互联网服务提供商
互联网的层次结构：
- 国际 ISP：跨国通信骨干网
- 国家、区域 ISP：连接一个国家或区域
- 本地 ISP：连接家庭和企业用户
### Accessing the Internet 接入互联网
常见接入方式：
- Dial-up 拨号：早期方式，速度慢
	- Digital Subscriber Line (DSL) 数字用户线路：电话线同时传输语音和数据
	- Cable：有线电视网络
- Wireless：Wi-Fi、移动网络
- Direct Connection 专线：企业/数据中心使用
### Internet Standards 互联网标准
由 Internet Engineering Task Force (IETF) 互联网工程任务组指定和发布
- 保证不同厂商的设备、系统能互操作
### Request for Comments (RFC)
- 定义互联网协议、标准和技术的文档
- IETF 是制定和发布 RFC 的组织
---
# Protocol 协议
协议定义了通信的**内容**、**方式**和**时机**
包括：
- 消息格式和顺序
- 通信双方在发送、接受时的动作
## Protocol Layering 协议分层
将复杂的通信任务分为多个独立且简单的任务，每一层的服务指的是该层向上一层提供的服务
- 例如应用层（HTTP）要传网页，会利用传输层（TCP）来保证可靠运输，而传输层又会利用网络层（IP）来找到目标地址
### Principles 分层的原则
- **First Principle 第一原则**：为了实现 **Bidirectional Communication 双向通信**，**每一层**必须都能够完成相反的任务
- **Second Principle 第二原则**：两个站点的每一层下对应的内容都是 **Identical 相同的**
### 分层的优点
- Separating the services from the implementation 分离服务实现，简化复杂任务
- Simpler and less expensive intermediate systems 更简单和更低成本的中间系统
- Modularity 模块化：方便维护、更新，修改一层不需要改变整个系统（黑箱，其它实现无需关心如何修改）
### 计算机网络操作模型
两种主要模型来描述计算机的工作：
- TCP/IP Protocol Suite TCP/IP 协议套件（或 TCP/IP 协议栈）：互联网用的模型，包括五层（按照数据发出顺序，接收时反过来）：
![[Pasted image 20250912085020.png]]
1. **Physical 物理层**
	- 应用 - 网卡
	- 通过数据链路从一个节点向下一个节点传输比特
	- 只关心比特如何运输，不关心内容
	- 如，浏览器发送请求，最后一定要变成“电压/光/电磁波”的模拟/数字信号才能传出去
2. **Data Link 数据链路层**
	- 主机 - 路由器/交换机
	- 在相邻设备之间可靠地传输数据
	- Protocol Data Unit (PDU) 传输单位：Frame 帧，是在协议栈的不同层传递的数据单元
	- 如，Ethernet 以太网、Wi-Fi
3. **Network 网络层**
	- 主机 - 主机
	- 决定数据从源主机到目标主机如何走
	- PDU 传输单位：数据报 Datagram/Packet
	- 如：IP、ICMP、ARP、DHCP
4. **Transport 运输层**
	- 系统 - 应用
	- 保证不同应用间能正确通信
	- PDU 传输单位：Segment 段（TCP）、Datagram 数据报（UDP）
	- TCP 提供可靠运输，UDP 提供快速运输
5. **Application 应用层**
	- 应用 - 用户
	- 面向用户的层
	- PDU 传输单位：Message 消息
	- 如：HTTP/HTTPS（网页）、FTP（文件传输）、SMTP/IMAP（邮件）、DNS（域名解析）
- OSI Model OSI 模型
	- 国际标准化组织 ISO 提出的理论模型
		- 包括七层，比 TCP/IP 更细致：应用层、表示层、会话层、传输层、网络层、数据链路层、物理层
		- 与 TCP/IP 相比，在运输层和应用层之间分了 Session Layer 会话层和 Presentation Layer 表示层
### Encapsulation and Decapsulation 封装与解封装
![[Pasted image 20250912085243.png]]
封装：上层数据加上本层的 Header 后交给下层
解封：反过来
### 传输示例
![[Pasted image 20250912085343.png]]
### 层级地址
在 TCP/IP 协议中，网络使用四层地址
- **应用层：Names**（URL、邮件地址）
- **传输层：Port numbers 端口号**：标识一个主机上的进程
- **网络层：Logical addresses 逻辑地址**：一个 IP 地址在互联网上唯一地标识主机
- **链路层：Link-layer addresses 链路地址**：在 LAN/WAN网络中标识了指定的主机/路由器
物理层和链路层一般由 Network Inerface Card (NIC) 网卡实现
- 只处理了设备与设备之间的直接通信
主机（终端）实现了 TCP/IP 的全部五层



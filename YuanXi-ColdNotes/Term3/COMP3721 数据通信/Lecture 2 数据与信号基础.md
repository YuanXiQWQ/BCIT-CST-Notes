# 主要内容
- Data 数据和 Signal 信号的概念及其类型
- Characteristics of periodic analog signals 周期性模拟信号的特征
- Characteristcs of digital signals 数字信号的特征
# 基本概念
## 数据—信号—物理层的关系
- **Physical Layer 物理层**：以 Electiomagnetic signals 电磁信号的形式在传输介质中传输数据
- **Data 数据**：必须转换为**Signal 信号**以便运输
- 应用层、传输层、网络层和数据链路层之间的 **Communication 通信**是 **Logical 逻辑性的**
## Analog Data 模拟数据和 Digital Data 数字数据
- **Analog Data**：Continuous 连续数值（例如声音强弱的连续变化）
- **Digital Data**：Discrete 离散数值（例如二进制位 0、1，不存在中间值 0.5）
## Analog Signal 模拟信号和 Digital Signal 数字信号
![[Pasted image 20250919052827.png]]
- **Analog Signal**：幅度随时间**连续变化**
![[Pasted image 20250919052921.png]]
- **Digital Signal**：幅度只取**有限**个电平（常见：高/低电平）
> 上层可以是数字数据，但在物理层既可以用数字信号（如以太网方波），也可以调制成模拟信号（如传统电话线的调制解调）
## Periodic Signal 周期信号与 Nonperiodic Signal 非周期信号
数字信号和模拟信号都可以被分为周期信号与非周期信号
![[Pasted image 20250919063246.png]]
- **Periodic 周期信号**：
	- **Cycle 循环**：一个完整模式的完成
	- **Period 周期**：完成一个循环需要的时间
		- 表示：$T$
		- 单位：秒
	- 一个 Sine Wave 正弦波信号，即 Simple 简单的周期性模拟信号无法分解为更简单的信号
		- Composite 复合信号可分解为多条正弦信号
- **Nonperiodic (Aperiodic) 非周期信号**：即不重复的信号
- **在数据通信中，通常使用周期的模拟信号，和非周期的数字信号**
# Sine Wave 正弦波
- 是周期性模拟信号的最基本形式（Fundamental form）
- 三要素：
	- **Peak amplitude 峰值幅度**
	- **Frequency 频率**
	- **Phase shift 相位**
## Peak amplitude 峰值幅度
![[Pasted image 20250919065404.png]]
- 波形从 $x$ 轴到波峰的距离
- 信号最高强度的绝对值，与信号能量成正比
- **表示**：$A$
- **单位**：通常是**伏特**（$V$）、安培（$A$）或分贝（$dB$）
## Frequency 频率
![[Pasted image 20250919065645.png]]
- $1$ 秒内完成的周期数（即信号重复的频率）
- **表示**：$f$
- **单位**：$Hz = cycle \space per \space second$
$$
T = \frac{1}{f}, f = \frac{1}{T}
$$
- 频率具体指随时间变化的速率，即：
	- 短时间发生改变：频率较高
	- 长时间内的变化：频率较低
	- 完全没有变化：频率为零
	- 瞬间发生变化（持续时间 $T=0 s$）：频率为正无穷
- 进位/退位后的单位转换：通常情况下，$Hz$ 实际总是与 $ms$ 对应，以此类推，因此不能直接用 $T=\frac{1}{f}$ 计算，因为那样得出的是对应 $s$

| **频率单位** | **对应周期单位** |
| :------: | :--------: |
|   $Hz$   |    $ms$    |
|  $kHz$   |  $\mu s$   |
|  $MHz$   |    $ns$    |
|  $GHz$   |    $ps$    |
|  $THz$   |    $fs$    |
如果不想每次都从 $s$ 再换算到 $ms$，可以直接对应 $T = \frac{1000}{f}$
$$\frac{1000}{频率}=周期$$
例

|   **频率**   | **换算（$\frac{1000}{频率}=周期$）** |   **周期**   |
| :--------: | :--------------------------: | :--------: |
| $1000 MHz$ |    $\frac{1000}{1000}=1$     |   $1 ns$   |
| $200 MHz$  |     $\frac{1000}{200}=5$     |   $5 ns$   |
|  $40 kHz$  |     $\frac{1000}{40}=25$     | $25 \mu s$ |
|  $80 Hz$   |    $\frac{1000}{80}=12.5$    | $12.5 ms$  |
| $250 kHz$  |     $\frac{1000}{250}=4$     | $4 \mu s$  |
|   $2 Hz$   |     $\frac{1000}{2}=500$     |  $500 ms$  |
## Phase shift 相位
![[Pasted image 20250919074630.png]]
- 波形相对于 $t = 0$ 的位置
-  **表示**：$\phi$
- **单位**：度（$\degree$）或弧度（rad）
	- $360\degree = 2\pi$
## 正弦波的表示
使用
-  $s(t)$：Instantaneous amplitude 瞬时振幅
- $A$：Peak amplitude 峰值振幅
-  $f$：Frequency 频率
-  $t$ ：Time 时间
- $T$：Period 周期
- $\phi$：Phase shift 相位
- $\omega$：Angular frequency 角频率，$\omega = 2 \pi f$
时，正弦波信号满足：
$$
s(t) = A sin(\omega t \pm \phi) = A \sin( \frac{2\pi}{T} t \pm \phi)
$$
# Wavelength 波长
![[Pasted image 20250919083450.png]]
- 一个简单信号在周期 $T = 1$ 时传播的波长 $\lambda = 1$
- 通常用于描述光在光纤中的传输情况
- **表示**：$\lambda$
- **单位**：通常是 $\mu s$
## 频率、波长分别与介质的关系
- 频率：信号每秒震荡的次数
	- 信号的频率是由信号源决定的，与介质无关
- 波长：信号在一个完整周期传播的距离
	- 取决于频率 $f$ 和传播速度 $c$
	- $c$ 取决于介质，真空中约为 $3 \times 10^{8} m/s$
$$
\lambda = \frac{c}{f} = c \times T
$$
## Time Domain 时域和 Frequency Domain 频域
- 时域图：信号幅度—时间
	- 除非与另一条波形图对比，否则相位不会明确表示
- 频域图：信号幅度—频率
	- 优点
		- 可以立即看出频率和峰值振幅的数值
			- 对于正弦波，仅由一个波峰表示
		- 处理多个正弦波时更紧凑直观
- 三个时域图的正弦波和它们对应的频域图
![[Pasted image 20250919085933.png]]
# Composite Signals 复合信号
单一的正弦波将无法传递任何信息，只会持续不断地传播同样的内容
- 因此传输数据需要使用复合信号
- 复合信号是由多个简单的正弦波组成的信号
## Fourier analysis 傅里叶分析
- 任何复合信号都是由**不同频率**、**峰值幅度**和**相位**的简单正弦波组合而成的
- 傅里叶分析是一种将时域信号和频域信号相互转换的工具
## Fourier Seroes 傅里叶级数
- 每一个复合**周期**信号都可以用一系列 sine 正弦和 cosine 余弦函数表示
- Harmonics 谐波：这些正弦/余弦分量的频率都是 Fundamental frequency 基频 $f$ 的整数倍，称为谐波
- 傅里叶级数可以将任何周期信号分解成谐波分量
$$
s(t)=A_{0}​ + \sum^{\infty}_{n = 1}{A_{n} \sin(2 \pi n f t)} + \sum^{\infty}_{n = 1}{B_{n} \cos(2 \pi n f t)}
$$
其中
$$
A_0 = \frac{1}{T} \int_0^T s(t), dt
$$
$$
A_n = \frac{2}{T} \int_0^T s(t) \cos(2\pi n f t), dt
$$
$$
B_n = \frac{2}{T} \int_0^T s(t) \sin(2\pi n f t), dt
$$
![[Pasted image 20250919092755.png]]
- 对周期复合信号做分解，得到的是一串离散的频率分量
## 常见周期波形的傅里叶级数关系
- **Square Signal 方波**
![[Pasted image 20250919092935.png]]
- **Sawtooth Signal 锯齿波**
![[Pasted image 20250919093035.png]]
## Fourier Transform 傅里叶变换
傅里叶变换能够将**非周期性**的时域信号转换为频域信号。
**Inverse Fourier Transform 反傅里叶变换** 能从频域还原回时域信号
## 复合信号的 Bandwidth 带宽
![[Pasted image 20250919093942.png]]
复合信号最高频率与最低频率的差值
$$
B = f_{h} - f_{l}
$$
# 数字信号
- 大多数数字信号都是非周期性的，因此用频率和周期作为数字信号的特征描述并不恰当的，而是使用
	- **Bit rate 比特率**
	- **Bit length 比特长度**
	- **Bit Duration 比特时长**
## Bit rate 比特率
- 每秒传输的比特数（$bps$）
## Bit length 比特长度
- 与波长的概念类似，为一个比特在传输介质中占据的长度
- $比特长度 = 介质传播速度 \times 比特时间$
## Bit Duration 比特时长
- $比特时长 = \frac{1}{比特率}$
## Level 电平
- 数字信号在某一时刻所能具有的特定状态或数值
- 编码 n 个电平的数字信号需要的比特数为
$$
bits = \log_{2}{n} \space levels
$$
## 数字信号作为复合模拟信号
- 无论周期还是非周期的数字信号，都是复合模拟信号，可以用傅里叶分析分解
### 周期性数字信号
![[Pasted image 20250919095908.png]]
- 该信号的频域图有无限的带宽和离散的频率
### 非周期性数字信号
![[Pasted image 20250919100021.png]]
- 该信号的频域图有无限的带宽和连续的频率
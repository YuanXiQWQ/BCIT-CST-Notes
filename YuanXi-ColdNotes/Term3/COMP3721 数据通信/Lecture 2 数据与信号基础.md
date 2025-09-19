# 主要内容
- Data 数据和 Signal 信号的概念及其类型
- Characteristics of periodic analog signals 周期性模拟信号的特征
- Characteristcs of digital signals 数字信号的特征
## 数据—信号—物理层的关系
- **Physical Layer 物理层**：以 Electiomagnetic signals 电磁信号的形式在传输介质中传输数据
- **Data 数据**：必须转换为**Signal 信号**以便运输
- 应用层、传输层、网络层和数据链路层之间的 **Communication 通信**是 **Logical 逻辑性的**

---
# 数据与信号
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
	- Cycle 循环：一个完整模式的完成
	- Period 周期（$T$）：完成一个循环需要的时间
		- 单位：秒
	- 一个 Sine Wave 正弦波信号，即 Simple 简单的周期性模拟信号无法分解为更简单的信号
		- Composite 复合信号可分解为多条正弦信号
- **Nonperiodic (Aperiodic) 非周期信号**：即不重复的信号
- **在数据通信中，通常使用周期的模拟信号，和非周期的数字信号**
## Sine Wave 正弦波
- 是周期性模拟信号的最基本形式（Fundamental form）
- 三要素：
	- **Peak amplitude 峰值幅度**
	- **Frequency 频率**
	- **Phase shift 相位**
### Peak amplitude 峰值幅度
![[Pasted image 20250919065404.png]]
- 波形从 $x$ 轴到波峰的距离
- 信号最高强度的绝对值，与信号能量成正比
- **表示**：$A$
- **单位**：通常是**伏特**（$V$）、安培（$A$）或分贝（$dB$）
### Frequency 频率
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
### Phase shift 相位
![[Pasted image 20250919074630.png]]
- 波形相对于 $t = 0$ 的位置
-  **表示**：$\phi$
- **单位**：度（$\degree$）或弧度（rad）
	- $360\degree = 2\pi$
### 正弦波的表示
根据上述三要素，正弦波可以被表示为
- 标准式
$$
s(t) = A sin(2 \pi ft) = A \sin( \frac{2\pi}{T} t)
$$
- 含相位
$$
s(t) = A sin(\omega t \pm \phi) \text{，} \omega = 2 \pi f
$$
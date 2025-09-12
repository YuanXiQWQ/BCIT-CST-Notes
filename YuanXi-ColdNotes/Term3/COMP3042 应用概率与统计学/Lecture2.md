# Statistics and Parameters（统计数据和参数）
对于变量 X
## Parameters 参数
### 表示： $n$
- 变量的样本数据
- 例：每科选取五个人后的数据
## Statistics 统计数据
### 表示：$N$
- 变量的总值
- 例：BCIT 总人数

---
# Measure of Proportion （比例的度量）
描述某部分在整体中占比多少
## 对于样本的度量
### 表示：$\hat{p}$
$$
\hat{p} = \frac{X}{n}
$$
## 对于总体的度量
### 表示：$p$
$$
p = \frac{X}{N}
$$
---
# Measures of Centre （中心位置的度量）
## Arithmetic Mean （算数平均数）
### Sample
### 表示：$\bar{X}$
$$
\bar{X} = \frac{\sum{X}}{n}
$$
### Population
#### 表示：$\mu$
$$
\mu = \frac{\sum{X}}{N}
$$
## Mean of Grouped Data （分组数据的均值）
要加权
$$
\bar{X} = \frac{\sum{(f_{i} X_{i})}}{\sum{f_{i}}}
$$
## Median （中位数）
### 表示：$\tilde{X} \text{或} Q_{2}$
$$
\text{对于} n \text{组数据，中位数是位于} \frac{n + 1}{2} \text{的那个值；如果指向两个值之间，则取这两个值的均值}
$$
---
# Measures if Position （位置的度量）
## Quartiles 分位数
## 表示：
- 第一四分位数：$Q_{1}$
- 第二四分位数（中位数）：$Q_{2}$
- 第三四分位数：$Q_{3}$
$$
Q_{1} = \text{位于} (n + 1) \times 0.25 \text{的值，如果位于两个值之间，则取均值或左值} \times \text{0.75} + \text{右值} \times 0.25 \text{，本课取均值}
$$
其它 Q 类似
## Percentiles 百分位数
### 表示：$P_{k}$    
计算方式与分位数相同
## Box and Whisker Plot （箱线图）
用来可视化五数总结
- 最小值 （$Q_{0}$）
- $Q_{1}$
- $Q_{2}$
- $Q_{3}$
- 最大值（$Q_{4}$）
## 表示：
![[Pasted image 20250909100850.png]]
- Box：覆盖 $Q_{1}$ 至 $Q_{3}$
- 中位数：在 $Q_{2}$ 画竖线
- 从 Box 延伸虚线，用 Whiskers（须）画出最小值和最大值
## Outliers 离群值
- 有可能是数据错误
- 同时也可能是极端情况
### Interquartile Range 四分位距法
#### 表示：$IQR$
使用四分位距法判断异常值
1. 计算四分位距
$$
IQR = Q_{3} - Q_{1}
$$
2. 定义 Fence（栅栏）
$$
Lower Fence = Q_{1} - 1.5 \times IQR
$$
$$
Upper Fence = Q_{3} + 1.5 \times IQR
$$
3. 判断异常值：在栅栏外围的点为异常值，用圆点表示
![[Pasted image 20250909101915.png]]
---
# Measures of Variation 离散程度的度量
衡量一个 $X$ 有多分散
## Range 极差
### 表示：$R$
$$
R = Max - Min
$$
- 直观且简单
- 易受离群值影响
## IQR
$$
IQR = Q_{3} - Q_{1}
$$
- 表示中间 $50\%$ 的范围
- 不受极端值影响
- 丢掉了两侧 $50\%$ 的信息
## Standard Deviation 标准差
数据点和均值之间的典型距离
- 标准差小标识数据集中在均值附近
- 标准差大表示数据分布得很分散
### Sample
#### 表示：S
$$
S = \sqrt{\frac{\sum{(X - \bar{X})^2}}{n - 1}}
$$
### Population
#### 表示：$\sigma$
$$
\sigma = \sqrt{\frac{\sum{(X - \mu)^2}}{N}}
$$
## Coefficient of Variation 离散系数
标准差表示数据的绝对离散程度，如果比较不同量纲或不同均值水平的数据，只看标准差不公平
### 表示：$CV$
### Sample
$$
CV = \frac{S}{\bar{X}} \times 100\%
$$
### Population
$$
CV = \frac{\sigma}{\mu} \times 100\%
$$
## Skewness 偏度
- 描述一个分布相对于对称分布（如正态分布）的偏斜成都
- 如果数据完全对称（均值=中位数=众数），$Sk \approx 0$
- 如果不对称，就会出现正负偏移
### 表示：Sk
#### Sample
$$
Sk = \frac{3(\bar{X}-Q——{2})}{s}
$$
#### Population
$$
Sk = \frac{3(\mu-Q_{2})}{\sigma}
$$
### 分布情况：
![[Pasted image 20250911031002.png]]
- Positive Skew 右偏/正偏态
	- $Sk > 1$
	- $\text{均值} > \text{中位数} > \text{众数}$
	- 图像尾巴在右边较长
![[Pasted image 20250911031150.png]]
- Symmetrical Distribution 对称分布
	- $\text{均值} = \text{中位数} = \text{众数}$
	- $Sk \approx 0$
![[Pasted image 20250911031201.png]]
- Negative Skew 左偏/负偏态
	- $Sk < 1$
	- $\text{均值} < \text{中位数} < \text{众数}$
	- 图像尾巴在左边较长
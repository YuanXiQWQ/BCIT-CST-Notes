# Pie Charts 饼图
- 饼图需要两个主要参数：
	- x：一个非负向量，表示每块扇区的大小
	- labels：标签字符串，给每个扇区命名
```R
percents <- c(10, 30, 5, 35, 20)
home.type <- c("On Campus","Parents","Alone","Roommates","Spouse")
pie(percents, home.type)
```
- 另外，图表还有一些额外的通用参数，用来整理图表样式
	- main：表标题
	- col：颜色，与 labels 的顺序是一一对应的
```R
pie(percents, 
	home.type, 
    main = "Living Arrangments of Students",
    col = c("pink", "snow","turquoise", "orange", "skyblue")
)
```
这会创建一个这样的饼图：
![[Pasted image 20250917230454.png]]
- MASS 包的 survey 数据包含 237 名学生的信息
```R
library(MASS)
```
- 使用饼图描述使用左手和使用右手的学生人数比例
```R
hands <- survey$W.Hnd
freq.tab <- table(hands)
pie(freq.tab)
```
- 加上人数到标签
```R
new.labels <- paste(
					names(freq.tab), 
					"\n(", freq.tab, 
					")", 
						sep=""
				)
pie(
	freq.tab,
	new.labels
)
```
- 以下是饼图的可用参数:
- **`x`** ：数值型向量（必填），每个扇区的数值（会自动按比例计算面积）。
- **`labels`** ：字符型向量，给每个扇区的标签。
- **`radius`** ：数值型，圆的半径，默认 `1`。
- **`col`** ：颜色（单个或向量），控制扇区颜色。
- **`main`** ：字符型，主标题。
- **`clockwise`** ：逻辑值，是否顺时针绘制（默认 `FALSE`）。
- **`init.angle`** ：数值型，起始角度（默认 `0`，从 3 点钟方向开始）。
```R
pie(
  *x          = numeric,
  labels      = character,
  radius      = numeric,
  col         = character,
  main        = character,
  clockwise   = logical,
  init.angle  = numeric
)
```
# Bar Graphs 条形图
- **`*height`** ：数值型向量或矩阵（必填）。
    - 向量时：生成单组条形。
    - 矩阵时：按列生成多组条形，可用 `beside` 控制是否并列显示。
- **`width`** ：数值型，条形的宽度，默认 `1`。
- **`space`** ：数值型或向量，条形之间的间隔，默认 `0.2`。
- **`names.arg`** ：字符型向量，每个条形对应的名称。
- **`col`** ：颜色（单个或向量），控制条形颜色。
- **`main`** ：字符型，主标题。
- **`xlab`** ：字符型，X 轴标签。
- **`ylab`** ：字符型，Y 轴标签。
- **`beside`** ：逻辑值，矩阵输入时是否并列显示（默认 `FALSE` 堆叠，`TRUE` 并列）。
- **`horiz`** ：逻辑值，是否绘制水平条形图（默认 `FALSE` 垂直）。
```R
barplot(
  *height    = numeric | matrix,
  width     = numeric,
  space     = numeric | vector,
  names.arg = character,
  col       = character,
  main      = character,
  xlab      = character,
  ylab      = character,
  beside    = logical,
  horiz     = logical
)
```
# Stem Plots 茎叶图
- **`x`** ：数值型向量（必填），要绘制的数据。
- **`scale`** ：调整图形的缩放。默认 1，越大图越“拉伸”，越小图越“压缩”。
- **`width`** ：每行显示的最大宽度，默认 80 个字符。
- **`atom`** ：最小区分单位，默认 `1e-08`，用于避免浮点数舍入问题。
```R
stem(
  *x     = numeric,
  scale = numeric,
  width = integer,
  atom  = numeric
)
```
# Back-to-Back Stem-and-Leaf Plot 背靠背茎叶图
- `aplpack` 包内容
- **`*x`** ：数值型向量（必填），第一组数据。
- **`*y`** ：数值型向量（必填），第二组数据。
- **`m`** ：整数型，分割比例，决定叶子数如何被分组。
- **`na.rm`** ：逻辑值，是否移除缺失值（默认 `FALSE`）。
- **`rule.line`** ：逻辑值，是否在中间的茎叶轴绘制分隔线。
- **`col`** ：字符型或颜色向量，控制不同侧的颜色显示。
```R
library(aplpack)
stem.leaf.backback(
  *x        = numeric,
  *y        = numeric,
  m         = integer,
  na.rm     = logical,
  rule.line = logical,
  col       = character
)
```
# Frequency Distributions 频数分布表

# Histograms 直方图

# Cumulative Frequencies & Ogives 累积频数表与曲线

# Scatterplots 散点图

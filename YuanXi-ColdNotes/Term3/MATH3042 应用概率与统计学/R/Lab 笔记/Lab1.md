# Mosaic 包
- 安装 mosaic 包
```R
install.packages("mosaic")
```
- 加载 mosaic 包
```R
library(mosaic)
```
# 内置数据
- 在 Packages 标签下点击 datasets，即可查看系统库中自带的数据集
- MosiacData 包也有额外数据集
## Lab 示例：mosaic 包 TenMileRace 数据集
- 查看数据集用法
```R
help(TenMileRace)
```
- 将数据集展示为数据框
```R
view(TenMileRace)
```
### 数据过滤
1. 选出数据
- 查看跑步者成绩（net 时间）
```R
TenMileRace$net
```
- 保存到变量 `race.times`
```R
race.times <- TenMileRace$net
```
2. 数据判断
- 查看是否小于 4000 秒
```R
race.time < 4000
# TRUE / FALSE
```
- 显示前 6 个元素
```R
head(race.times)
# [1] 5978 4457 4928 4229 5076 5968
```
- 判断前 6 个元素是否小于 4000
```R
head(race.times < 4000)
# [1] FALSE FALSE FALSE FALSE FALSE FALSE
```
- 计算 TenMileRace 的 net 小于 4000 秒的人数
```R
sum(race.times < 4000)
# [1] 346
```
3. 条件提取
- 提取小于 4000 秒的行
```R
fast.runners <- subset(TenMileRace, net < 4000)
fast.runners
# 小于 4000 秒跑者的数据框

也可以使用 dplyr 包的 filter
install.packages("dplyr")
library(dplyr)
fast.runners <- filter(TenMileRace, net < 4000)
fast.runners
# 小于 4000 秒跑者的数据框
```
- 统计小于 4000 秒的人的数量（统计筛选出的数据框 fast. Runners 的行数）
```R
nrow(fast.runners)
# [1] 346
```
## 例题
##### 创建 slow. runners，包含 $net$ 时间 $>8000$ 秒的跑者
```R
slow.runners <- filter(TenMileRace, net > 8000)
```
##### 统计 slow. runners 人数
```R
nrow(slow.runners)
```
##### 列出下列数据
- 所有女性跑者
- 所有非美国跑者
```R
filter(TenMileRace, sex == "F")
# 先将 state 从 Factor 转换为字符，再判断长度大于 2
filter(TenMileRace, nchar(as.character(state)) > 2)
```
##### 生成一个表格，显示每个州/国家（除了美国）的跑者人数（仍会显示美国州名，但计数为 0。）
```R
# 筛选非美国跑者
nonUS.runners <- filter(TenMileRace, nchar(as.character(state)) > 2)

# 生成人数表（包含所有水平，美国州会显示为 0）
table(nonUS.runners$state)
```
##### 重做上一题，但使用 `droplevels()` 避免显示 0 的州名。
```R
# 筛选非美国跑者
nonUS.runners <- filter(TenMileRace, nchar(as.character(state)) > 2)

# 去掉无效 levels
nonUS.runners <- droplevels(nonUS.runners)

# 生成人数表（包含所有水平，美国州会显示为 0）
table(nonUS.runners$state)
```
##### 打印出跑者人数最多的州
```R
# 创建各州/国家的频数表
state.counts <- table(TenMileRace$state)

# 找出人数最多的州/国家
max.state <- names(which.max(state.counts))
max.state
```
##### 求出用时比最快女性更短的男性跑者人数
```R
nrow(
	filter(
		TenMileRace,
		sex == "M",
		net < min(data=TenMileRace, net ~ sex)
	)
)
```
##### 找到第一个跑者，其在 net 上的排名优于 time 排名，并输出其年龄、性别、州
```R
net.faster.than.time <- filter(TenMileRace, time > net)
net.faster.than.time[1, c("age", "sex", "state")]
```
##### 定义 “典型” 跑者：去掉最快 5% 和最慢 5% 之后的所有跑者。写命令生成新数据框，并用 `head()` 显示前几行。不得硬编码数字，除 0.05 和 0.95 外。
```R
typical.runners <- filter(
						TenMileRace, 
                        net >= quantile(TenMileRace$net, 0.05)
                        &
                        net <= quantile(TenMileRace$net, 0.95)
                    )
head(typical.runners)
```
##### 为典型跑者绘制直方图
```R
hist(
	typical.runners$net,
	main = paste(
				"Typical Runners (n = ", 
            	nrow(typical.runners),
            	")",
            	, sep=""
            )
	xlab = "Net (s)",
	ylab = "Frequency"
)
```
## 定义
- 两个集合 $X$，$Y$ 的笛卡尔积，又称直积，在集合论中表示为 $X × Y$，是所有可能的有序对组成的集合，其中有序对的第一个对象是 $X$ 的成员，第二个对象是 $Y$ 的成员。
$$
X \times Y = \{(x, y) \mid x \in X \land y \in Y\}
$$
- 例如, 如果如果集合 $X$ 是 13 个元素的点数集合 $\{A, K, Q, J, 10, 9, 8, 7, 6, 5, 4, 3, 2\}$，而集合 $Y$ 是 4 个元素的花色集合 $\{\spadesuit, \heartsuit, \diamondsuit, \clubsuit\}$，则这两个集合的笛卡儿积是有 52 个元素的标准扑克牌的集合：
$$
\{(A, \spadesuit), (K, \spadesuit), (Q, \spadesuit), \dots, (2, \spadesuit), \dots, (A, \clubsuit), \dots, (3, \clubsuit), (2, \clubsuit)\}.
$$
## 性质
- 对于任意集合 $A$，根据定义有 $A \times \emptyset = \emptyset \times A = \emptyset$。
- 一般来说笛卡儿积**不满足**交换律和结合律。
- 笛卡儿积对集合的并和交满足**分配律**，即：

$$
A \times (B \cup C) = (A \times B) \cup (A \times C)
$$

$$
(B \cup C) \times A = (B \times A) \cup (C \times A)
$$

$$
A \times (B \cap C) = (A \times B) \cap (A \times C)
$$

$$
(B \cap C) \times A = (B \times A) \cap (C \times A)
$$

$$
(A \times B) \cap (C \times D) = (A \cap C) \times (B \cap D)
$$

- 若一个集合 $A$ 包含有无限多的元素，那么这个集合对自身的笛卡儿积 $A \times A$ 有和 $A$ 一样多的元素。

**同余**是数论中的一个概念，用来描述整数之间的“模相等”关系。简而言之，如果两个整数对同一个数取模的余数相同，我们就说它们是同余的。
## 定义
给定整数 $a$、$b$ 和正整数 $n$，如果 $a$ 和 $b$ 对 $n$ 取模后得到的余数相等，那么我们称 $a$ 和 $b$ 在模 $n$ 意义下是同余的，记作：
$$
a \equiv b \pmod{n}
$$
这表示 $n$ 整除 $a - b$，即存在一个整数 $k$ 使得：
$$
a - b = kn
$$
## 示例
1. $17 \equiv 5 \pmod{12}$  
   因为 $17 - 5 = 12$，12可以被12整除，所以 $17$ 和 $5$ 对 $12$ 取模时同余。
2. $23 \equiv 2 \pmod{7}$  
   因为 $23 - 2 = 21$，21可以被7整除，所以 $23$ 和 $2$ 在模 $7$ 意义下同余。
## 性质
同余关系具有一些类似于等式的性质：
1. **自反性**：$a \equiv a \pmod{n}$
2. **对称性**：如果 $a \equiv b \pmod{n}$，那么 $b \equiv a \pmod{n}$
3. **传递性**：如果 $a \equiv b \pmod{n}$ 且 $b \equiv c \pmod{n}$，那么 $a \equiv c \pmod{n}$
此外，同余还可以在加法、减法和乘法运算中使用：
- **加法**：如果 $a \equiv b \pmod{n}$ 且 $c \equiv d \pmod{n}$，则 $a + c \equiv b + d \pmod{n}$
- **减法**：如果 $a \equiv b \pmod{n}$ 且 $c \equiv d \pmod{n}$，则 $a - c \equiv b - d \pmod{n}$
- **乘法**：如果 $a \equiv b \pmod{n}$ 且 $c \equiv d \pmod{n}$，则 $a \cdot c \equiv b \cdot d \pmod{n}$

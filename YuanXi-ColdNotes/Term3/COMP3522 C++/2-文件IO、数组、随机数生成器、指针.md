# 文件 IO
`<fstream>` 头文件包含了三个类
- `ifstream ` 用于只读
- `ofstream` 用于只写
- `fstream` 用于读取和写入
文件流可以使用 `<<` `>>` 操作符
## 开关文件
- 现代方式：定义对象的同时打开文件
```cpp
#include <fstream>
fstream f{"data.txt"} // 构造 fstream 的对象 f
if(!f.is_open()){
	cerr << "Unable to open file" << endl;
	exit(1);
}
f << "hello" << 123 << endl; // 向文件输入文字
f.close(); // 关闭文件
```
- 传统方式：先定义对象，再调用 `.open()`
```cpp
// 只读
ifstream fin;
fin.open("123.txt");
fin.close();

// 只写
ofstream fout;
fout.open("123.txt");
fin.close();

// 读写
fstream fs;
fs.open("123.txt");
fin.close();
```
##  buffer 缓冲区
在  C++ 的 IO 系统里，流对象并不直接与文件、终端交互，而是首先通过一个内部缓冲区，用于提高效率，避免频繁的系统调用
缓冲区几乎不需要手动管理，但仍可以显式控制：
-  `cout << flush;` 强制立即刷新缓冲区到屏幕
- `fout.flush();` 强制把文件缓冲区写入磁盘
### 文件流：`filebuf`
```cpp
ifstream fin("123.txt");
```
1. 文件内的数据进入缓冲区 `filebuf`
2. 数据交给 `fin`
### 标准 IO 流（cin、cout、cerr）：`streambuf`
```cpp
cout << "Hello";
```
1. “Hello”放入 `streambuf`
2. 显示到终端上
### 字符串流：`stringbuf`
```cpp
stringstream ss;
ss << 123;
cout << ss.str();  // 输出 "123"
```
1. 数据存入 `stringbuf` 中
2. 使用 `.str()` 取出数据
##  Openmod 打开模式
打开一个文件时，可以指定一个“模式”参数，告诉程序：
- 要如何使用这个文件（读、写、读写）
- 应当如何处理（追加、覆盖、二进制、从文件末尾开始等）
这些模式本质上是一些常量，定义在 `std::ios_base` 中，但调用时也可以使用 `std::ios`，因为 `std::ios` 继承了 `std::ios_base` 基类。
- `ios_base::in` ：读（`ifstream` 默认）
- `ios_base::out` ：写（`ofstream` 默认）
- `ios_base::app` ：append 追加，每次写入前都把“写指针”移到末尾追加，而不是覆盖）
- `ios_base::trunc` ：truncate 截断，**打开文件**时把原内容清空（默认）
- `ios_base::binary`： 二进制模式：精确处理字节，不做换行符转换
- `ios_base::ate` ：at end，打开文件时指针就放在末尾，但和 app 不同的是可以移动指针
### 打开模式的组合
打开模式被设计为 bitmask 位掩码，因此使用 `|` 按位或将不同模式组合起来：
```cpp
// 二进制输出
std::ifstream f1("data", std::ios::in | std::ios::binary);
// 追加写
std::ofstream f2("dest", std::ios::out | std::ios::app);
```

不同编译器的实现可能不同，但其逻辑为：
```
in     = 000001
out    = 000010
app    = 000100
trunc  = 001000
ate    = 010000
binary = 100000
```

这样当组合 `out` 和 `app` 时，就是
```
out  = 000010
app  = 000100
结果 = 000110   // 同时包含 out 和 app
```
## Char-by-char 逐字符读写
- 思路与 C 类似：
	- 用 `istream::get()` 取一个字符
	- 用 `ostream::put()` 写一个字符
```cpp
char c;
while ((c = in.get()) != EOF) {
 // ...
 }
```
由于 `get()` 返回的是 `int_type`，含有 `EOF` 特殊值，若装进 `char` 会丢失 EOF （End Of File）信息，因此更常使用
```cpp
// 逐字节拷贝：in -> out
std::ifstream in{src, std::ios::binary};
std::ofstream out{dst, std::ios::binary};
int ch;
while ((ch = in.get()) != EOF) {
  // 写出一个字节
  out.put(static_cast<char>(ch));
}
```
## Seeking within a file 文件内定位

## 概述
- Lambda是JDK8中的一个语法糖, 可以对一些匿名内部类的写法进行简化.
- 是函数式编程思想的一个重要体现
	- 不关注对象,更关注对数据进行的操作
- 当接口只有唯一一个抽象函数时, 可以对该接口的继承类实例使用 Lambda 表达式快速地重写抽象方法, 而不必显式地创建一个匿名内部类再重写方法
- 例
```java
@FunctionalInterface
interface Runnable() {
	void run(){}
}

Runnable task = new Runnable() {
    @Override
    public void run() {
        System.out.println("Task is running");
    }
};
task.run();


```
## 核心原则
- 可推导可省略
	- 如果参数的类型/方法名可以被推导出来,则可以省略类型/方法名
## 基本格式
`(参数列表)->{代码}`
例:
- 在创建线程并启动时可以使用匿名内部类的写法:
```java
new Thread(new Runnable(){
	@Override
	public void run(){
		System.out.println(123);
	}
}).start();
```
可以使用Lambda格式进行修改,修改后如下:
```java
new Thread(()->{
	System.out.println(123);
}).start();
```
-  现有如下方法,其中IntBinaryOperator是一个接口. 先使用匿名内部类的写法调用该方法
```java
public static int calculateNum(IntBinaryOperator operator) {
    int a = 10;
    int b = 20;
    return operator.applyAsInt(a, b);
}

public static void main(String[] args) {
	int i = calculateNum(new IntBinaryOperator(){
			@Override
			public int applyAsInt(int left, int right) {
				return left + right;
			}
		});
	System.out.println(i);
}

```
Lambda 写法: 函数式变成只关注参数和方法体,将匿名内部类的参数和方法体剪切出来,使用->连接
```java
public static void main(String[] args) {
	int i = calculateNum((int left, int right) -> left + right);
	System.out.println(i);
}
```
- 
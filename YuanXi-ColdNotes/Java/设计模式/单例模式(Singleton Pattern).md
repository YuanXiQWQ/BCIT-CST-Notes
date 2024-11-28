## 定义
- 单例设计模式, 是采取一定的方法保证在整个的软件系统中, 对某个类**只能存在一个对象实例**, 并且该类只提供一个取得其对象实例的方法 (静态)
## 性质
- 唯一性: 一个类只能有一个实例
- 全局性: 提供一个静态方法或全局变量, 允许程序的任何部分访问该实例
- 延迟初始化 (可选): 只有在第一次需要该实例时才进行初始化, 节省资源
## 实现要点
1. 私有构造函数: 禁止外部直接创建实例
2. 静态实例变量：  用于存储单例类的唯一实例
3. 静态方法（或静态块）：  提供全局访问入口，并负责创建实例（如果尚未创建）
## 实现方式
- **饿汉式（Eager Initialization）**
	- 静态常量
	- 静态代码块
- 懒汉式（Lazy Initialization）
	- 线程不安全
	- 线程安全, 同步方法
- **双重检查（Double-Checked Locking）**
- **静态内部类**
- **枚举**
### 饿汉式 (静态常量)
- 饿汉式单例在类加载时就立即创建实例，无论该实例是否被实际使用。这意味着在应用程序启动或类被首次引用时，单例对象已经存在。就像一个“饿汉”总是处于“饥饿”状态，随时准备“进食”或“行动”，饿汉式单例也始终存在，随时可以被调用和使用。
#### 步骤
1. 构造器私有化 ( 防止通过 new 获得实例)
2. 类的内部创建对象
3. 向外暴露一个静态的公共方法以返回实例对象
4. 代码实现
```java 
class SingleTon {
    // 1.构造器私有化 ( 防止通过 new 获得实例)
    private SingleTon() {}

    // 2.类的内部创建对象
    private final static SingleTon instance = new SingleTon();

    // 3.向外暴露一个静态的公共方法以返回实例对象
    public static SingleTon getInstance() {
        return instance;
    }
}
```
- 测试
```java
public class SingletonTest{
	public static void main(String[] args){
		// 第一次调用类方法, 实例已经被创建
		Singleton instance1 = Singleton.getInstance();
		// 第二次调用类方法, 返回的仍然是那个实例
		Singleton instance1 = Singleton.getInstance();
		// true
		System.out.println(instance1 == instance2);
		// Hash code 相同
		System.out.println("Hash code of instance1 ="instance1.hashCode());
		System.out.println("Hash code of instance2 ="instance2.hashCode());
	}
}
```
#### 特点
这种方式基于类装载机制避免了多线程的同步问题. 不过, 由于实例在类装载时就实例化, 尽管在单例模式中大多数是使用 `getInstance ()` 来进行类装载, 但是导致类装载的原因**仍有很多种**, 因此**不能确定是否有其他方式导致了类装载**, 此时就可能造成内存浪费
##### 优点
- 写法简单, 在类装载时就完成实例化, 避免了线程同步问题
##### 缺点
- 在类装载的时候就完成实例化, 如果从始至终都没使用过这个实例, 则会造成内存浪费
#### 静态代码块
- 在静态代码块中创建单例对象
```java 
class SingleTon {
    // 1.构造器私有化 ( 防止通过 new 获得实例)
    private SingleTon() {}

    // 2.类的内部创建对象
    private static SingleTon instance;
    
    // 在静态代码块中创建单例对象
    static {
    	// 可以在这里添加复杂的初始化逻辑 
		try {
			// 静态代码块中初始化实例 
			INSTANCE = new Singleton();
		} catch (Exception e) {
			throw new RuntimeException("初始化单例失败", e); 
		}
    }

    // 3.向外暴露一个静态的公共方法以返回实例对象
    public static SingleTon getInstance() {
        return instance;
    }
}
```
##### 特点
- 和静态常量类似, 只不过将类实例化的过程放在了静态代码块中
- 静态代码块同样是在类装载时执行
- 当单例实例的创建需要处理异常、进行多步初始化或者需要更复杂的逻辑时，静态代码块提供了更大的灵活性
###### 对比
- 静态常量
	- 适用于**简单且不需要额外初始化逻辑**的场景
	- 代码更加简洁高效
- 静态代码块
	- 适用于**需要处理复杂初始化逻辑或异常**的场景
	- 提供了更大的灵活性和控制力
### 懒汉式 (线程不安全)
- 仅在真正调用方法的时候对实例进行初始创建
- 避免了因其它方式造成的类装载导致实例被意外创建
#### 步骤
1. 构造器私有化 ( 防止通过 new 获得实例)
2. 将未初始化的对象实例保留为字段
3. 向外暴露一个静态的公共方法以仅初始时创建并返回实例对象
4. 代码实现
```java
class SingleTon {
    // 1.构造器私有化 ( 防止通过 new 获得实例)
    private SingleTon() {}

    // 2.将未初始化的对象实例保留为字段
    private final static SingleTon instance;

    // 3.向外暴露一个静态的公共方法以仅初始时创建并返回实例对象
    public static synchronized SingleTon getInstance() {
    	// 懒汉式: 仅在真正调用方法的时候对实例进行初始创建
    	if(instance == null){
    		 instance = new SingleTon()
    	}
        return instance;
    }
}
```
#### 特点
##### 优点
- 起到了懒加载 (Lazy Loading) 效果, 仅在需要实例时创建实例, 类似在前端中学到的仅滚动到相应页面位置时才加载元素的懒加载方法
##### 缺点
- 只能在单线程下使用, 多线程下, 如果一个线程进入了 `if(instance == null)` 判断语句块, 还未来得及继续执行, 另一个线程就也进入该判断句, 就会造成产生多个实例
#### 线程安全, 同步方法
- 使用同步方法改进原本线程不安全的初始化实例方法
```java
class SingleTon {
    // 1.构造器私有化 ( 防止通过 new 获得实例)
    private SingleTon() {}

    // 2.将未初始化的对象实例保留为字段
    private final static SingleTon instance;

    // 3.向外暴露一个静态的公共方法以仅初始时创建并返回实例对象
    // 使用同步方法 synchronized
    public static synchronized SingleTon getInstance() {
    	// 懒汉式: 仅在真正调用方法的时候对实例进行初始创建
    	if(instance == null){
    		 instance = new SingleTon()
    	}
        return instance;
    }
}
```
##### 特点
- 效率过低
- 每个线程在想要获得类实例时, 都要执行 ` getInstance ()` 方法
	- 而只有第一次 ` getInstance ()` 是为了初始化实例后返回
	- 往后只需要返回实例即可
	- 但是每次都要对方法进行同步
### 双重检查
- 对字段使用 `volatile` 关键字
	- 防止指令重排序
		-  `new (Singleton())` 的具体指令实际上包括
			1. **分配内存空间**: 为 `Singleton` 对象分配内存
			2. **初始化实例**: 调用构造器，初始化对象的各个字段
			3. **将 `instance` 指向分配的内存空间**: 将分配的内存地址赋值给 `instance` 变量
		- Java 编译器可能在初始化实例时对这三步重排序以提高性能, 步骤 3 可能在 2 前执行
			- 这意味着另一个线程可能在 `instance` 被初始化前就通过了 `(instance == null)` 检查, 从而访问到一个尚未完全初始化的对象
	- 保证可见性
		- 多线程下, 一个线程对 `instance` 的写入操作可能不会立即对其它线程可见
		- 每个线程可能会有自己的本地缓存, 从而导致它们读取到的仍是旧值 (`null`)
		- `volatile` 关键字确保其它线程立刻看到任何对该变量的修改
- 进行两次 `(instance == null)` 检查
	- 检查 1: 避免在实例已经被创建后再次进入含同步锁的代码块, 提升性能
	- 检查 2: 如果多个线程同时通过了检查 1, 通过同步锁保证了此时只有一条线程能够继续向下执行同步代码块, 此时会有两种情况:
		1. 此时 `instance` 未初始化, 通过检查 2, 对实例进行初始化
		2. 此时 `instance` 已经由第一个进入同步代码块的线程初始化, 未通过检查 2, 取消初始化
#### 步骤
1. 构造器私有化 ( 防止通过 new 获得实例)
2. 将未初始化的对象实例保留为字段, 并
	1. 禁止编译器对初始化该实例的指令重排序
	2. 保证任何线程对该变量时其它线程的可见性
3. 向外暴露一个静态的公共方法以返回实例对象, 并两次 instance 非空检查
	1. 避免实例被初始化后再进入同步锁 (保证效率)
	2. 避免多个线程进入同步锁后重复初始化实例 (保证线程安全)
4. 代码实现
```java
class SingleTon {
    // 1.构造器私有化 ( 防止通过 new 获得实例)
    private SingleTon() {}

    // 2.将未初始化的对象实例保留为字段
    // vloatile 禁止指令重排序, 并保证线程可见性
    private final static volatile SingleTon instance;

    // 3.向外暴露一个静态的公共方法以仅初始时创建并返回实例对象
    public static SingleTon getInstance() {
    	// 懒汉式: 仅在真正调用方法的时候对实例进行初始创建
    	// 检查1:在初始化实例处执行同步, 保证同时只能有一个线程执行初始化
    	if(instance == null){
    		// 同步锁, 保证线程安全
    		synchronized (Singleton.class){
    			/* 检查2: 此时第二个线程如果意外进来了,第一个线程已经初始化好了, 线程2再检
    			查就会不满足判断式而推出*/
				if(instance == null){
    				instance = new SingleTon()
				}
    		}
    	}
        return instance;
    }
}
```
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
	- 线程安全, 同步代码块
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
    public static SingleTon getInstance() {
    	// 懒汉式: 仅在真正调用方法的时候对实例进行初始创建
    	if(instance == null){
    		 instance = new SingleTon()
    	}
        return instance;
    }
}
```
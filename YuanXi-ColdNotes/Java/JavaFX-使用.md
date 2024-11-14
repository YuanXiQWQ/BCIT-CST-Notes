- JavaFX 必须扩展 `Application` 类并重写 `start()` 方法
- 在 `start()` 方法内部定义 `Stage` (也就是应用的窗口) 并设置 `Scene` (窗口的内容)
- 例
```java
public class TestJavaFX extends Application {
	@Override
	public void start(final Stage primaryStage){
		primaryStage.setTitle("Hello JavaFX!");
		primaryStage.show();
	}
}
```
- 在 JavaFX 项目中,main方法仅用于调用 `Application.launch(args)` , 这会初始化 JavaFX 环境并调用 `start()` 方法. 该方法将应用程序逻辑与 GUI 创建分开.
```java
public static void main(final String[] args){
	Application.launch(args);
	//或者简写成
	launch(args);
}
```
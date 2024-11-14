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
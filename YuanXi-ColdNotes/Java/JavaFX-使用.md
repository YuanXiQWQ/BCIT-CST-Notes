## 部署
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

## 启用
在 JavaFX 项目中,main方法仅用于调用 `Application.launch(args)` , 这会初始化 JavaFX 环境并调用 `start()` 方法. 该方法将应用程序逻辑与 GUI 创建分开.
```java
public static void main(final String[] args){
	Application.launch(args);
	//或者简写成
	launch(args);
}
```
### 最佳方法实践
在组织 JavaFX 应用程序时, 将逻辑与 `start()` 方法分开, 以保持代码可读性. 在单独的方法中初始化复杂组件 (如按钮和布局), 并从 `start()` 中调用他们.
```java
@Override
public void start(final Stage stage) {
    VBox layout = createLayout();
    Scene scene = new Scene(layout, 300, 200);
    stage.setScene(scene);
    stage.setTitle("Structured JavaFX App");
    stage.show();
}

private VBox createLayout() {
    Label label = new Label("Welcome to JavaFX!");
    Button button = new Button("Click me!");
    return new VBox(label, button);
}

```
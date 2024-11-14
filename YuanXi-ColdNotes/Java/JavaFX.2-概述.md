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
![[Pasted image 20241114081047.png]]

## 组容器
![[Pasted image 20241114081340.png]]
- `Stage` 表示一个顶级容器, 相当于窗口
- `Scene` 是显示在该舞台内的内容, 包括按钮, 文本字段和布局等节点
- 每个 JavaFX 应用程序都有一个由 `start()` 方法管理的主舞台
- `Scene Graphs` 是场景中组织应用程序的视觉组件
- 节点在场景图中排列, 每个节点可以包含子节点
```java
// 创建窗口
Stage stage = new Stage();
// 创建场景
Scene scene = new Scene(new VBox(), 400, 300);
// 指定窗口的场景
stage.setScene(scene);
// 显示包含了场景的窗口
stage.show();
```

### 场景图
- JavaFX 将组件组织成一个层次化的场景图, 其中每个组件都是一个节点, 节点可以与其子节点组成树状结构, 根节点(例如布局容器) 位于顶部
- 从一个单一的根节点 (如VBox, HBox)开始, 以有效管理子节点
```java
VBox root = new VBox();
Button btn = new Button("Click Me");
Label label = new Label("Hello, JavaFX");
root.getChildren().addAll(label, btn);
Scene scene = new Scene(root, 300, 200);

primaryStage.setScene(scene);
primaryStage.setTitle("My JavaFX GUI");
primaryStage.show();
```
![[Pasted image 20241114082616.png]]

### 舞台
- **一个舞台（Stage）只能包含一个场景（Scene）**：每个 `Stage` 只能加载一个 `Scene`，**不能把多个场景直接添加到同一个 `Stage` 中**，也**不能直接把一个场景嵌套到另一个场景中**。
    
- **一次只能在一个舞台上显示一个场景**：如果需要切换不同的显示内容（例如从一个界面切换到另一个界面），需要在同一个 `Stage` 上设置新的 `Scene`。这种切换可以通过 `Stage.setScene(newScene)` 方法实现。
```java
// 显示场景1
primaryStage.setScene(s1);
// 替换为场景2
primaryStage.setScene(s2);
```

#### 切换场景
```java
@Override
public void start(final Stage primaryStage) {
    // 创建第一个场景，包含一个按钮用于切换到第二个场景
    Button button1 = new Button("Go to Scene 2");
    StackPane layout1 = new StackPane(button1);
    Scene scene1 = new Scene(layout1, 300, 200);

    // 创建第二个场景，包含一个按钮用于切换回第一个场景
    Button button2 = new Button("Back to Scene 1");
    StackPane layout2 = new StackPane(button2);
    Scene scene2 = new Scene(layout2, 300, 200);

    // 设置按钮的动作以切换场景
    button1.setOnAction(e -> primaryStage.setScene(scene2));
    button2.setOnAction(e -> primaryStage.setScene(scene1));

    // 设置初始场景并显示舞台
    primaryStage.setScene(scene1);
    primaryStage.setTitle("场景切换示例");
    primaryStage.show();
}
```
![[Pasted image 20241114083327.png]]
![[Pasted image 20241114083342.png]]
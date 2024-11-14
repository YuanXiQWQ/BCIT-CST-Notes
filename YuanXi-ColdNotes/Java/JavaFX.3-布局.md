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
## 布局 (Layouts)
- 常见布局包括
	- VBox (Vertical Box, 垂直布局)
	- HBox (Horizontal Box, 水平布局)
	- GridPane (表格布局)
- 布局避免了绝对定位(`setLayoutX()` , `setLayoutY()`), 提供响应式设计
```java
@Override
public void start(Stage primaryStage) {
    // 在顶部创建一个垂直标签
    Label verticalLabel = new Label("Vertical Layout:");

    // 在HBox内创建一个水平标签
    Label horizontalLabel = new Label("Horizontal Layout:");

    // 创建一个HBox，包含一个标签和两个按钮，水平排列
    HBox hbox = new HBox(10); // 10像素间距
    Button button1 = new Button("Button 1");
    Button button2 = new Button("Button 2");
    hbox.getChildren().addAll(horizontalLabel, button1, button2);

    // 创建一个VBox以垂直排列标签和HBox
    VBox vbox = new VBox(15); // 15像素间距
    vbox.getChildren().addAll(verticalLabel, hbox);

    // 设置场景，以VBox作为根布局
    Scene scene = new Scene(vbox, 300, 200);

    // 配置舞台
    primaryStage.setScene(scene);
    primaryStage.setTitle("HBox and VBox with Labels");
    primaryStage.show();
}
```
![[Pasted image 20241114083728.png]]

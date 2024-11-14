## 布局容器 (Layouts Containers)
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

## 控件
- 使用户能够输入数据并接受反馈
- 是可以添加到布局容器 (如VBox, HBox) 的节点
- 常见的控件包括
	- 按钮(Button): 用于触发操作
	- 标签(Label): 显示文本信息
	- 文本框(TextField): 输入单行文本
### 创建按钮
- 按钮应避免分配过长的标签，因为这可能会影响可读性并导致对齐问题。
```java
Button button = new Button("Submit");
VBox layout = new VBox(button);
Scene scene = new Scene(layout, 200, 100);
```
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
### 按钮
- 使用 `Button` 类创建
- 应避免分配过长的标签，否则可能会影响可读性并导致对齐问题。
```java
Button button = new Button("Submit");
VBox layout = new VBox(button);
Scene scene = new Scene(layout, 200, 100);
```

### 标签
- 使用 `Label` 类创建
- 是非交互式的 (只读), 用户无法直接修改文本
- 因为其只读性, 通常用来显示指令或状态更新
```java
Label greeting = new Label("Welcome to JavaFX!");
VBox layout = new VBox(greeting);
Scene scene = new Scene(layout, 300, 150);

```

### 文本框
- 使用 `TextField` 类创建
- 用于单行文本输入
- 使用 `setText()` 设置初始文本, `getText()` 获取用户输入
```java
TextField nameField = new TextField();
nameField.setPromptText("Enter your name"); // 占位符文本
String userName = nameField.getText();      // 获取输入
```

以下是 `TextArea` 控件的使用说明：

### 文本区 (TextArea)
- 使用 `TextArea 类创建
- 用于多行文本输入，非常适合用于较长的输入内容，如描述、评论或消息
- 使用 `setText()` 设置初始文本, `getText()` 获取用户输入
- 支持自动换行，水平和垂直滚动条，当内容超过可见区域时会自动出现滚动条
```java
TextArea commentsArea = new TextArea();
commentsArea.setPromptText("Enter your comments"); // 占位符文本
String comments = commentsArea.getText();          // 获取输入
```

## 在布局容器中添加控件
**所有控件必须添加到布局容器中**, 不允许直接添加到场景中, 否则将导致编译错误
```java
// 编译错误
Scene scene = new Scene(button);

// 正确
Vbox layout = new VBox(button);
Scene scene = new Scene(layout, 200, 100);
```

## 表格布局
- `GridPane` 将组件按行和列排列, 类似表格结构
- 可以为每个组件指定行和列, 并设置间距和填充
```
```
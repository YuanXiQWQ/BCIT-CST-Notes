## 布局容器 (Layouts Containers)
- 常见布局包括
	- VBox (Vertical Box, 垂直布局)
	- HBox (Horizontal Box, 水平布局)
	- GridPane (表格布局)
- 布局避免了绝对定位 (`setLayoutX()` , `setLayoutY()`), 提供响应式设计
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
- 是可以添加到布局容器 (如 VBox, HBox) 的节点
- 常见的控件包括
	- 按钮 (Button): 用于触发操作
	- 标签 (Label): 显示文本信息
	- 文本框 (TextField): 输入单行文本
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
```java
// 创建一个带有单元格间距的 GridPane 布局
GridPane grid = new GridPane();
grid.setHgap(10); // 设置单元格之间的水平间距
grid.setVgap(10); // 设置单元格之间的垂直间距

// 向网格添加组件
Label nameLabel = new Label("Name:");
TextField nameField = new TextField();
grid.add(nameLabel, 0, 0); // 列 0，行 0
grid.add(nameField, 1, 0); // 列 1，行 0

Label emailLabel = new Label("Email:");
TextField emailField = new TextField();
grid.add(emailLabel, 0, 1); // 列 0，行 1
grid.add(emailField, 1, 1); // 列 1，行 1

Label phoneLabel = new Label("Phone:");
TextField phoneField = new TextField();
grid.add(phoneLabel, 0, 2); // 列 0，行 2
grid.add(phoneField, 1, 2); // 列 1，行 2

// 创建和设置场景
Scene scene = new Scene(grid, 300, 200);
primaryStage.setScene(scene);
primaryStage.setTitle("GridPane Example");
primaryStage.show();

```

## 锚点面板
- `AnchorPane` 将组件固定在与面板边界特定距离的位置
- 可以通过设定锚点约束动态调整以适应窗口大小变化
```java
Button button = new Button("Click Me");

AnchorPane.setTopAnchor(button, 10.0); // 距顶部10像素
AnchorPane.setLeftAnchor(button, 20.0); // 距左侧20像素

anchorPane.getChildren().add(button);

Scene scene = new Scene(anchorPane, 300, 200);
primaryStage.setScene(scene);
primaryStage.setTitle("AnchorPane Example");
primaryStage.show();
```

## 边界面板
- `BorderPane` 将布局分为五个区域: 
	- 顶部 (Top)
	- 底部 (Bottom)
	- 左侧 (Left)
	- 右侧 (Right)
	- 中心 (Center)
```java
BorderPane borderPane = new BorderPane();
borderPane.setTop(new Label("顶部区域"));
borderPane.setLeft(new Label("左侧区域"));
borderPane.setCenter(new Label("中心区域"));
borderPane.setRight(new Label("右侧区域"));
borderPane.setBottom(new Label("底部区域"));

Scene scene = new Scene(borderPane, 300, 200);
primaryStage.setScene(scene);
primaryStage.setTitle("BorderPane 示例");
primaryStage.show();
```

## 堆叠面板
- `StackPane` 允许节点相互叠加. 先添加的在底部, 按照栈式排列
- 适合分层组件, 例如图像上显示文本
```java
@Override
public void start(Stage stage) {
    ImageView imageView = new ImageView(new Image("file:sky.jpg"));
    Label overlayText = new Label("享受生活！");
    overlayText.setStyle("-fx-text-fill: white;");

    StackPane stackPane = new StackPane(imageView, overlayText);
    stage.setScene(new Scene(stackPane, 300, 200));
    stage.show();
}
```

## 灵活布局
- 避免使用固定尺寸, 使用布局容器自动调整布局
```java
// 不推荐的做法：固定宽度按钮
Button fixedWidthButton = new Button("固定宽度按钮");
fixedWidthButton.setPrefWidth(300); // 可能在较小屏幕上适配不佳

// 推荐的做法：灵活宽度按钮
Button flexibleWidthButton = new Button("灵活宽度按钮");
flexibleWidthButton.setMaxWidth(Double.MAX_VALUE); // 根据屏幕大小自适应

// 布局
VBox badPracticeBox = new VBox(10, fixedWidthButton);
badPracticeBox.setPadding(new Insets(10));
badPracticeBox.setStyle("-fx-border-color: red; -fx-border-width: 2; -fx-padding: 10;");

VBox goodPracticeBox = new VBox(10, flexibleWidthButton);
goodPracticeBox.setPadding(new Insets(10));
goodPracticeBox.setStyle("-fx-border-color: green; -fx-border-width: 2; -fx-padding: 10;");

// 将两者添加到 HBox 中以进行并排比较
HBox root = new HBox(20, badPracticeBox, goodPracticeBox);
root.setPadding(new Insets(20));

Scene scene = new Scene(root, 600, 200);
stage.setScene(scene);
stage.setTitle("布局实践：不推荐 vs 推荐");
stage.show();
```
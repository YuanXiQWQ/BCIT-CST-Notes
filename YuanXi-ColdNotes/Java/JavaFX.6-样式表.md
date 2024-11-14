JavaFX支持使用CSS和FXML来样式化GUI组件, 以便将设计, 结构与逻辑分离
- CSS
	- 对 GUI 进行样式设置
	- 使用 `scene.getStylesheets().add()` 加载 `.css` 文件
- FXML
	- 在 XML 中定义 UI
	- 使用 `FXMLLoader.load()` 加载 `.fxml` 文件
## CSS
### 方法
- `getStylesheets()` 方法用于获取元素关联的所有样式表文件
- `getStyleClass()` 方法用于获取元素的类
- `setId("<ID>")` 方法用于给元素添加 ID
- 在 get 指定元素后使用 
	- `add("<String>")` 添加属性值
	- `addAll("<String1>","<String2>")` 添加多个属性值
	- `remove("<String>")` 移除属性值
	- `removeAll("<String1>", "<String2>")` 移除多个属性值
	- `contains("<String>")` 检查是否包含属性值 (boolean)
	- `isEmpty()` 检查是否为空 (boolean)
### 配置
1. 创建一个 `styles.css` 文件
```css
.label {
    -fx-font-size: 16px;
    -fx-text-fill: blue;
}

.button {
    -fx-background-color: #FF6347;
    -fx-text-fill: white;
}
```
2. 在 JavaFX 中应用 CSS
```java
public class CSSExample extends Application {
    @Override
    public void start(final Stage stage) {
        Label label = new Label("Styled Label");
        Button button = new Button("Styled Button");

        VBox root = new VBox(10, label, button);
        Scene scene = new Scene(root, 300, 200);

        // 加载 CSS 文件
		scene.getStylesheets()
			.add(getClass().getResource("/styles.css").toExternalForm());

        stage.setScene(scene);
        stage.setTitle("CSS 示例");
        stage.show();
    }

    public static void main(final String[] args) {
        launch(args);
    }
}
```

## FXML
- 是一种基于 XML 的语言, 可以将 GUI 结构与逻辑分离
### 配置
1. 创建一个 `example.fxml` 文件
```xml
<?xml version="1.0" encoding="UTF-8"?>
<?import javafx.scene.layout.VBox?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.control.Button?>

<VBox spacing="10" xmlns:fx="http://javafx.com/fxml">
    <Label text="Hello from FXML!" />
    <Button text="Click Me" />
</VBox>
```
2. 在 JavaFX 中应用 FXML
```java
public class FXMLExample extends Application {
    @Override
    public void start(Stage stage) throws Exception {
        // 加载 FXML 文件
        Parent root = FXMLLoader.load(getClass().getResource("/example.fxml"));

        Scene scene = new Scene(root, 300, 200);
        stage.setScene(scene);
        stage.setTitle("FXML 示例");
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

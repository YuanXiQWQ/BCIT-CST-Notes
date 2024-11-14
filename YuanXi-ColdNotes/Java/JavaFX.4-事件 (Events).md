## 概述
- 每个空间都可以监听点击或文本更改等事件
- 可以使用 Lambda 表达式进行简洁的事件处理

## 添加动作
```java
Button button = new Button("Click Me");
button.setOnAction(event -> System.out.println("Hello!"));
```

#### Lambda表达式使用准则
- 避免在 Lambda 中使用长事件代码, 将长代码拆分为单独方法
```java
// 带有长 lambda 表达式的按钮
Button longLambdaButton = new Button("计算");
longLambdaButton.setOnAction(event -> {
    int result = 0;
    for (int i = 1; i <= 10; i++) {
        result += i;
    }
    System.out.println("计算完成：" + result);
});

// 使用单独方法重构处理逻辑的按钮
Button refactoredButton = new Button("计算");
refactoredButton.setOnAction(event -> performCalculations());

// 布局和场景设置
VBox vbox = new VBox(10, longLambdaButton, refactoredButton);
Scene scene = new Scene(vbox, 300, 200);
primaryStage.setScene(scene);
primaryStage.setTitle("计算按钮示例");
primaryStage.show();

// 单独的方法来处理计算
private void performCalculations() {
    int result = 0;
    for (int i = 1; i <= 10; i++) {
        result += i;
    }
    System.out.println("重构计算完成：" + result);
}

```

## 菜单和回调函数
### 创建菜单
1. 在场景中放置面板 (例如放置在窗口顶部)
2. 在面板中放入菜单栏
3. 在菜单栏中放入菜单
4. 在菜单中放入菜单项
5. 给菜单项添加 `setOnAction()` 方法
```java
public class MenuExample extends Application {
    @Override
    public void start(Stage stage) {
        MenuBar menuBar = new MenuBar();
        Menu fileMenu = new Menu("文件");
        Menu helpMenu = new Menu("帮助");

        MenuItem openItem = new MenuItem("打开");
        openItem.setOnAction(e -> openFile());

        MenuItem saveItem = new MenuItem("保存");
        saveItem.setOnAction(e -> saveFile());

        MenuItem aboutItem = new MenuItem("关于");
        aboutItem.setOnAction(e -> showAbout());

        fileMenu.getItems().addAll(openItem, saveItem);
        helpMenu.getItems().add(aboutItem);

        menuBar.getMenus().addAll(fileMenu, helpMenu);

        BorderPane root = new BorderPane();
        root.setTop(menuBar);

        Scene scene = new Scene(root, 400, 300);
        stage.setScene(scene);
        stage.setTitle("菜单示例：方法调用");
        stage.show();
    }

    private void openFile() {
        System.out.println("调用了打开文件方法！");
    }

    private void saveFile() {
        System.out.println("调用了保存文件方法！");
    }

    private void showAbout() {
        System.out.println("调用了关于方法！");
    }
}

```
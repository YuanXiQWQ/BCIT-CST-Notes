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
import javafx.application.Application;  
import javafx.scene.Scene;  
import javafx.scene.control.*;  
import javafx.scene.layout.BorderPane;  
import javafx.stage.Stage;

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
![[Pasted image 20241114101134.png]]
## 线程 (Threading)和图形用户界面 (GUI)
- JavaFX 采用单线程 UI 模型, 所有 UI 更改必须在 JavaFX 应用程序线程上进行
### JavaFX 应用程序线程 (the JavaFX Application Thread) 
- JavaFX 用来进行所有 UI 更新的主线程
- 如果在该线程上运行耗时的操作, 整个方法栈会被阻塞, 导致界面无响应
- 使用 `javafx.concurrent` 包提供的 `Task<V>` 和 `Service<V>` 类帮助在应用程序线程之外运行耗时的任务, 并在任务完成时安全地更新 UI
	- `Task<V>`: 表示一个单独的后台操作, 适用于一次性任务
	- `Service<V>`: 适合需要多次运行或重新启动的任务
- `Task<V>` 和 `Service<V>` 类支持像 `onSucceeded`, `onFailed`, `onCancelled` 这样的属性, 可以用来指定任务在对应状态时的处理方式

### `Task<V>`
- `V`
	- 任务的返回值类型
	- 是一个泛型参数, 因此在创建 `Task` 时指定类型, 就可以定义任务完成后产生的结果类型
	- 是 `Task` 类的方法 `call()` 返回的结果类型
- 当 `Task` 执行成功后, 可以用该类的 `getValue()` 方法获取结果. 该结果的类型为 `V`
- 例1: 返回一个字符串结果
```java
Task<String> stringTask = new Task<>() {
    @Override
    protected String call() {
        return "Hello, World!";
    }
};
```
- 例2: 返回一个整数结果
```java
Task<Integer> intTask = new Task<>() {
    @Override
    protected Integer call() {
        return 42;
    }
};
```
- 例3: 无返回值
```java
Task<Void> voidTask = new Task<>() {
    @Override
    protected Void call() {
        System.out.println("Doing some work...");
        return null; // Void 需要返回 null
    }
};
```
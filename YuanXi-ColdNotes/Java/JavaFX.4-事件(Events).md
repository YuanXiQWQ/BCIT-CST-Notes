## 概述
- 每个空间都可以监听点击或文本更改等事件
- 可以使用 Lambda 表达式进行简洁的事件处理

## 添加动作
### 按钮
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
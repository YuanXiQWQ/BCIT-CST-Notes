JavaFX 采用单线程 UI 模型, 所有 UI 更改必须在 JavaFX 应用程序线程上进行
## JavaFX 应用程序线程 (the JavaFX Application Thread) 
- JavaFX 用来进行所有 UI 更新的主线程
- 如果在该线程上运行耗时的操作, 整个方法栈会被阻塞, 导致界面无响应
- 使用 `javafx.concurrent` 包提供的 `Task<V>` 和 `Service<V>` 类帮助在应用程序线程之外运行耗时的任务, 并在任务完成时安全地更新 UI
	- `Task<V>`: 表示一个单独的后台操作, 适用于一次性任务
	- `Service<V>`: 适合需要多次运行或重新启动的任务
- `Task<V>` 和 `Service<V>` 类支持像 `onSucceeded`, `onFailed`, `onCancelled` 这样的属性, 可以用来指定任务在对应状态时的处理方式(`Service<V>` 的属性在前面加一个 `set` ,如 `setOnSucceeded`)

## 后台任务
- 创建后台任务以避免响应时间过长的方法占用主线程导致界面阻塞
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
        return "你好!";
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
        System.out.println("正在搞事...");
        return null; // Void 需要返回 null
    }
};
```

### `Service<V>`
- 只是一个负责管理任务创建, 启动, 停止, 重启等操作的框架, 本身并没有直接执行后台任务的职能, 不能直接替代 `Task<V>`. 

## 方法回调
- 例1: 在点击按钮后, 唤起 `task` 任务. 该任务会在执行成功后用返回值更新 `statusLabel`.
```java
public class Gui extends Application {
    @Override
    public void start(Stage stage) {
        Label statusLabel = new Label("Waiting...");
        Button startButton = new Button("Start Task");

        // 定义一个返回字符串结果的 Task
        Task<String> task = new Task<>() {
            @Override
            protected String call() throws InterruptedException {
                Thread.sleep(2000); // 模拟后台工作
                return "Task Completed Successfully!";
            }
        };

        // 当任务成功完成时更新标签
        task.setOnSucceeded(e -> {
            String result = task.getValue(); // 获取任务的结果
            statusLabel.setText(result);     // 用结果更新标签
        });

        // 在点击按钮时，在新线程上启动任务
        startButton.setOnAction(e -> new Thread(task).start());

        VBox root = new VBox(10, statusLabel, startButton);
        stage.setScene(new Scene(root, 300, 150));
        stage.setTitle("Task Example with getValue()");
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
```
- 例2: 点击按钮后执行任务并在 `statusLabel` 中返回任务状态, 同时更改按钮文字. 该任务会在失败时自动重启.
```java
public class Gui extends Application {
    @Override
    public void start(Stage stage) {
        Label statusLabel = new Label("等待中...");
        Button controlButton = new Button("开始");

        // 定义一个用于重复后台工作的 Service
        Service<String> service = new Service<>() {
            @Override
            protected Task<String> createTask() {
                return new Task<>() {
                    @Override
                    protected String call() throws InterruptedException {
                        if (Math.random() < 0.3) throw new RuntimeException("随机失败！");
                        Thread.sleep(2000); // 模拟后台工作
                        return "成功！";
                    }
                };
            }
        };

        // 定义服务每个状态的 UI 更新
        service.setOnRunning(e -> {
            statusLabel.setText("运行中...");
            controlButton.setText("取消");
        });

        service.setOnSucceeded(e -> {
            statusLabel.setText("完成：" + service.getValue());
            controlButton.setText("重新开始");
        });

        service.setOnFailed(e -> {
            statusLabel.setText("失败：" + service.getException().getMessage());
            controlButton.setText("重新开始");
        });

        service.setOnCancelled(e -> {
            statusLabel.setText("已取消！");
            controlButton.setText("重新开始");
        });

        // 处理按钮点击，用于取消或重启服务
        controlButton.setOnAction(e -> {
            if (service.isRunning()) {
                service.cancel(); // 取消正在运行的服务
            } else {
                service.restart(); // 重启服务
            }
        });

        VBox root = new VBox(10, statusLabel, controlButton);
        stage.setScene(new Scene(root, 300, 150));
        stage.setTitle("带动态按钮的服务示例");
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```
## 直接更新UI
- JavaFX (以及大多数GUI框架) 为了确保线程安全和 UI 渲染稳定性, 采用单线程模型处理 UI 更新. 对于 JavvaFX 来说, 该线程就是 JavaFX 应用线程
- 除此之外, 很多操作系统及底层图形库都是单线程设计, 因此多线程更新 UI 可能会导致未定义行为. 因此, JavaFX 禁止在外部线程直接更新 UI, 否则会抛出运行时错误:  `IlleagalStateException`
- 如果要在后台任务线程中更新 UI, 需要使用方法 `Platform.runLater()` . 该方法可以将更新操作发送到 JavaFX 应用线程的事件队列中, 保证操作按顺序在线程上执行, 从而确保线程安全和数据一致性.
- 例
```java
public class Gui extends Application {
    @Override
    public void start(Stage stage) {
        Label statusLabel = new Label("状态：等待中...");
        Label progressLabel = new Label("进度：0%");

        // 模拟具有周期性 UI 更新的后台工作
        new Thread(() -> {
            for (int i = 1; i <= 10; i++) {
                try {
                    Thread.sleep(500); // 模拟工作
                    int progress = i * 10; // 计算进度
                    Platform.runLater(() -> {
                        statusLabel.setText("状态：工作中...");
                        progressLabel.setText("进度：" + progress + "%");
                    });
                } catch (InterruptedException e) {
                    Platform.runLater(() -> statusLabel.setText("状态：已中断！"));
                    return;
                }
            }
            // 完成后的最终更新
            Platform.runLater(() -> statusLabel.setText("状态：已完成！"));
        }).start();

        VBox root = new VBox(10, statusLabel, progressLabel);
        stage.setScene(new Scene(root, 250, 150));
        stage.setTitle("Platform.runLater 增强示例");
        stage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```
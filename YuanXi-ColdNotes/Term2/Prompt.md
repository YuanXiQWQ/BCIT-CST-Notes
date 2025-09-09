请使用中文对话.请你根据要求完成游戏. 该游戏强制要求符合下列要求:
## 游戏概述
**游戏名称**：MinecraftItem
**游戏目标**：玩家需要根据提示，在 3 x 3 的工作台上摆放正确的物品，完成指定物品的合成。
## 游戏界面设计
- **问题区**：
    - 显示提示文字：“请提供该物品的合成配方”。
    - 在提示文字下方显示待合成物品的图片。
- **选项区**：
    - 显示九个可供选择的物品（图标），供玩家选择放置到工作台上。
    - 这些物品包括正确的合成材料和干扰项。
- **回答区（工作台）**：
    - 一个 3 x 3 的网格，代表工作台。
    - 玩家可以点击网格中的格子，将选项区的物品放置到对应位置。
    - 包含一个“提交”按钮，玩家点击后提交当前的配方。
- **反馈区**：
    - 显示当前得分、剩余题目数等信息。
    - 在提交后，显示合成是否成功的反馈。
## 游戏逻辑
1. **题目生成**：
    - 从预设的 Minecraft 可合成物品列表中随机选择一个物品作为当前题目。
    - 获取该物品的正确合成配方。
2. **选项生成**：
    - 将正确的合成材料加入选项区。
    - 随机添加其他干扰物品，凑够九个选项。
3. **玩家操作**：
    - 玩家从选项区选择物品，点击工作台的格子进行放置。
    - 选项区的物品可以重复使用。
4. **配方判定**：
    - 在玩家点击“提交”按钮后，检查玩家在工作台上的摆放是否与正确配方匹配（考虑平移和水平翻转）。
5. **得分规则**：
    - 若配方正确，得 1 分，并进入下一题。
    - 若配方错误，不得分，直接进入下一题。
    - 一共进行 10 道题，结束后弹窗询问用户是否继续, 如果用户选否, 通过弹窗统计得分, 格式 (代码层面) 为 
```java
StringBuilder sb;  
sb = new StringBuilder();
sb.append("Game Statistics:")  
        .append("\nTotal Games Played: ").append(gamesPlayed)  
        .append("\nTotal Score: ").append(totalScore)  
        .append("\nAverage Scores per Game: ")  
        .append(String.format("%.2f", averageScores));
```
1. **配方匹配规则**：
    - **允许的变换**：
        - 平移：在工作台范围内，配方可以向左、右、上、下平移。
        - 水平翻转：配方可以水平镜像翻转。
    - **不允许的变换**：
        - 旋转：配方不能旋转。
        - 超出工作台范围：配方不能超出 3 x 3 的工作台。
	- 坐标以工作台的中心格子, 也就是第二列第二行为原点 (0,0), 那么它的坐标范围应该是
		- $x$ 轴的范围：$x \in {-1, 0, 1}$
		- $y$ 轴的范围：$y \in {-1, 0, 1}$
	- **示例**：
		- 定义物品"木棍"的合成配方为木板 (0,0) 和木板 (0,-1), 那么能够合成木棍的配方可以是:
			- (-1, 0), (-1, -1)（左移 1 格）
			- (-1, 1), (-1, 0)（左移 1 格，上移 1 格）
			- (0, 1), (0, 0)（上移 1 格）
			- (0, 0), (0, -1)（原配方）
			- (1, 1), (1, 0)（右移 1 格，上移 1 格）
			- (1, 0), (1, -1)（右移 1 格）
		- 以下是不能合成的反例和原因
			- 木板 (0,0), 木板 (1,0): 配方 90°旋转
			- 木板 (0,0), 木板 (1,-1): 配方 45°旋转
			- 木板 (0,-1), 木板 (0,-2): 超出范围
		- 定义钻石斧的配方为钻石 (0,1), 钻石 (1,1), 木棍 (0,0), 钻石 (1,0), 木棍 (0,-1), 那么能够合成钻石斧的配方可以是:
			- 钻石 (0,1), 钻石 (1,1), 木棍 (0,0), 钻石 (1,0), 木棍 (0,-1) : 原配方
			- 钻石 (-1,1), 钻石 (0,1), 木棍 (-1,0), 钻石 (0,0), 木棍 (-1,-1)(配方左移一格)  
			- 钻石 (0,1), 钻石 (-1,1), 木棍 (0,0), 钻石 (-1,0), 木棍 (0,-1)(配方水平翻转)  
			- 钻石 (1,1), 钻石 (0,1), 木棍 (1,0), 钻石 (0,0), 木棍 (1,-1)(配方水平翻转后右移一格)
		- 以下是不能合成的反例和原因
			- 钻石 (2,1), 钻石 (1,1), 木棍 (2,0), 钻石 (1,0), 木棍 (2,-1): 超出范围
## 强制需要使用的技术
### 1. JavaFX 界面
- **应用内容**：JavaFX 用于构建游戏的 GUI 界面，包括按钮、网格布局、事件处理等。
### 2. 面向对象编程
- **继承和多态：
    - 创建一个基类 `Item`，表示所有的物品。
    - 派生出具体的物品类，如 `CraftingItem`、`MaterialItem` 等。
    - 使用多态来处理不同类型的物品。
- **抽象类和接口**：
    - 定义一个接口 `Craftable`，包含方法 `getRecipe()`。
    - 抽象类 `AbstractItem` 实现公共方法，具体物品类继承该抽象类。
### 3. 集合和泛型
- **集合**：
    - 使用 `List` 或 `Map` 来存储物品列表、配方等。
    - 使用 `Set` 来处理不重复的物品。
- **泛型**：
    - 定义泛型方法或类，处理不同类型的集合。
- **迭代器**：
    - 使用迭代器遍历物品集合，生成选项和检查配方。
### 4. 异常处理
- 在玩家操作和配方判定过程中，可能会出现异常情况（如数组越界、空指针等），需要使用异常处理来保证程序的健壮性。
### 5. Lambda 表达式和方法引用
- **Lambda 表达式**：
    - 在事件处理器中，使用 Lambda 表达式简化代码，例如按钮点击事件。
- **方法引用**：
    - 如果有适用的地方，可以使用方法引用来进一步简化代码。
### 6. 文件和流
- **文件读取**：
    - 从外部文件中读取物品的图片。
- **流式处理**：
    - 使用流来过滤和处理物品列表，如随机选择题目、生成选项等。
### 7. 设计模式
- **单例模式**：
    - 例如，使用单例模式来管理游戏的状态或配置。
- **工厂模式**：
    - 使用工厂模式创建物品对象，根据类型返回相应的实例。
- **观察者模式**：
    - 在玩家操作后，更新界面和状态，使用观察者模式监听变化。
### 8. 单元测试
- 为关键的逻辑部分编写单元测试，例如配方匹配算法，确保游戏逻辑的正确性。
### 9. 内部类
- 使用内部类来组织代码，例如在界面类中定义事件处理的内部类。
### 10. 线程和并发（可选）
- 如果需要，可以使用线程来处理耗时操作，确保界面不卡顿。
### 11. 其他内容
- **验证和正则表达式**：
    - 在输入或文件读取时，使用验证和正则表达式确保数据格式正确。
- **StringBuilder：
    - 在生成提示文字或日志时，使用 `StringBuilder` 提高效率。
## 文件说明
- **MyGame. Java**：主程序文件，包含游戏的主要逻辑和界面。
- **Item. Java**：物品基类，定义基本属性和方法。
- **CraftingItem. Java**：可合成物品类，包含配方信息。
- **MaterialItem. Java**：材料物品类。
- **Recipe. Java**：配方类，定义合成所需的材料和位置。
- **GameController. Java**：游戏控制器，处理事件和游戏状态。
- **applications. Txt**：列出各个技术的应用位置。
## 注意事项
- **代码注释**：请在代码中添加详细的英文注释，说明各部分的功能和实现细节。
- **用户体验**：界面简洁美观，操作流畅，提供清晰的反馈。
- **错误处理**：在玩家进行非法操作时，提供友好的提示，而不是程序崩溃。
## 起始代码
- 从 `Main` 的 `minecraftItem.start();` 来运行整个 MinecraftItem 游戏
```java
// Main.java
import java.util.Scanner;  
  
/**  
 * The main entry point of the application. Displays the menu and handles user choices to * start different games. Ensures the program runs in a loop until the user decides to * quit. * * @author Jiarui Xing  
 */public class Main {  
    /**  
     * The main method that starts the application.     *     * @param args command-line arguments (not used)  
     */    public static void main(final String[] args)  
    {  
        final Scanner scanner = new Scanner(System.in);  
        while(true)  
        {  
            printMenu();  
            final String choice = scanner.nextLine().trim().toLowerCase();  
            switch(choice)  
            {  
                case "w":  
                    final WordGame wordGame = new WordGame();  
                    wordGame.start();  
                    break;  
                case "n":  
                    final NumberGame numberGame = new NumberGame();  
                    numberGame.start();  
                    break;  
                case "m":  
                    final MinecraftItem minecraftItem = new MinecraftItem();  
                    minecraftItem.start();  
                    break;  
                case "q":  
                    System.out.println("Quitting the program. Goodbye!");  
                    scanner.close();  
                    System.exit(0);  
                default:  
                    System.out.println("Invalid input. Please enter W, N, M, or Q.");  
            }  
        }  
    }  
  
    /**  
     * Prints the main menu options to the console.     */    private static void printMenu()  
    {  
        StringBuilder sb;  
        sb = new StringBuilder();  
        sb.append("Press W to play the Word game.\n")  
                .append("Press N to play the Number game.\n")  
                .append("Press M to play the MinecraftItem.\n")  
                .append("Press Q to quit.\n")  
                .append("Your choice: ");  
        System.out.print(sb);  
    }  
}

// Game.java
/**  
 * Represents a game interface. Can be used to define common methods for different games. * * @author Jiarui Xing  
 */public interface Game {  
    void start();  
}
```
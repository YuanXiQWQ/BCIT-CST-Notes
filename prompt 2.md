请你遵照这个格式来检测我的代码在技术列标中对应的技术的首次使用,并告知我没有用到什么技术:
## 参考格式
lesson 1: initializers in class X
overloading in class Y

lesson 2: inheritance in class A and B
exceptions in class C and D

lesson 3: overriding in class E
substitution in class D

lesson 4: abstract methods in class B
abstract classes in class E

lesson 5: collections in class F
iterator in class G

lesson 6: lambda expressions in class B
method references in class C
nested classes in class F

lesson 8: scanner in class F
file in class A
streams and filters in class B

lesson 9: GUI in class MyGUI
lesson 10: unit tests in class BTest
lesson 11: design pattern in class A
lesson 12: concurrency in class MyGUI

## 技术列表
lesson 1:
    Validation
    Method Overloading
    Constructor Chaining
    Stringbuilder
    Regex

lesson 2:
    Inheritance
    Polymorphism
    Exception Handling
    
lesson 3:
    Final Method
    Abstract Class
    
lesson 4:
    Interfaces
    
lesson 5:
    Arrays
    Collections (List, Map, Set)
    Enhanced For Loop
    Generics Collections
    Iterators

lesson 6:
    Generics Methods
    Nested Classes
    
lesson 7:
    Functional Interfaces
    Lambdas
    Method References

lesson 8:
    Paths
    Files
    Scanner
    Streaming
    Random

lesson 9:
    JavaFX
    Threading
    
lesson 10:
    Unit Testing

lesson 11:
    Singleton
    Factory
    Abstract Factory
    Command
    Decorator
    Observer

lesson 12:
    Thread
    Timer/TimerTask
    Executor
    Future Task
    Parallel Task

## 我的代码:
```java
// Craftable.java  
  
/**  
 * Interface representing craftable items. */public interface Craftable {  
    /**  
     * Get the crafting recipe of the item.     *     * @return Recipe object  
     */    Recipe getRecipe();  
}

// CraftingItem.java  
  
/**  
 * Represents a craftable item with a recipe. */public class CraftingItem extends Item implements Craftable {  
    private final Recipe recipe;  
  
    public CraftingItem(String name, String imagePath, Recipe recipe)  
    {  
        super(name, imagePath);  
        this.recipe = recipe;  
    }  
  
    @Override  
    public Recipe getRecipe()  
    {  
        return recipe;  
    }  
}

// Game.java

/**  
 * Represents a game interface. Can be used to define common methods for different games. * * @author Jiarui Xing  
 */public interface Game {  
    void start();  
}

// GameController.java  
  
import javafx.application.Platform;  
import javafx.scene.control.Alert;  
import javafx.scene.control.Alert.AlertType;  
  
import java.util.*;  
import java.util.stream.Collectors;  
  
/**  
 * Controls the game logic, handles player actions, and updates the game state. * * @author  
 */  
public class GameController {  
    private int totalQuestions = 10; // Total number of questions in the game  
  
    private int score = 0;  
    private int currentQuestion = 0;  
    private CraftingItem currentItem;  
    private List<Item> optionItems;  
    private final Map<Recipe.Position, String> playerRecipe;  
  
    private final List<CraftingItem> craftingItems;  
    private final List<MaterialItem> materialItems;  
    private List<CraftingItem> availableItems;  
  
    // Game statistics  
    private int gamesPlayed = 0;  
    private int totalScore = 0;  
  
    private MinecraftItem gameUI;  
  
    // Track attempts left for the current question  
    private int attemptsLeft = 2; // Allow one retry after first failure  
  
    public GameController(MinecraftItem gameUI)  
    {  
        this.gameUI = gameUI;  
        craftingItems = new ArrayList<>();  
        materialItems = new ArrayList<>();  
        playerRecipe = new HashMap<>();  
  
        loadItems();  
    }  
  
    /**  
     * Load items and recipes.     */    private void loadItems()  
    {  
        // Load material items  
        materialItems.add(new MaterialItem("Wood Planks", "images/wood_planks.png"));  
        materialItems.add(new MaterialItem("Stick", "images/stick.png"));  
        materialItems.add(new MaterialItem("Diamond", "images/diamond.png"));  
        materialItems.add(new MaterialItem("Iron Ingot", "images/iron_ingot.png"));  
        materialItems.add(new MaterialItem("Gold Ingot", "images/gold_ingot.png"));  
        materialItems.add(new MaterialItem("Cobblestone", "images/cobblestone.png"));  
        materialItems.add(new MaterialItem("String", "images/string.png"));  
        materialItems.add(new MaterialItem("Feather", "images/feather.png"));  
        materialItems.add(new MaterialItem("Flint", "images/flint.png"));  
        materialItems.add(new MaterialItem("Leather", "images/leather.png"));  
        materialItems.add(new MaterialItem("Paper", "images/paper.png"));  
        materialItems.add(new MaterialItem("Gunpowder", "images/gunpowder.png"));  
        materialItems.add(new MaterialItem("Sand", "images/sand.png"));  
        materialItems.add(new MaterialItem("Glass", "images/glass.png"));  
        materialItems.add(new MaterialItem("Redstone", "images/redstone.png"));  
        materialItems.add(new MaterialItem("Lapis Lazuli", "images/lapis_lazuli.png"));  
        materialItems.add(new MaterialItem("Emerald", "images/emerald.png"));  
        materialItems.add(new MaterialItem("Obsidian", "images/obsidian.png"));  
        materialItems.add(new MaterialItem("Ender Pearl", "images/ender_pearl.png"));  
        materialItems.add(new MaterialItem("Book", "images/book.png"));  
        materialItems.add(new MaterialItem("Eye of Ender", "images/eye_of_ender.png"));  
        materialItems.add(new MaterialItem("Ghast Tear", "images/ghast_tear.png"));  
  
        // Load crafting items with recipes  
        // Stick        Recipe stickRecipe = new Recipe();  
        stickRecipe.addItem(0, 0, "Wood Planks");  
        stickRecipe.addItem(0, -1, "Wood Planks");  
        craftingItems.add(new CraftingItem("Stick", "images/stick.png", stickRecipe));  
  
        // Diamond Axe  
        Recipe diamondAxeRecipe = new Recipe();  
        diamondAxeRecipe.addItem(0, 1, "Diamond");  
        diamondAxeRecipe.addItem(1, 1, "Diamond");  
        diamondAxeRecipe.addItem(1, 0, "Diamond");  
        diamondAxeRecipe.addItem(0, 0, "Stick");  
        diamondAxeRecipe.addItem(0, -1, "Stick");  
        craftingItems.add(new CraftingItem("Diamond Axe", "images/diamond_axe.png",  
                diamondAxeRecipe));  
  
        // Iron Sword  
        Recipe ironSwordRecipe = new Recipe();  
        ironSwordRecipe.addItem(0, 1, "Iron Ingot");  
        ironSwordRecipe.addItem(0, 0, "Iron Ingot");  
        ironSwordRecipe.addItem(0, -1, "Stick");  
        craftingItems.add(  
                new CraftingItem("Iron Sword", "images/iron_sword.png", ironSwordRecipe));  
  
        // Bow  
        Recipe bowRecipe = new Recipe();  
        bowRecipe.addItem(-1, 0, "Stick");  
        bowRecipe.addItem(0, 1, "Stick");  
        bowRecipe.addItem(0, -1, "Stick");  
        bowRecipe.addItem(1, 1, "String");  
        bowRecipe.addItem(1, 0, "String");  
        bowRecipe.addItem(1, -1, "String");  
        craftingItems.add(new CraftingItem("Bow", "images/bow.png", bowRecipe));  
  
        // Arrow  
        Recipe arrowRecipe = new Recipe();  
        arrowRecipe.addItem(0, 1, "Flint");  
        arrowRecipe.addItem(0, 0, "Stick");  
        arrowRecipe.addItem(0, -1, "Feather");  
        craftingItems.add(new CraftingItem("Arrow", "images/arrow.png", arrowRecipe));  
  
        // Enchanting Table  
        Recipe enchantingTableRecipe = new Recipe();  
        enchantingTableRecipe.addItem(-1, -1, "Obsidian");  
        enchantingTableRecipe.addItem(-1, 0, "Diamond");  
        enchantingTableRecipe.addItem(0, -1, "Obsidian");  
        enchantingTableRecipe.addItem(0, 0, "Obsidian");  
        enchantingTableRecipe.addItem(0, 1, "Book");  
        enchantingTableRecipe.addItem(1, -1, "Obsidian");  
        enchantingTableRecipe.addItem(1, 0, "Diamond");  
        craftingItems.add(  
                new CraftingItem("Enchanting Table", "images/enchanting_table.gif",  
                        enchantingTableRecipe));  
  
        // End Crystal  
        Recipe endCrystalRecipe = new Recipe();  
        endCrystalRecipe.addItem(-1, -1, "Glass");  
        endCrystalRecipe.addItem(-1, 0, "Glass");  
        endCrystalRecipe.addItem(-1, 1, "Glass");  
        endCrystalRecipe.addItem(0, -1, "Ghast Tear");  
        endCrystalRecipe.addItem(0, 0, "Eye of Ender");  
        endCrystalRecipe.addItem(0, 1, "Glass");  
        endCrystalRecipe.addItem(1, -1, "Glass");  
        endCrystalRecipe.addItem(1, 0, "Glass");  
        endCrystalRecipe.addItem(1, 1, "Glass");  
        craftingItems.add(new CraftingItem("End Crystal", "images/end_crystal.gif",  
                endCrystalRecipe));  
  
        // Add more crafting items as needed...  
    }  
  
    /**  
     * Start the game by generating the first question.     */    public void startGame()  
    {  
        gamesPlayed++;  
        score = 0;  
        currentQuestion = 0;  
  
        // Initialize available items and shuffle  
        availableItems = new ArrayList<>(craftingItems);  
        Collections.shuffle(availableItems);  
  
        // Set totalQuestions to min(10, available items)  
        totalQuestions = Math.min(10, availableItems.size());  
  
        nextQuestion();  
    }  
  
    /**  
     * Generate the next question.     */    public void nextQuestion()  
    {  
        if(currentQuestion >= totalQuestions || availableItems.isEmpty())  
        {  
            endGame();  
            return;  
        }  
  
        currentQuestion++;  
        // Reset attempts  
        attemptsLeft = 2;  
  
        // Randomly select a crafting item  
        currentItem = availableItems.remove(0);  
  
        // Generate options  
        generateOptions();  
  
        // Reset player recipe  
        playerRecipe.clear();  
  
        // Update the UI accordingly  
        gameUI.updateUI();  
    }  
  
    /**  
     * Generate options including correct materials and distractors.     */    private void generateOptions()  
    {  
        optionItems = new ArrayList<>();  
        Set<String> materialNames = new HashSet<>();  
  
        // Add correct materials  
        for(String itemName : currentItem.getRecipe().getRecipeMap().values())  
        {  
            if(!materialNames.contains(itemName))  
            {  
                materialNames.add(itemName);  
                optionItems.add(getMaterialItemByName(itemName));  
            }  
        }  
  
        // Add distractor materials  
        Random rand = new Random();  
        while(optionItems.size() < 9 && optionItems.size() < materialItems.size())  
        {  
            MaterialItem material = materialItems.get(rand.nextInt(materialItems.size()));  
            if(!materialNames.contains(material.getName()))  
            {  
                materialNames.add(material.getName());  
                optionItems.add(material);  
            }  
        }  
  
        // Shuffle options  
        Collections.shuffle(optionItems);  
    }  
  
    /**  
     * Get a material item by its name.     *     * @param name Material item name  
     * @return MaterialItem object  
     */    private MaterialItem getMaterialItemByName(String name)  
    {  
        for(MaterialItem item : materialItems)  
        {  
            if(item.getName().equals(name))  
            {  
                return item;  
            }  
        }  
        return null;  
    }  
  
    /**  
     * Handle the player's action when they place an item on the crafting grid.     *     * @param gridX    Grid X-coordinate (0 to 2)  
     * @param gridY    Grid Y-coordinate (0 to 2)  
     * @param itemName Name of the item placed  
     */    public void placeItemOnGrid(int gridX, int gridY, String itemName)  
    {  
        // Convert grid coordinates to recipe positions (-1, 0, 1)  
        int x = gridX - 1;  
        int y = 1 - gridY; // Invert Y-axis  
  
        Recipe.Position position = new Recipe.Position(x, y);  
        if(itemName != null)  
        {  
            playerRecipe.put(position, itemName);  
        } else  
        {  
            playerRecipe.remove(position);  
        }  
    }  
  
    /**  
     * Submit the player's recipe and check if it matches the correct recipe.     */    public void submitRecipe()  
    {  
        boolean isCorrect = checkRecipe();  
        if(isCorrect)  
        {  
            score++;  
            gameUI.displayFeedback(true, false); // 成功，跳到下一题  
        } else  
        {  
            attemptsLeft--;  
            if(attemptsLeft > 0)  
            {  
                gameUI.displayFeedback(false, true); // 第一次失败，允许重试  
            } else  
            {  
                gameUI.displayFeedback(false, false); // 第二次失败，跳到下一题  
            }  
        }  
    }  
  
    /**  
     * Skip the current question. The question is not counted towards the score.     */    public void skipQuestion()  
    {  
        nextQuestion();  
    }  
  
    /**  
     * Check if the player's recipe matches the correct recipe, considering allowed     * transformations.     *     * @return True if correct, False otherwise  
     */    private boolean checkRecipe()  
    {  
        Map<Recipe.Position, String> correctRecipe =  
                currentItem.getRecipe().getRecipeMap();  
  
        // Generate all allowed transformations of the correct recipe  
        List<Map<Recipe.Position, String>> transformedRecipes =  
                generateTransformedRecipes(correctRecipe);  
  
        // Compare player's recipe with each transformed recipe  
        for(Map<Recipe.Position, String> transformedRecipe : transformedRecipes)  
        {  
            if(recipesMatch(playerRecipe, transformedRecipe))  
            {  
                return true;  
            }  
        }  
        return false;  
    }  
  
    /**  
     * Generate all allowed transformations (translations and horizontal flips) of the     * recipe.     *     * @param recipe Original recipe map  
     * @return List of transformed recipes  
     */    private List<Map<Recipe.Position, String>> generateTransformedRecipes(  
            Map<Recipe.Position, String> recipe)  
    {  
        List<Map<Recipe.Position, String>> transformedRecipes = new ArrayList<>();  
  
        // Possible translations  
        int[] dx = {-1, 0, 1};  
        int[] dy = {-1, 0, 1};  
  
        for(int tx : dx)  
        {  
            for(int ty : dy)  
            {  
                if(canTranslate(recipe, tx, ty))  
                {  
                    Map<Recipe.Position, String> translatedRecipe =  
                            translateRecipe(recipe, tx, ty);  
                    transformedRecipes.add(translatedRecipe);  
  
                    // Add horizontal flip of the translated recipe  
                    Map<Recipe.Position, String> flippedRecipe =  
                            horizontalFlipRecipe(translatedRecipe);  
                    if(isWithinBounds(flippedRecipe))  
                    {  
                        transformedRecipes.add(flippedRecipe);  
                    }  
                }  
            }  
        }  
  
        return transformedRecipes;  
    }  
  
    /**  
     * Check if translating the recipe by (dx, dy) keeps all positions within bounds.     *     * @param recipe Original recipe map  
     * @param dx     Translation in X-direction  
     * @param dy     Translation in Y-direction  
     * @return True if translation keeps all positions within bounds, False otherwise  
     */    private boolean canTranslate(Map<Recipe.Position, String> recipe, int dx, int dy)  
    {  
        for(Recipe.Position pos : recipe.keySet())  
        {  
            int newX = pos.getX() + dx;  
            int newY = pos.getY() + dy;  
            if(newX < -1 || newX > 1 || newY < -1 || newY > 1)  
            {  
                return false;  
            }  
        }  
        return true;  
    }  
  
    /**  
     * Translate the recipe by given offsets.     *     * @param recipe Original recipe  
     * @param dx     Offset in X-direction  
     * @param dy     Offset in Y-direction  
     * @return Translated recipe  
     */    private Map<Recipe.Position, String> translateRecipe(  
            Map<Recipe.Position, String> recipe, int dx, int dy)  
    {  
        Map<Recipe.Position, String> newRecipe = new HashMap<>();  
        for(Map.Entry<Recipe.Position, String> entry : recipe.entrySet())  
        {  
            int newX = entry.getKey().getX() + dx;  
            int newY = entry.getKey().getY() + dy;  
            newRecipe.put(new Recipe.Position(newX, newY), entry.getValue());  
        }  
        return newRecipe;  
    }  
  
    /**  
     * Perform a horizontal flip of the recipe.     *     * @param recipe Original recipe  
     * @return Horizontally flipped recipe  
     */    private Map<Recipe.Position, String> horizontalFlipRecipe(  
            Map<Recipe.Position, String> recipe)  
    {  
        Map<Recipe.Position, String> newRecipe = new HashMap<>();  
        for(Map.Entry<Recipe.Position, String> entry : recipe.entrySet())  
        {  
            int newX = -entry.getKey().getX();  
            int newY = entry.getKey().getY();  
            newRecipe.put(new Recipe.Position(newX, newY), entry.getValue());  
        }  
        return newRecipe;  
    }  
  
    /**  
     * Check if all positions in the recipe are within bounds.     *     * @param recipe Recipe map to check  
     * @return True if all positions are within bounds, False otherwise  
     */    private boolean isWithinBounds(Map<Recipe.Position, String> recipe)  
    {  
        for(Recipe.Position pos : recipe.keySet())  
        {  
            if(pos.getX() < -1 || pos.getX() > 1 || pos.getY() < -1 || pos.getY() > 1)  
            {  
                return false;  
            }  
        }  
        return true;  
    }  
  
    /**  
     * Check if two recipes match exactly.     *     * @param recipe1 First recipe  
     * @param recipe2 Second recipe  
     * @return True if recipes match, False otherwise  
     */    private boolean recipesMatch(Map<Recipe.Position, String> recipe1,  
                                 Map<Recipe.Position, String> recipe2)  
    {  
        if(recipe1.size() != recipe2.size())  
        {  
            return false;  
        }  
        for(Map.Entry<Recipe.Position, String> entry : recipe1.entrySet())  
        {  
            String itemName = recipe2.get(entry.getKey());  
            if(itemName == null || !itemName.equals(entry.getValue()))  
            {  
                return false;  
            }  
        }  
        return true;  
    }  
  
    /**  
     * End the game and show statistics.     */    private void endGame()  
    {  
        totalScore += score;  
        double averageScore = (double) totalScore / gamesPlayed;  
  
        // Build statistics string  
        StringBuilder sb = new StringBuilder();  
        sb.append("游戏统计:").append("\n游戏次数: ").append(gamesPlayed)  
                .append("\n总得分: ").append(totalScore).append("\n平均每局得分: ")  
                .append(String.format("%.2f", averageScore));  
  
        // Show statistics  
        Platform.runLater(() ->  
        {  
            Alert alert = new Alert(Alert.AlertType.INFORMATION);  
            alert.setTitle("游戏统计");  
            alert.setHeaderText(null);  
            alert.setContentText(sb.toString());  
            alert.showAndWait();  
  
            // Ask if the player wants to play again  
            gameUI.askToPlayAgain();  
        });  
    }  
  
    /**  
     * Get the current item to craft.     *     * @return Current CraftingItem  
     */    public CraftingItem getCurrentItem()  
    {  
        return currentItem;  
    }  
  
    /**  
     * Get the list of option items.     *     * @return List of Items  
     */    public List<Item> getOptionItems()  
    {  
        return optionItems;  
    }  
  
    /**  
     * Get the player's current recipe.     *     * @return Map of Position to item names  
     */    public Map<Recipe.Position, String> getPlayerRecipe()  
    {  
        return playerRecipe;  
    }  
  
    /**  
     * Get the current score.     *     * @return Current score  
     */    public int getScore()  
    {  
        return score;  
    }  
  
    /**  
     * Get the remaining number of questions.     *     * @return Remaining questions  
     */    public int getRemainingQuestions()  
    {  
        return totalQuestions - currentQuestion;  
    }  
  
    /**  
     * Get the remaining attempts for the current question.     *     * @return Remaining attempts  
     */    public int getAttemptsLeft()  
    {  
        return attemptsLeft;  
    }  
  
    /**  
     * Reset the player's recipe for retrying.     */    public void resetPlayerRecipe()  
    {  
        playerRecipe.clear();  
        Platform.runLater(() -> gameUI.resetCraftingGrid());  
    }  
}

// Item.java

/**  
 * Abstract base class representing a generic item in the game. Provides basic properties * like name and image path. * * @author Jiarui Xing  
 */public abstract class Item {  
    protected String name;  
    protected String imagePath;  
  
    public Item(String name, String imagePath)  
    {  
        this.name = name;  
        this.imagePath = imagePath;  
    }  
  
    /**  
     * Get the name of the item.     *     * @return item name  
     */    public String getName()  
    {  
        return name;  
    }  
  
    /**  
     * Get the image path of the item.     *     * @return image path  
     */    public String getImagePath()  
    {  
        return imagePath;  
    }  
}

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

// MaterialItem.java

// MaterialItem.java  
  
/**  
 * Represents a material item that can be used in crafting recipes. */public class MaterialItem extends Item {  
  
    public MaterialItem(String name, String imagePath)  
    {  
        super(name, imagePath);  
    }  
}

// MinecraftItem.java
  
import javafx.animation.PauseTransition;  
import javafx.application.Application;  
import javafx.application.Platform;  
import javafx.geometry.Insets;  
import javafx.geometry.Pos;  
import javafx.scene.Cursor;  
import javafx.scene.ImageCursor;  
import javafx.scene.Scene;  
import javafx.scene.control.*;  
import javafx.scene.image.Image;  
import javafx.scene.image.ImageView;  
import javafx.scene.input.MouseButton;  
import javafx.scene.layout.*;  
import javafx.stage.Stage;  
import javafx.util.Duration;  
  
import java.io.File;  
import java.util.List;  
  
/**  
 * Main class for the MinecraftItem game. Extends JavaFX Application and implements the * Game interface. */public class MinecraftItem extends Application implements Game {  
  
    private GameController gameController;  
  
    // UI components  
    private HBox topOptionsBox;  
    private Pane centerPane; // 使用Pane进行绝对定位  
    private ImageView backgroundImageView; // 背景图片  
    private GridPane craftingGrid; // 工作台格子  
    private StackPane itemDisplayCell; // 合成物格子  
    private ImageView itemToCraftImageView;  
    // private ImageView feedbackImageView; // 已移除  
  
    private Label scoreLabel;  
    private Label remainingLabel;  
    // private Button submitButton; // 已移除  
    private Button skipButton;  
    private Label feedbackLabel; // 新增反馈标签  
  
    private Stage primaryStage;  
  
    // Currently selected item  
    private String selectedItemName = null;  
    private String selectedItemImagePath = null;  
    private ImageCursor selectedCursor = null;  
  
    @Override  
    public void start(Stage primaryStage) throws Exception  
    {  
        this.primaryStage = primaryStage;  
        gameController = new GameController(this);  
  
        // Initialize UI components  
        initUIComponents();  
  
        // Set up the main layout  
        BorderPane mainLayout = new BorderPane();  
        mainLayout.setPadding(new Insets(20));  
  
        mainLayout.setStyle("-fx-background-color: #c6c6c6;");  
  
        // Top area: 1x9 candidate items  
        VBox topArea = new VBox(10);  
        topArea.setAlignment(Pos.CENTER);  
        topArea.getChildren().add(topOptionsBox);  
        mainLayout.setTop(topArea);  
  
        // Center area: Pane with background image, crafting grid, and item display  
        centerPane = new Pane();  
        centerPane.setPrefSize(472, 266); // 背景图片大小为472×266  
  
        // 设置背景图片  
        backgroundImageView = createBackgroundImageView();  
        centerPane.getChildren().add(backgroundImageView);  
  
        // 创建工作台格子  
        craftingGrid = createCraftingGrid();  
        // 手动设置工作台格子的位置（相对于背景图片）  
        craftingGrid.setLayoutX(8); // X轴位置  
        craftingGrid.setLayoutY(48); // Y轴位置  
        centerPane.getChildren().add(craftingGrid);  
  
        // 创建合成物格子  
        itemDisplayCell = createItemDisplayCell();  
        // 手动设置合成物格子的位置（相对于背景图片）  
        itemDisplayCell.setLayoutX(368);  
        itemDisplayCell.setLayoutY(104);  
        centerPane.getChildren().add(itemDisplayCell);  
  
        // 使用 StackPane 让 centerPane 居中  
        StackPane centerContainer = new StackPane(centerPane);  
        centerContainer.setAlignment(Pos.CENTER); // 居中对齐  
        mainLayout.setCenter(centerContainer);  
  
        // 添加要合成的物品ImageView到合成物格子中  
        itemToCraftImageView = new ImageView();  
        itemToCraftImageView.setFitWidth(64);  
        itemToCraftImageView.setFitHeight(64);  
        itemToCraftImageView.setVisible(false); // 初始隐藏  
        itemDisplayCell.getChildren().add(itemToCraftImageView);  
  
        mainLayout.setCenter(centerPane);  
  
        // Bottom control area: score, remaining questions, skip button, and feedback  
        // label        HBox controlArea = new HBox(20);  
        controlArea.setAlignment(Pos.CENTER_LEFT);  
        scoreLabel = new Label("得分: 0");  
        remainingLabel = new Label("剩余题目数: 10");  
        skipButton = new Button("跳过");  
        skipButton.setOnAction(e -> gameController.skipQuestion());  
  
        // 初始化反馈标签，设置为红色字体，初始为空  
        feedbackLabel = new Label("");  
  
        // 将scoreLabel, remainingLabel, skipButton, feedbackLabel添加到controlArea  
        controlArea.getChildren()  
                .addAll(scoreLabel, remainingLabel, skipButton, feedbackLabel);  
        mainLayout.setBottom(controlArea);  
  
        // Set the scene with specified size  
        Scene scene = new Scene(mainLayout, 800, 400);  
        primaryStage.setTitle("MinecraftItem Game");  
        primaryStage.setScene(scene);  
        primaryStage.show();  
  
        // Start the game  
        gameController.startGame();  
        updateUI();  
  
        // 在 start 方法中，为 itemDisplayCell 添加点击事件  
        itemDisplayCell.setOnMouseClicked(event ->  
        {  
            if(event.getButton() == MouseButton.PRIMARY)  
            {  
                gameController.submitRecipe();  
            }  
        });  
  
    }  
  
    /**  
     * Initialize UI components, including top options and crafting grid.     */    private void initUIComponents()  
    {  
        // Initialize the top options box (1x9)  
        topOptionsBox = new HBox(5);  
        topOptionsBox.setAlignment(Pos.CENTER);  
        // Initially empty; will be populated in updateUI()  
    }  
  
    /**  
     * Create the background ImageView.     *     * @return Configured ImageView  
     */    private ImageView createBackgroundImageView()  
    {  
        ImageView bgImageView = new ImageView();  
        Image bgImage = loadImage("images/background.png");  
        if(bgImage != null)  
        {  
            bgImageView.setImage(bgImage);  
            bgImageView.setFitWidth(472);  
            bgImageView.setFitHeight(266);  
        } else  
        {  
            // 如果背景图片加载失败，设置一个默认背景色  
            bgImageView.setStyle("-fx-background-color: #d3d3d3;");  
        }  
        return bgImageView;  
    }  
  
    /**  
     * Create a cell for the item to craft display with border.     *     * @return StackPane representing the item display cell  
     */    private StackPane createItemDisplayCell()  
    {  
        StackPane cell = new StackPane();  
        cell.setPrefSize(95, 95);  
        cell.setStyle(  
                "-fx-background-color: transparent; -fx-border-color: transparent;");  
        return cell;  
    }  
  
    /**  
     * Create the crafting grid (3x3 GridPane).     *     * @return Configured GridPane  
     */    private GridPane createCraftingGrid()  
    {  
        GridPane grid = new GridPane();  
        grid.setHgap(8);  
        grid.setVgap(8);  
        grid.setAlignment(Pos.CENTER);  
  
        for(int row = 0; row < 3; row++)  
        {  
            for(int col = 0; col < 3; col++)  
            {  
                StackPane cell = createCraftingCell(col, row);  
                grid.add(cell, col, row);  
            }  
        }  
  
        return grid;  
    }  
  
    /**  
     * Create a cell for the crafting grid.     *     * @param col Column index  
     * @param row Row index  
     * @return StackPane representing the cell  
     */    private StackPane createCraftingCell(int col, int row)  
    {  
        StackPane cell = new StackPane();  
        cell.setPrefSize(64, 64);  
        cell.setStyle(  
                "-fx-background-color: transparent; -fx-border-color: transparent;");  
        cell.setOnMouseClicked(event ->  
        {  
            if(event.getButton() == MouseButton.PRIMARY)  
            {  
                if(selectedItemName != null && selectedItemImagePath != null)  
                {  
                    // Place the selected item in the cell  
                    Image image = loadImage(selectedItemImagePath);  
                    if(image != null)  
                    {  
                        ImageView imageView = new ImageView(image);  
                        imageView.setFitWidth(60);  
                        imageView.setFitHeight(60);  
                        cell.getChildren().clear();  
                        cell.getChildren().add(imageView);  
  
                        // Update game controller  
                        gameController.placeItemOnGrid(col, row, selectedItemName);  
                    }  
                    // Reset cursor and selection  
                    resetCursor();  
                } else  
                {  
                    // 如果没有选择任何物品，移除该格子的物品  
                    cell.getChildren().clear();  
                    gameController.placeItemOnGrid(col, row, null);  
                }  
            } else if(event.getButton() == MouseButton.SECONDARY)  
            {  
                // 右键点击移除该格子的物品  
                cell.getChildren().clear();  
                gameController.placeItemOnGrid(col, row, null);  
            }  
        });  
        return cell;  
    }  
  
    /**  
     * Update the UI components with the current game state.     */    public void updateUI()  
    {  
        // Update the top candidate items (1x9)  
        topOptionsBox.getChildren().clear();  
        List<Item> options = gameController.getOptionItems();  
        for(Item item : options)  
        {  
            Image itemImage = loadImage(item.getImagePath());  
            Button button = getButton(item, itemImage);  
            topOptionsBox.getChildren().add(button);  
        }  
  
        // Update the item to craft display  
        String imagePath = gameController.getCurrentItem().getImagePath();  
        Image image = loadImage(imagePath);  
        if(image != null)  
        {  
            itemToCraftImageView.setImage(image);  
            itemToCraftImageView.setFitWidth(64);  
            itemToCraftImageView.setFitHeight(64);  
            itemToCraftImageView.setVisible(true);  
        } else  
        {  
            itemToCraftImageView.setImage(null);  
            itemToCraftImageView.setVisible(false);  
        }  
  
        // Update score and remaining labels  
        scoreLabel.setText("得分: " + gameController.getScore());  
        remainingLabel.setText("剩余题目数: " + gameController.getRemainingQuestions());  
  
        // Clear crafting grid  
        for(javafx.scene.Node node : craftingGrid.getChildren())  
        {  
            if(node instanceof StackPane cell)  
            {  
                cell.getChildren().clear();  
            }  
        }  
  
        // Reset cursor and selection  
        resetCursor();  
  
        // 清除反馈标签  
        feedbackLabel.setText("");  
    }  
  
    private Button getButton(Item item, Image itemImage)  
    {  
        ImageView imageView = new ImageView(itemImage);  
        imageView.setFitWidth(64);  
        imageView.setFitHeight(64);  
        Button button = new Button();  
        button.setGraphic(imageView);  
        button.setStyle("-fx-background-color: transparent;");  
        button.setOnAction(e ->  
        {  
            // Handle item selection  
            selectedItemName = item.getName();  
            selectedItemImagePath = item.getImagePath();  
            Image cursorImage = loadImage(selectedItemImagePath);  
            if(cursorImage != null)  
            {  
                selectedCursor = new ImageCursor(cursorImage, cursorImage.getWidth() / 2,  
                        cursorImage.getHeight() / 2);  
                primaryStage.getScene().setCursor(selectedCursor);  
            }  
        });  
        return button;  
    }  
  
    /**  
     * Reset the cursor and clear the selected item.     */    private void resetCursor()  
    {  
        selectedItemName = null;  
        selectedItemImagePath = null;  
        selectedCursor = null;  
        primaryStage.getScene().setCursor(Cursor.DEFAULT);  
    }  
  
    /**  
     * Load an image from the given path.     *     * @param imagePath Relative path to the image (e.g., "images/wood_planks.png")  
     * @return Image object or null if loading fails  
     */    private Image loadImage(String imagePath)  
    {  
        try  
        {  
            File file = new File(imagePath);  
            if(file.exists())  
            {  
                return new Image(file.toURI().toString());  
            } else  
            {  
                System.err.println("Image not found: " + imagePath);  
                return null;  
            }  
        } catch(Exception e)  
        {  
            System.err.println("Error loading image: " + imagePath);  
            e.printStackTrace();  
            return null;  
        }  
    }  
  
    @Override  
    public void start()  
    {  
        // Launch the JavaFX application  
        Application.launch();  
    }  
  
    /**  
     * Display feedback to the player using the feedback label.     *     * @param isSuccess      True if success, False if failure  
     * @param isFirstFailure True if it's the first failure, allowing retry  
     */    /**     * Display feedback to the player using the feedback label.     *     * @param isSuccess      True if success, False if failure  
     * @param isFirstFailure True if it's the first failure, allowing retry  
     */    public void displayFeedback(boolean isSuccess, boolean isFirstFailure)  
    {  
        Platform.runLater(() ->  
        {  
            if(isSuccess)  
            {  
                // 合成成功，用绿色字体显示提示  
                feedbackLabel.setStyle("-fx-text-fill: green;");  
                feedbackLabel.setText("合成成功!");  
                // 短暂延迟后跳到下一题  
                PauseTransition pause = new PauseTransition(Duration.seconds(1));  
                pause.setOnFinished(event ->  
                {  
                    feedbackLabel.setText("");  
                    gameController.nextQuestion();  
                    updateUI();  
                });  
                pause.play();  
            } else  
            {  
                // 合成失败，用红色字体显示提示  
                feedbackLabel.setStyle("-fx-text-fill: red;");  
                if(isFirstFailure)  
                {  
                    feedbackLabel.setText("合成失败,请重试!");  
                } else  
                {  
                    // 第二次失败，显示提示并跳到下一题  
                    feedbackLabel.setText("合成失败!");  
                    PauseTransition pause = new PauseTransition(Duration.seconds(1));  
                    pause.setOnFinished(event ->  
                    {  
                        feedbackLabel.setText("");  
                        gameController.nextQuestion();  
                        updateUI();  
                    });  
                    pause.play();  
                }  
            }  
        });  
    }  
  
    /**  
     * Reset the crafting grid after a retry.     */    public void resetCraftingGrid()  
    {  
        // Clear all cells in the crafting grid  
        for(javafx.scene.Node node : craftingGrid.getChildren())  
        {  
            if(node instanceof StackPane)  
            {  
                StackPane cell = (StackPane) node;  
                cell.getChildren().clear();  
            }  
        }  
    }  
  
    /**  
     * Ask the player if they want to play again.     */    public void askToPlayAgain()  
    {  
        Platform.runLater(() ->  
        {  
            Alert alert = new Alert(Alert.AlertType.CONFIRMATION);  
            alert.setTitle("游戏结束");  
            alert.setHeaderText(null);  
            alert.setContentText("是否继续游戏？");  
            ButtonType yesButton = new ButtonType("是");  
            ButtonType noButton = new ButtonType("否");  
            alert.getButtonTypes().setAll(yesButton, noButton);  
            alert.showAndWait().ifPresent(type ->  
            {  
                if(type == yesButton)  
                {  
                    gameController.startGame();  
                    updateUI();  
                } else  
                {  
                    // Exit the game or return to main menu  
                    primaryStage.close();  
                }  
            });  
        });  
    }  
  
    /**  
     * Entry point when running the MinecraftItem game separately.     *     * @param args Command-line arguments  
     */    public static void main(String[] args)  
    {  
        MinecraftItem game = new MinecraftItem();  
        game.start();  
    }  
}

// Recipe.java  
  
import java.util.HashMap;  
import java.util.Map;  
  
/**  
 * Represents a crafting recipe. Stores the required materials and their positions. */public class Recipe {  
    // Map of positions to item names  
    private Map<Position, String> recipeMap;  
  
    public Recipe()  
    {  
        recipeMap = new HashMap<>();  
    }  
  
    /**  
     * Add an item to the recipe at a specific position.     *     * @param x        X-coordinate (-1, 0, 1)  
     * @param y        Y-coordinate (-1, 0, 1)  
     * @param itemName Name of the material item  
     */    public void addItem(int x, int y, String itemName)  
    {  
        recipeMap.put(new Position(x, y), itemName);  
    }  
  
    /**  
     * Get the recipe map.     *     * @return Map of Position to item names  
     */    public Map<Position, String> getRecipeMap()  
    {  
        return recipeMap;  
    }  
  
    /**  
     * Inner class representing a position on the crafting grid.     */    public static class Position {  
        private final int x;  
        private final int y;  
  
        public Position(int x, int y)  
        {  
            if(x < -1 || x > 1 || y < -1 || y > 1)  
            {  
                throw new IllegalArgumentException("Position out of bounds.");  
            }  
            this.x = x;  
            this.y = y;  
        }  
  
        /**  
         * Get the X-coordinate.         *         * @return X-coordinate  
         */        public int getX()  
        {  
            return x;  
        }  
  
        /**  
         * Get the Y-coordinate.         *         * @return Y-coordinate  
         */        public int getY()  
        {  
            return y;  
        }  
  
        @Override  
        public boolean equals(Object obj)  
        {  
            if(this == obj)  
            {  
                return true;  
            }  
            if(!(obj instanceof Position))  
            {  
                return false;  
            }  
            Position pos = (Position) obj;  
            return this.x == pos.x && this.y == pos.y;  
        }  
  
        @Override  
        public int hashCode()  
        {  
            return x * 31 + y;  
        }  
    }  
}
```


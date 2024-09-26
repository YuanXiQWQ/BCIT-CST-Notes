```java
/**  
 * Java笔记  
 *  
 * @author YuanXi  
 * @version 2024.1.30  
 */package note;  
  
import java.util.Scanner;  
  
public class Note {  
  
  
    /**  
     * 创建检查质数的方法,该方法为isPrime();  
     *     * @param checkPrime 检查质数  
     */  
    static boolean isPrime(int checkPrime) {  
        //首先排除不符合质数最基本定义(大于1的自然数)的数  
        if (checkPrime <= 1) {  
            //根据质数的定义:"一个大于1的自然数，除了1和它自身外，不能被其他自然数整除的数叫做质数",首先排除小于等于1的整数(变量checkPrime已经由int规定了为整数,因此无需特意排除非整数)  
            return false;  
            //输入值小于等于1,不是质数该方法返回false  
        }  
  
        //然后开始对符合最基本定义的数检查  
        for (int isFactors = 2;                         //创建一个尝试数,从2开始对待检数进行整除测试  
             isFactors < checkPrime;                    //重复检查直到尝试数大于等于待检数(大于:一个数无法被比他大的数整除;等于:质数定义因数需要是除了1和它自身外的数)  
             isFactors++)                               //如果本次循环中尝试数不是因数则增量  
        {  
            if (checkPrime % isFactors == 0) {          //因数定义:若a是b的因数，那么a除以b的余数一定为0  
                return false;                           //被整除,不是质数,该方法返回false  
            }  
        }  
        return true;                                    //满足定义,是质数,该方法返回true  
    }  
  
  
    /**  
     * 开始执行bugs  
     *     * @param args arguments  
     */    public static void main(String[] args) {  
        //该字段是必须的,每个Java程序中都有  
  
        System.out.println("Hello Java!");  
        //与C++一样,文本内容需要使用双引号;不同的是,Java区分大小写!!!  
        System.out.println(114514);  
        //数字就不需要双引号  
        System.out.println(1 + 2 * 3);  
        //可以进行数字计算  
  
        /*与C++一样,Java有双斜杠和斜杠星号两种注释,且功能相同。但是Java还有另一种注释快,单斜杠开头,双星号紧跟,结尾同注释块结尾*/  
  
        //**变量  
        /*变量标识符命名规则：  
           开头:a-z(推荐),A-Z,$,_  
           内容:a-z,A-Z,$,_  
           不能包含空格和保留字(如 int,boolean)        */        String UserName;  
        UserName = "MUTT";  
  
        /*使用逗号可以一次性声明多个变量；使用等于号可以使多个变量对应一个值*/  
        int x = 5, y = 6, z = 7;  
        System.out.println(x + y + z);  
        x = y = z = 10;  
        System.out.println(UserName);  
        System.out.println(x + y + z);  
            /*  
              String:  文本变量(Java区分大小写！！！)字符串需要引号括起来  
              int:     整数  
              float:   浮点数  
              char:    单个字符  
              boolean: 布尔值(Java是boolean,C++是bool)  
            */        /*常量:final + 变量名*/  
        final String MUTTName = "MUTT";  
  
        //**数据类型:  
        /*原始数据型  
          包含byte, short, int, long, float, double, boolean和char*/  
            /*这其中又包含两组:  
                整数类型:byte, short, int和long,用于存储整数(正数或者负数)  
                浮点类型:float和double*/  
        /*非原始数据类型  
          String等*/  
  
        //整数类型:  
        /*byte: 可以存储-128到127的整数,在这之间的整数可以用byte代替int或者其他整数类型来节省内存*/  
        /*short:可以存储从-32768到32767的整数*/  
        /*int:  可以存储从-2147483648到2147483647的整数,一般首选*/  
        /*long: 可以存储从-9223372036854775808到9223372036854775807的整数,用来弥补int到达不到的值，但是必须加如下前缀:*/  
        long longNum = Long.parseLong("1145141919816");  
  
        System.out.println(longNum);  
  
        //浮点类型:  
        /*float:精度只有6-7位小数,应以f结尾*/  
        float floatNum = 3.1415926535897932384626f;  
        /*double:精度约15位,应以d结尾*/  
        double doubleNum = 3.1415926535897932384626d;  
  
        System.out.println(floatNum);  
        System.out.println(doubleNum);  
        /*运行时观察显示区别*/  
  
        //科学数字e  
        /*使用e来表示10的幂次,显示出来也将是科学计数法*/  
        final double PlunkC = 6.62607015E-34d;  
  
        System.out.println(PlunkC);  
  
        //**非原始数据类型  
            /*非原始类型的例子包括字符串、数组、类、接口等等。  
              原始类型是Java中预定义的，非原始数据类型由程序员创建，不由Java定义(String)  
              非原始类型可以用于调用方法执行特定操作，而原始类型则不能。  
              原始类型始终具有一个值，而非原始类型可以为空。              原始类型以小写字母开头，而非原始类型以大写字母开头。  
            */  
        //**Java类型转换  
        /*自动转换:当将较小的类型传递给较大的类型时，会自动进行扩展转换*/  
        int changedInt = 9;  
        double changeToDouble = changedInt;  // Automatic casting: int to double  
  
        System.out.println(changedInt);      // 输出 9        System.out.println(changeToDouble);  // 输出 9.0  
        /*手动转换:通过在值前面加上括号来手动完成数据类型转换*/  
        changeToDouble = 10.78;  
        changedInt = (int) changeToDouble;  
  
        System.out.println(changeToDouble);  //输出10.78  
        System.out.println(changedInt);      //输出10  
        //**Java运算符  
        //算术运算符  
            /*跟C++一样，有  
              + 加  
              - 减  
              * 乘  
              / 除  
              % 取余数(15 % 7 = 1, 15 / 7 = 2)  
              ++增量  
              --减量  
            */  
        //赋值运算符  
            /*跟C++差不多？  
              x+=3等同于x = x + 3  
              x-=3等同于x = x - 3  
              以此类推，有  
              =              +=              -=              *=              /=              %=              &=              |=              ^=              >>=              <<=            */  
        //比较运算符  
            /*同C++  
              用于比较两个值或者变量并返回boolean值*/  
        Scanner compareInt = new Scanner(System.in);   //Scanner类从标准输入(通常是键盘)获取输入,但是必须先导入  
        System.out.println("比较大小\n请输入一个整数值,范围是-2147483648到2147483647(int范围)");  
        x = compareInt.nextInt();  
        System.out.println("请输入另一个整数值(int范围)");  
        y = compareInt.nextInt();  
        //将用户输入的整数分别赋值于x,y  
  
        boolean isXgtY = x > y;  
        boolean isXeqY = x == y;  
        //对x,y进行比较  
  
        String xString = String.valueOf(x);  
        String yString = String.valueOf(y);  
        //将x,y值转换为String值xString和yString，便于稍后返回的展示  
  
        if (!isXgtY && !isXeqY) {  
            System.out.println(xString + "小于" + yString + "。");  
        } else if (isXgtY) {  
            System.out.println(xString + "大于" + yString + "。");  
        } else {  
            System.out.println(xString + "等于" + yString + "。");  
        }  
        //展示结果  
  
  
        //这一段也可以使用Math.max(x,y)和Math.min(x,y)实现  
  
        //逻辑运算符  
        /*和C++一样  
          && 与  
          || 或  
          !  非  
        */  
        //**字符串(类)  
        /*字符串String用于存储文本,包含由双括号括起来的字符集合*/  
  
        //字符串(方法)  
  
        /*字符串长度:  
           变量名.length() 方法找到字符串的长度  
        */        System.out.println("MUTT的昵称总共" + MUTTName.length() + "个字");  
  
        /*字符串大小写:  
           变量名.toUpperCase() 将字符全部变为大写  
           变量名.toLowerCase() 将字母全部变为小写  
        */        String doNotGoGentle = """  
                        Do not go gentle into that good night,                        Old age should burn and rave at close of day;                        Rage, rage against the dying of the light.  
                        Though wise men at their end know dark is right,                        Because their words had forked no lightning they                        Do not go gentle into that good night.  
                        Good men, the last wave by, crying how bright                        Their frail deeds might have danced in a green bay,                        Rage, rage against the dying of the light.                """;  
  
        String intoThatGoodNight = """  
  
                        Wild men who caught and sang the sun in flight,                        And learn, too late, they grieved it on its way,                        Do not go gentle into that good night.  
                        Grave men, near death, who see with blinding sight                        Blind eyes could blaze like meteors and be gay,                        Rage, rage against the dying of the light.  
                        And you, my father, there on the sad height,                        Curse, bless, me now with your fierce tears, I pray.                        Do not go gentle into that good night.                        Rage, rage against the dying of the light.                """;  
  
        System.out.println(doNotGoGentle.toUpperCase());  
        System.out.println(intoThatGoodNight.toLowerCase());  
  
        /*字符串中查找  
          变量名.indexOf()返回字符串中指定文本的第一次出现的位置(第一个位置为0)  
        */        System.out.println("第一次Rage出现在第" + doNotGoGentle.indexOf("Rage") + "个词");  
  
        /*字符串连接*/  
        /* 变量名 + 变量名 连接两个变量*/  
  
        String poem = doNotGoGentle + intoThatGoodNight;  
        System.out.println(poem);  
  
        /* 变量名.contact(另一个变量名) 连接两个变量*/  
        poem = doNotGoGentle.concat(intoThatGoodNight);  
        System.out.println(poem);  
  
        //**特殊字符  
  
        /* \保留符号 来避免编译器混淆*/  
        poem = "\"Do not go gentle into that good night\"";  
        System.out.println(poem);  
  
        /*其它转义符  
        \' 插入单引号  
        \" 插入双引号  
        \\ 插入反斜杠  
        \n 插入新行(New line)  
        \r 插入回车（Return)  
        \t 插入TAB  
        \b 插入回退(Backspace)  
        \f 插入换页(Form feed)  
        */  
        //**数学(类)  
  
        /*部分数学方法  
           Math.max(x,y) 找到x和y的最大值  
           Math.min(x,y) 找到x和y的最小值  
           Math.sqrt(x)  返回x的平方根  
           Math.abs(x)   返回x的绝对值  
           Math.random() 返回0.0(含)至1.0(不含)之间的随机数  
        */  
        /*Math.random()的范围控制*/  
        int randomNum = (int) (Math.random() * 101); //输出0到100之间的整数,原理是先输出该方法本身随机出的小数，然后乘以101倍,之后转换为int取整数  
        System.out.println(randomNum);  
  
        //**Boolean(类)  
        /*          用于存储true或false值。和C++一样，也可以通过使用  
          (变量 运算符 变量) 来返回bool值  
        */        x = (int) (Math.random() * 51);  
        System.out.println("\"x\"的值为" + x);//随机并展示x的值  
  
        y = (int) (Math.random() * 51);  
        System.out.println("\"y\"的值为" + y);//随机并展示y的值  
  
        System.out.println("\"x\"比\"y\"大的命题为:" + (x > y));//判断命题真假  
  
        //**if, else  
        /*基本语句: 同C++ */  
        x = (int) (Math.random() * 4);  
  
        if (x == 0) {  
            System.out.println("x等于0");  
        } else if (x == 1) {  
            System.out.println("x等于1");  
        } else {  
            System.out.println("x等于2");  
        }  
  
        /*三元运算符: 同C++ */  
        System.out.println(((int) (Math.random() * 2) == 1) ? "x等于1" : "x不等于1");  
  
        //**Switch  
        /*避免写一大堆else if。同C++:*/  
        x = (int) (Math.random() * 4);      //给x赋值0-3的随机整数  
  
        switch (x) {  
            case 0:                         //判断 x==0 是否为真  
                System.out.println("x等于0");  
                break;  
            case 1:                         //判断 x==1 是否为真  
                System.out.println("x等于1");  
                break;  
            default:                        //判断x!=0 && x!=1 是否为真  
                System.out.println("x等于2");  
                break;  
        }  
  
  
        //**循环  
        /*while循环:同C++,先检查是否满足条件,满足再执行*/  
        x = (int) (Math.random() * 4);      //给x赋值0-3的随机整数  
  
        while (x != 10) {                   //检查条件"x不等于10"真假,若为真,开始/再次执行;若为假,跳出循环  
            System.out.println(x);          //输出x的数值  
            x++;                            //x数值+1  
        }                                   //回到检查  
  
        /*do while循环:同C++,先执行,再检查是否满足条件,满足再进行下一次执行*/  
        x = (int) (Math.random() * 4);  //给x赋值0-3的随机整数  
  
        do {                                //开始执行  
            System.out.println(x);          //输出x的数值  
            x++;                            //x数值+1  
        } while (x < 10);                     //检查条件"x<10"真假,若为真,再次执行;若为假,跳出循环  
  
        /*for循环:同C++,差不多是while的简写形式,常用在确切知道循环次数的时候*/  
        for (x = (int) (Math.random() * 4); //循环之前执行一次  
             x < 10;                        //判断条件"x<10"真假,若为真,开始/再次执行代码块;若为假,跳出循环  
             x++) {                         //代码块执行结束后执行一次,x数值+1  
            System.out.println(x);          //输出x的数值  
        }  
  
        /*break中断: 用于跳出循环*/  
        System.out.println("下面的列表会一直显示偶数直到遇到奇数");  
        int i = 1;                          //给i赋值1  
        do {                                //先显示1,所以使用do-while  
            if (i % 2 == 0) {               //条件:i/2的余数为0(判断i是否为偶数)  
                break;                      //i为偶数的时候跳出循环  
            }                               //不满足条件继续  
            System.out.println(i);          //输出i的值  
            x = (int) (Math.random() * 4);  //给x赋值0-3的随机整数  
            i += x;                         //x数值+0-3的随机数  
        } while (i < 50);                   //条件:i小于50  
        //循环执行显示i并i+1,当i=5时跳出循环  
  
        /*continue继续:当满足条件时,立刻终止当前循环体并进行下一次循环*/  
        System.out.println("下面的函数将会显示1-20中的所有偶数");  
        i = 1;                              //赋值i=0  
        do {                                //先执行  
            i++;                            //i自增  
            if (i % 2 == 1) {               //如果i是奇数  
                continue;                   //跳过下面的循环块并重新开始循环  
            }  
            System.out.println(i);          //输出i的值  
        } while (i < 21);  
  
        //这段代码使用for循环重构  
        System.out.println("下面的函数将会显示21-40中的所有偶数");  
        for (i = 21;                        //初始化  
             i < 41;                        //满足条件时执行  
             i++) {                         //代码块执行结束后执行一次,x数值+1  
            if (i % 2 == 1) {               //如果i是奇数  
                continue;                   //跳过下面的循环块并重新开始循环  
            }  
            System.out.println(i);          //输出x的数值  
        }  
  
  
        //**数组(类)  
        /*用于在单个变量中存储多个值*/  
        String[] class3Zoo = {"MUTT", "Bird", "Turtle", "Others"};  
  
        /*访问数组元素:编程语言从0开始数数!!!!!!!!!!!!!!!!!!!!!!!!*/  
        System.out.println("三班动物园的第一个是" + class3Zoo[0]);  //输出第一个元素  
  
        /*更改特定的值*/  
        class3Zoo[3] = "Bear";  
  
        /*访问数组长度  
          数组名.length 来访问数组长度  
        */        System.out.println(class3Zoo.length);  //输出数组长度  
  
        /*循环遍历数组*/  
        /*使用for循环并使用length属性指定循环运行的次数*/  
        System.out.println("下面是三班动物园中的所有动物");  
        for (i = 0;                             //初始化i  
             i < class3Zoo.length;              //循环条件:i小于数组长度(没遍历完)  
             i++) {                             //i自增  
            System.out.println(class3Zoo[i]);   //输出  
        }  
  
        /*for-each循环遍历数组*/  
        /*        for (用来展示数组内容的临时变量 : 数组名称) {  
            System.out.println(用来展示数组内容的临时变量);s  
        }        */        System.out.println("下面还5" + "是三班动物园中的所有动物");  
        for (String animal : class3Zoo) {  
            System.out.println(animal);  
        }  
  
        /*多维数组*/  
        /*数组的数组*/  
        int[][] multiDimensionalArrays = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};  
  
        /*更改,访问,循环遍历多维数组:报坐标*/  
        multiDimensionalArrays[2][0] = 10;                  //更改第三个数组里的第一个数  
        System.out.println(multiDimensionalArrays[2][0]);   //输出第三个数组里的第一个数  
  
        for (i = 0; i < multiDimensionalArrays.length; i++) {  
            //初始化我们的老替身i,循环条件设置为i小于多维数组的总长度,每次循环i自增  
            for (x = 0; x < multiDimensionalArrays[i].length; x++) {  
                //初始化我们的老替身x,循环条件设置为x小于多维数组内部数组的长度,每次循环x自增  
                System.out.println(multiDimensionalArrays[i][x]);  
                //输出元素坐标所对应的内容  
            }  
        }  
  
        //**Java方法  
        /*  
        一段只有调用时才会运行的代码块,需要定义  
        必须在类(Class)内声明  
        * */  
        /*预定义方法  
          System.out.println()          是Java的预定义方法的一种  
        */  
        /*自定义方法  
          例:在Main内创建一个方法  
          public class note.Note {            方法类别 返回值 方法名称() {  
                该方法要执行的代码  
          }  
             static void methodA() {                 System.out.println("Hello World");             }             static 表示该方法属于Main类而非Main类的对象  
             void   表示该方法没有返回值  
        */  
        /*方法调用:在Main内输入  
          方法名称();  
          调用方法  
        */  
        /*方法参数:在方法内部充当变量,记得声明变量类型  
        public class note.Note {            static void greeting(String firstname,String lastname) {                System.out.println("Hello," +firstname +  lastname);  
            }  
            static void nameAndAge(String name, int age) {                System.out.println(name + "is" + age + "years old");            }            以上为自定义方法  
  
            }            public static void main(String[] args) {                greeting("Jiarui", "Xing");                greeting("Jiajun", "Feng");                greeting("Jack", "Le");                nameAndAge("Jiarui", 19);                nameAndAge("Jiajun", 20);                nameAndAge("Jack", 21);            }            以上为主方法(程序开始执行)  
        }        将会输出:  
        Hello, Jiarui Xing        Hello, Jiajun Feng        Hello, Jack Le        Jiarui is 19 years old        Jiajun is 20 years old        Jack is 21 years old        (乱填的)  
        */  
        /*方法返回值:  
          void 表示该方法不返回值,如果希望返回值,可以使用原始数据类型(包含byte, short, int, long, float, double, boolean和char)代替void,并在方法内部使用return关键字  
  
          public class note.Note {            static int add(int alpha, int beta) {                return alpha + beta;            }            public static void main(String[] args) {                System.out.println(add(5, 8));            }          }          将输出 13 (5 + 8)        */  
        /*方法实战示例:寻找范围内的质数,方法已在程序前声明*/  
        int rangeStart;  
        int rangeEnd;  
        Scanner range = new Scanner(System.in);     //初始化检测器,命名为inputRange  
        System.out.println("查找质数,如果只需要查询一个数,两次输入相等即可.请输入一个范围:\n从");  
        rangeStart = range.nextInt();  
        System.out.println("到");  
        rangeEnd = range.nextInt();  
  
        //检查输入的范围反没反  
        if (rangeStart > rangeEnd) {                //运行条件:开始值大于结束值  
            int temp = rangeStart;                  //创建媒介变量并继承rangeStart的值  
            rangeStart = rangeEnd;                  //将rangeStart的值变成rangeEnd的值  
            rangeEnd = temp;                        //将继承自最初rangeStart的值还原至rangeEnd  
        }  
  
        //初始化  
        int totalNum = rangeEnd - rangeStart + 1;   //计算范围内总共多少个数  
        int totalPrime;                             //建立质数总数的计数变量  
        int[] primesForAll = new int[totalNum];     //建立并初始化能装得下范围内所有数的质数数组  
  
        //开始筛选质数  
        for (i = rangeStart, totalPrime = 0; i <= rangeEnd; i++) {  //初始化替身i和两个计数器,遍历范围内的数  
            if (isPrime(i)) {                       //当isPrime()方法返回true时  
                primesForAll[totalPrime] = i;       //将检测到的质数储存在能装得下范围内所有数的质数数组中,使用totalPrime作为数组坐标节省了一个定位坐标的变量  
                totalPrime++;                       //质数总数+1  
            }  
        }  
  
        //整理能装得下范围内所有数的质数数组  
        i = 0;                                      //再次初始化替身i  
        int[] primes = new int[totalPrime];         //建立并初始化质数数组  
        for (int prime : primesForAll) {            //遍历能装得下范围内所有数的质数数组  
            if (prime == 0) {  
                continue;  
            }  
            primes[i] = prime;  
            i++;  
        }  
  
        //总结并输出  
        if (totalPrime == 0) {                      //如果没有质数  
            System.out.println("没有符合条件的质数");  
        } else {                                    //如果有质数  
            System.out.println("共检查了" + totalNum + "个数，其中下列" + totalPrime + "个数是质数");  
            for (int prime : primes) {  
                System.out.println(prime);  
            }  
        }  
  
        /*我真棒,哎呀*/  
  
        //**方法重载  
        /*当方法的执行方式相同,但是参数类型不同时(如int和double),可以通过方法重载保留方法执行方式但改变其参数类型  
        构成条件:  
            {形参类型不同 || 形参个数不同 || 形参顺序不同}  
            返回值不同 不会 构成方法重载  
            详见 Overload 类  
        */  
        //**方法范围  
        /*  
        变量只能在创建的区域内使用,称之为范围.  
        直接在方法中声明的变量在方法中声明它们的代码行后面的任何位置都可用:  
        例:  public class note.Note {  
            public static void main(String[] args) {                int x = 5;          //这里面的x变量就可以在main方法中的任何位置使用  
                System.out.println(x);            }            x = 10;                 //这里面的x变量就不会被识别,因为在该代码块中变量未声明  
        }        */  
        //**递归  
        /*  
        用来调用函数本身,提供了将复杂问题分解为简单问题的方法  
        通常占用较多内存,尽量使用循环代替  
        例:详见文件Recursion  
        */  
        //**类(Class)与对象(Object)  
        /*        类是用来创建对象的模板，对象是类的实例  
  
        例:   Class类:水果  
             Object对象:苹果 香蕉 芒果  
             Attribute属性:甜度 重量 颜色  
             Method方法:吃 玩 看  
  
  
             Class类: 车  
             Object对象: 沃尔沃 奥迪 丰田  
             Attribute属性: 车牌号 车型 车颜色  
             Method方法: 前进 后退 刹车  
  
        同样,当创建个体对象时,对象继承类中所有变量和方法  
        */        /*详见 JavaOOP 类*/  
  
        /*类属性  
        详见 ClassMethods 类  
        */  
        //**修饰符  
        /*访问修饰符(Access Modifier):控制访问级别  
          对于类Class  
            public:任何其他类都可以访问这个类  
            default:只能由同一个包(package)的类访问  
  
          对于属性,方法和构造函数Attributes,Methods and Constructors  
            public:代码可以被所有类访问  
            protected:代码可以在同一个包和不同包的子类中访问。  
            default:代码只能在同一个包中访问。当没有指定修饰符时使用。  
            private:代码只能在声明的类中访问  
  
            修饰符/访问场景    同一类内部   同一包内所有类   不同包的子类   不同包的非子类   同一包的非子类  
            public         √           √             √            √             √              protected      √           √             √            ×             √              default        √           √             ×            ×             √              private        √            ×             ×            ×             ×        */  
        /*非访问修饰符  
          对于类Class  
            final:这个类不能被其他类继承  
            abstract:类不能用于创建对象  
  
          对于属性,方法和构造函数Attributes,Methods and Constructors  
            final:属性和方法不能被覆盖/修改  
            static:属性和方法属于类，而不是对象  
            abstract:只能在抽象类中使用，并且只能在方法上使用。该方法没有主体，例如abstract void run();主体由子类提供  
            transient:在序列化包含属性和方法的对象时将跳过它们  
            synchronized:方法一次只能由一个线程访问  
            volatile:属性的值不会在线程本地缓存，而总是从“主内存”中读取。  
        */  
        /*各修饰符作用  
          final:如果不希望能够覆盖现有属性值,可以声明属性为 final          static:static 方法意味着可以在不创建类的对象的情况下访问  
          abstract:没有具体实现。具体实现由子类提供  
        */  
        //**封装  
        /*确保敏感数据对用户隐藏:  
            声明类变量/类属性为 private            提供公共的 getter 和 setter 方法来访问和更新一个变量的值  
        */  
        /*获取(get)和设置(set):  
            private 变量只能在同一个类中访问,但是当使用 getter 和 setter 方法时可以从外部类访问  
            getter:返回变量的值  
            setter:修改变量的值  
            用于在外部类中访问 "private" 修饰的变量的值  
                使用方法: get变量名(首字母大写)  
                         set变量名(首字母大写)  
          详见 PrivateExample 类  
          可以有效保护某一类的内部状态,防止被外部代码直接修改导致无效或不一致;也提供了一种灵活的方式来检查和处理对 MUTT 的任何更改状态  
        */  
        /*封装的好处  
          1. 更好地控制类属性和方法  
          2. 类属性可以设置为只读(就是只使用 getter 方法)或者只写(就是只使用 setter 方法)  
          3. 更灵活,可以更改代码的一部分而不影响其它部分  
          4. 数据安全性提高,可以有效保护某一类的内部状态  
        */  
        //**包(packages)  
        /*包  
          用于将相关的类分组(就像这个笔记项目(project)正在做的一样),相当于文件目录中的文件夹(为什么不直接使用文件夹这类称呼,搞得神乎其神的)  
          避免名称冲突  
          使代码更易于维护  
        */  
        /*包分为  
           内置包 (Built-in Packages),来自Java API的包  
           自定义包 (User-defined Packages), 自己创建的包  
        */  
        /*内置包  
          是 Java 开发环境中包含的一组预先编写的类库(library)  
            包含用于管理输入,数据库编程等等的组建  
            库(library)被分为包和类,这意味着可以导入单个类,或者导入包含属于指定包的所有类的整个包  
            使用 import 关键词来导入库中的类或包  
            import package.name.Class;   //导入包的一个类: import 关键词, package.name包名, Class类名  
            import package.name.*;       //导入包的所有类  
  
          导入一个类  
            import java.util.Scanner;   //java.util是一个包,Scanner是这个包的一个类  
  
          导入一个包  
            import java.util.*        */  
        /*自定义包  
            使用 package 关键词创建包(IDEA可以用重构自动创建)  
        */  
        //**继承  
        /*Java可以从类中继承属性和方法.包含两个概念:  
            子类(subclass): 继承自另一个类的类  
            超类/父类(superclass):被继承的类  
          创建类时,在子类类名后加注 extends 关键词和父类类名来继承一个类  
          class A {            public void Method() {              ...            }          }  
          class B extends A {            public static void main(String[] args) {                B bObject = new B();                bObject.Method();            }          }          子类中的B方法仍会执行.详见 Inheritance 类  
        */        /*如果不希望其它类继承一个类,在这个类 class 前加注 final          final class A {            ...          }          class B extends A {            ...          }          将会返回 错误  
        */        compareInt.close();  
        range.close();  
  
        //**类  
        /*  定义方式:class  
            成员:属性field  
                方法Method  
                构造器Constructor  
              属性:表示静态数据  
              方法:表示动态行为  
        */        //属性:  
        /* 用于定义该类或该类对象包含的数据(或者说静态特征)  
            作用范围是整个类体  
            定义成员变量时可以对其进行初始化;如果不初始化,Java会使用默认值进行初始化:  
            数据类型         默认值  
            整型int           0  
            浮点型float       0.0  
            字符型char     '\u0000'  
            布尔型boolean    false  
            字符串String     *String属于引用类型,不属于基本类型  
            引用类型          null        */        //方法:  
        /*  用于定义该类或该类示例的行为特征和功能实现  
            是类和对象行为特征的抽象            从属于类和对象            面向对象中,整个程序的基本单位是类  
        */  
        //**垃圾回收机制  
        //判断为垃圾的方法:  
        /*            1. 引用计数: 当对象的引用数为0时,则删除,但是无法删除互相引用的对象  
            2. 分代垃圾回收机制:  
                对象分为三种状态:年轻代,年老代,持久代. JVM将堆内存分别划分为 Eden, Survivor和 Tenured/Old 空间.  
                    年轻代:  
                    新生成对象首先放入Eden区. 当年轻代区域存放满对象后,就将对象存放到年老代区域.  
                    年老代:  
                    在年轻代中经历了N(默认15)次垃圾回收后仍然存活的对象,就将对象放入年老代区域  
                    永久代:  
                    用来存放静态文件,如Java类.垃圾回收对永久代没有显著影响.JDK8以后就没有永久代了,而是使用 meetaspace                    元数据空间和对替代.  
            3. 垃圾回收器:  
                Minor GC:                用于清理年轻代. Eden 区域满了就会触发一次 Minor GC, 清理无用对象,并将有用对象复制到 Survivor1,                Survivor2 中.  
                Major GC:                用于清理年老代. 用于清理年老代  
                Full GC:                用于清理年轻代,年老代啊区域,成本较高,会对系统性能产生影响.  
         */    }  
}
```
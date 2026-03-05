# Block 1-4 单词表和习题集
compile 编译
encapsulation 封装
implementation/implement 执行
the method signature 方法签名
superclass/subclass 父类/子类
default 默认
invoke 调用
be preceded with 在……之前
appropriate 合适的
utilize 利用
inheritance 继承
convention 惯例
sensible 合理的
# 1 Java 程序的运行流程
Java 支持一次编写到处运行。Java 程序从编写到运行经历如下步骤：
1. 编写源代码，可以使用你喜欢的任意编辑器。
2. 通过指令 javac 将代码编译成字节码（xxx.class）（而非直接的可执行文件）3.通过指令 java 运行该字节码。会先检查这段字节码的所有字节是否合法，是否违反 java 安全限制，随后通过解释器在对应平台上的 Java 虚拟机（JVM，Java Virtual Machine）上执行该程序。
对于程序 MyProgram.java，应当先运行 javac MyProgram.java，随后运行 java MyProgram（注意没有.class），就可以运行程序了。
![image1 3|image1 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%203.png)
# 2 一段基础的Java 代码
```Java
public class HelloWorld {
public static void main(String[] args) {
System.out.println("Hello world!");
	}
}
```
这是一段基础的Java 代码
类定义(class declaration) public class HelloWorld: Java 对面向对象的崇拜已经到了痴狂的地步，所以每个程序的最根部应该是一个类，如果该类为 public，则要求该代码的文件名必须等于类名。例如此文件应当为 MyProgram.java。
public static void main(String[] args):
我们一行一行看：
public：是指访问限制。public 说明该方法全局可访问。
static：表示静态方法。即该方法为单例，与类相关，而非与对象相关。后面面向对象会讲。
void：表示返回值类型。void 表示没有返回值。
main：方法名。名为 main 的方法会被系统当作程序入口，和 C 类似。 String[] args：指通过命令行传入的其他参数。详见 Lab 1.
System.out.println("Hello world!"):这个东西类似 C 语言的 printf。ln 表示打印完了会带一个换行。
# 3 Java 编程基础
## 3.1 变量
Java 的变量可以在程序中的任何位置声明。变量声明方法与 C 语言类似。
`typeName name1, name2, ... namen;`
`typeName name1 = initvalue;`
## 3.2 数据类型
Java 是强类型语言。意思是你声明变量时就需要指定该变量的数据类型。基本数据类型：
![image2 3|image2 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%203.png)
![image3 3|image3 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%203.png)
注意：0.2363 类型的数据默认当成 double，0.2363F 才是单精度浮点；86827263927 默认当作 int，86827263927L 才会当作 long。
每种数据类型在 Java 中都有一个默认值，某些时候 Java 会把变量初始化为默认值。字符串 String 不是 Java 的基本类型，而是一种对象。
### 3.2.1 类型转换
Java 变量类型可自低到高自动无损转换
`byte => short => int => long => float => double`
反向转换时需要使用强制转换声明（Type Cast）：j = (int)(x + 1.3); // j = 8
`i = (int)x + (int)1.3; // i = 7`
反向转换时，由于变量范围问题，转换结果可能会被截断或溢出。3.3 保留字
这些词语不能当作用户标识符（变量名类名方法名等等）
## 3.4 赋值和操作符
![image4 3|image4 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%203.png)
基本用法：赋值符还是 =，自增自减运算符 ++ 和 -- 也能用。
++i 和 i++ 的效果和 C 语言也还是一样的，前者自身作为表达式会返回 i+1，后者自身作为表达式会返回 i，二者都会将 i 本身的值加一。
![image5 3|image5 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%203.png)
### 3.4.1 代数操作符
![image6 3|image6 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%203.png)
加减乘除，取模余数
所有代数操作符都可以与赋值符结合在一起用。
```Java
int c = 3;
c += 7; // c = c + 7 = ?
c -= 5; // c = c - 5 = ?
c *= 6; // c = c * 6 = ?
c /= 3; // c = c / 3 = ?
c %= 3; // c = c % 3 = ?
```
### 3.4.2 条件运算符（三元运算符）
比较特殊的一种运算符。
a = (这个条件成立吗 ? 如果成立值就是我 : 否则就是我);
### 3.4.3 操作符优先级
高优先级操作符优先运算，低优先级运算符后运算。同优先级的运算符：二元操作符从左向右运算，赋值符从右向左运算。
![image7 3|image7 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%203.png)
### 3.4.4 关系运算符/逻辑运算符
和 C 语言类似。
![image8 3|image8 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%203.png)
## 3.5 控制结构
### 3.5.1 选择结构
**if、if else：**
```Java
if (这里的条件成立) {
System.out.println("passed");
}
else {
System.out.println("failed");
}
switch：switch 结构和 C 类似，需要写 break，否则会一直执行下面的东西。
char grade = 'a';
switch (grade) {
case 'a':
System.out.println("excellent");
break;
case 'b':
System.out.println("good");
break;
case 'c':
System.out.println("not bad");
break;
case 'd':
System.out.println("bad");
break;
default:
System.out.println("no such grade!");
}
```
### 3.5.2 循环结构
do while，while ：会先做那段代码块里的东西，再判断条件如何。也就是不管什么情况都会先把代码块里的东西执行一次。用法和 C 语言类似。
```Java
do {
System.out.println("i = " + i);
i++;
} while (i < 3);
// 或者
int i = 0;
while (i < 3) {
System.out.println("i = " + i);
i++;
}
for : 循环跟 C 的写法很类似
for (int i = 0; i < 3; i++) {
System.out.println(“i = ” + i);
}
```
break：退出当前循环
continue：结束当前循环轮次
Java 支持内层和外层循环标记，标记后可以在内层直接退出外层循环。通过outer inner 标记内层和外层循环，跳出（continue 或 break）时选择跳出外层循
环。如图：
## 3.6 注释
Java 的注释和 C 比较类似：
// 这是单行注释
/* 这是
多行
注释 */
长下面这样的叫 javadoc 注释。 Javadoc 这个工具能识别代码内的 Javadoc 注释，然后把他们整理成文档。
![image9 3|image9 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%203.png)
## 3.7 参数（Parameter）和实参（Argument）
**参数（Parameter）**：是方法定义时写在方法名后面括号里的变量，如 void go(int z) 里 z 就是一个参数。
**实参（Argument）**：是调用方法时传递进去的具体数值或变量，如 p.go(x); 调用时传入的 x 就是实参。
当我们在方法内部对参数（这里是 z）进行操作，比如 z = z + 7; 时，这并不会影响到外部传入的实参（这里是 x）本身。Java 是“值传递”(pass-by-value)，所以实参的值不会直接被方法内部的修改所改变。
## 3.8 修饰符
在 Java 中，修饰符（Modifiers）是用来限定类、方法、变量等成员访问权限或行为特性的关键词。简单来说，修饰符告诉编译器或其他程序员——“这个类/方法/变量能在哪里使用”、“它是不是固定的”、“是不是只能初始化一次”等。
Java 中的修饰符大致可以分为两类：
### 3.8.1 访问修饰符（Access Modifiers）
|修饰符|说明|适用范围|
|---|---|---|
|public|对所有类都可见|类、方法、变量、构造器|
|protected|对本类、同一包、子类可见|方法、变量、构造器|
|default（无修饰）|对本类和同一包内的类可见，不写就是默认（不是关键词 default）|类、方法、变量、构造器|
|private|只对本类可见|方法、变量、构造器|
### 3.8.2 非访问修饰符（Non-access Modifiers）
|修饰符|说明|使用示例|
|---|---|---|
|static|静态成员，属于类而不是对象|static int count|
|final|不能修改：- 变量：常量 – 方法：不能被重写 – 类：不能被继承|final double PI = 3.14|
|abstract|抽象类或方法，不能实例化、必须被子类实现|abstract class Shape|
|synchronized|同步方法或代码块，用于多线程控制|synchronized void run()|
|volatile|多线程中强制从内存读取变量，避免缓存问题|volatile boolean running|
|transient|不序列化字段（如写入文件或网络时忽略）|transient String password|
|native|本地方法，使用 C/C++ 编写，用 JNI 调用|native void start();|
其中：
- final 修饰符：用于限制修改或继承
|用法|示例|含义说明|
|---|---|---|
|final 变量|final int topSpeed = 100;|这个变量的值不能被修改|
|final 方法|final void stop() { ... }|子类不能重写这个方法|
|final 类|final class Square { ... }|这个类不能被继承|
- static 修饰符：用于类级别成员
|用法|示例|含义说明|
|---|---|---|
|static 变量|static int count = 0;|类变量，所有对象共享|
|static 方法|static void showCount()|类方法，可以不用创建对象就调用|
|static 代码块|static { ... }|类加载时执行一次的初始化块|
this 关键字代表当前对象，只能在非静态方法（实例方法）中使用。
**静态变量的特点（static）：**
类共享一份拷贝：所有对象共用同一个静态变量。
在类加载时初始化：早于任何对象创建。
如果没有初始化，则使用默认值（比如 int 是 0，boolean 是 false）。
和实例变量不同：实例变量属于每一个对象；静态变量属于类。
**静态常量的特点（static final）：**
不能被修改：加上 final 后就成了常量，值不允许再变。
Java 推荐将 static final 常量命名为全大写。
必须初始化，方式有两种：
初始化方式一：在声明时直接赋值
`public static final int MAX_SIZE = 100;`
初始化方式二：在 static 初始化代码块中
  
```Java
public static final int MAX_SIZE;
static {
MAX_SIZE = 100;
}
```
  
注意：不能在构造方法里初始化 static final 变量，因为它跟对象无关。
类变量示例：计数器
```Java
public class Student {
public static int count = 0; // 类变量（静态变量）
public Student() {
count++; // 每创建一个对象，count 加 1
}
public static void printCount() {
System.out.println("总共创建了 " + count + " 个学生对象"); }
}
public class Test {
public static void main(String[] args) {
Student s1 = new Student();
Student s2 = new Student();
Student s3 = new Student();
Student.printCount(); // 输出：总共创建了 3 个学生对象}
}
```
|特性|类变量（static）|实例变量（普通变量）|
|---|---|---|
|属于|类（所有对象共享）|每个对象单独拥有|
|声明方式|static 修饰|普通声明即可|
|生命周期|随类一起加载|随对象创建而产生|
|访问方式|类名.变量名 or 对象.变量名|对象.变量名|
final + static 常用于定义常量
public static final double PI = 3.14159;
static：属于类；
final：不可修改；
PI：常量名，一般用大写字母表示。
|特性|static|final|static final|
|---|---|---|---|
|特性|static|final|static final|
|---|---|---|---|
|属于谁？|类（所有实例共享）|赋值后不能修改|类共享 + 不能修改|
|可否被对象访问？|可以，但推荐用类名访问|可以|可以|
|是否可以更改值？|可以更改|不可以|不可以|
|初始化时间|类加载时|声明或构造器|声明时或 static 初始化块中|
|命名约定|通常小写开头的驼峰命名法|一般小写开头|全部大写，用下划线分隔4 面向对象基础|
# 4 面对对象基础
Java 是面向对象的编程语言，最基础的实体是类（Class）。
面向对象的设计方法将代码拆分为由类规划的对象。对象拥有自己的属性和方法。
例如，我要设计一个系统，该系统和动物、动物行为相关。现在我要设计小猫。
小猫拥有小猫的属性（Properties）：例如毛色、年龄，名字、体重等等，这些数据是和这只小猫相关的，一只小猫可以拥有这些数据作为属性。小猫拥有小猫的动作（方法（Methods））：例如叫、吃东西、跑步等等。小猫可以拥有这些东西作为函数方法，也就是这只小猫的动作。
我们通过编写一个类来定义这个对象到底拥有什么。类就像是一个饼干模具，决定了饼干长什么样子，但是类本身并不是一个饼干。一旦类编写好了，我们通过代码，基于类来创建对象（Object）。创建出的对象拥有这个类定义的全部内容。每个属性和方法现在都将属于这个对象而非类（除非声明为静态方法/属性）。
为了减少代码量，增加可维护性，类是可以进行继承的。例如，我的代码要拓展到动物，那么我定义一个类叫动物，让接下来的小猫、小狗都继承这个动物。这样，一旦后续需求变动（例如，需要为所有动物都添加“身高”的属性），那么我直接修改动物类的属性，继承了其的小猫小狗等都会拥有这个身高属性，就不需要一个一个修改这么多具体动物的类了。
面向对象更加灵活，还支持多态、重载和重写。
动物类实现了方法移动，但是狗可以跑，而兔子可以跳，这时狗和兔子就可以分别重写（Override）自己的移动方法，实现自己的逻辑。狗的跑只需要跑的距离作为参数，而兔子的跳需要跳的距离和高度两个参数，于是就可以在狗和兔子中分别重载（Overload）这个方法，使其能够接收不同的参数，返回不同的内容，抛出不同的异常等等。
![image10 3|image10 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image10%203.png)
## 4.1 实例方法和静态方法
在Java 中，实例方法（Instance methods）又称非静态方法；类方法（Class Methods）又称静态方法（static methods）。
### 4.1.1 实例方法
定义：不带 static 关键字，属于对象级别的方法，必须先创建该类的对象（实例）后才能调用。
特点：
- 可以访问类中的所有成员变量（包括实例变量和静态变量）。
- 可以调用类中的所有方法（包括实例方法和静态方法）。
- 必须通过对象来调用。
### 4.1.2 静态方法
定义：使用 static 关键字修饰，属于类级别的方法。
特点：
- 无需创建对象即可通过类名直接调用。
- 只能直接访问类中的静态成员（静态变量、静态方法）；
- 若要访问实例成员，则需要先创建对象（实例）。常用于工具类、辅助方法或与特定对象实例无关的操作。
## 4.2 实例变量和静态变量
### 4.2.1 实例变量
定义：不带 static 关键字。
特点：
- 通常代表「对象的特征/属性」。
- 只有在该对象被创建后，才具备这些属性。
- 每个对象可以有不同的属性值。
### 4.2.2 静态变量
定义：带 static 关键字。
特点：
- 常被称为「类变量」，通常用于表示与实例无关的公共数据或需要在所有实例中共享的数据。
- 适合统计或共享信息，如计数器、全局配置、缓存等。
- 对该类所有实例都是「一份」数据，任何一个实例对该静态变量的修改对其他实例都是可见的。
## 4.3 构造函数（Constructor）
在 Java 中，构造函数（Constructor）是一种特殊的方法，它主要用于创建并初始化一个类的对象。
如果一个类中没有显式定义任何构造函数，编译器会自动为我们生成一个“无参构造函数”（默认构造函数）。一旦自己显式定义了任意构造函数（哪怕只是带参数的构造函数），那么编译器就不再自动生成无参构造函数。如果你需要无参构造函数但又定义了其他构造函数，就需要显式地写出无参构造函数。
与一般方法不同，构造函数具有以下特点：
- 名称与类名相同
- 构造函数的名字必须与其所在的类的名字完全一致（包括大小写）。
- 没有返回类型
- 构造函数不声明返回类型，也不能用 void 来修饰；它不通过 return 返回任何值。
在创建对象时被自动调用
当我们通过 new 关键字创建对象时，会自动调用相应的构造函数来完成对象的初始化工作。例如：
`ClassName obj = new ClassName();`
这行代码会调用 ClassName 类中没有参数的构造函数（即默认构造函数）。
可以重载
和普通方法一样，构造函数也可以进行方法重载（Overloading）。也就是说，在同一个类中，可以有多个同名但参数列表不同的构造函数，满足不同场景的初始化需求。例如：
```Java
public class Person {
String name;
int age;
// 无参构造函数
public Person() {
this.name = "未命名";
this.age = 0;
}
// 带参数的构造函数
public Person(String name, int age) {
this.name = name;
this.age = age;
}
}
```
构造函数的作用：确保对象在创建之初就处于一个合理或有效的状态。例如，上面的 Person 类可以在对象创建时就带上姓名和年龄，或者将它们初始化为默认值。
## 4.4 访问修饰符
![image11 3|image11 3.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image11%203.png)
访问修饰符从上到下，访问权限逐渐减小，依次是：
- public：最开放，可以被任何类访问。
- protected：可以被同一包(package)中的类访问，也能被不同包中继承它的子类访问。
- 默认(default)：又称“包访问权限”，如果在声明时不加任何修饰符，则默认为default。它只允许同一个包中的其他类访问。
- private：最严格，只能在本类内部访问。
不要将所有实例变量或方法都设为 public。这会违背信息隐藏和封装的原则面向对象编程追求让对象的内部细节“藏起来”（hidden），只提供所需的“公共接口”供外部调用。
通过使用 public 或 private 等关键字来控制类内部哪些成员可以被外部访问，哪些只能内部使用。
### 4.4.1 访问器（Accessor/Getter）和修改器（Mutator/Setter）
如下面代码所示：
```Java
public class Cat {
private String name;
private String colour;
private int age;
// other code
}
Cat c = new Cat();
c.age = 5; // ERROR
```
  
如果直接修改private 属性会报错，这时候我们就需要访问器和修改器了访问器：
```Java
public String getColour() {
return colour;
}
```
  
命名规范：一般写成 getXxx()，这里 Xxx 是对应的属性名首字母大写（例如 getColour、getName、getAge 等）。
注意：如果一个属性不需要对外暴露，就可以不提供相应的 getter 方法，以实现信息隐藏。
修改器：
```Java
public void setName(String name) {
this.name = name;
}
```
命名规范：一般写成 setXxx(参数)，如 setName(String name)、setAge(int age) 等。
在 setName(String name) 里可以看到 this.name = name; this.name 指的是当前对象（this）内部的 name 属性。
name （方法的参数）是外面传进来的值。
之所以要用 this.name 来区分，是为了防止与方法参数的名字冲突。
## 4.5 Java 的参数传递方式
Java 始终使用“值传递”（pass-by-value），无论是基本数据类型还是对象引用：基本数据类型（int、double 等）：方法接收到的是数值的副本，方法内部的修改不会影响原变量。
对象和数组：方法接收到的是对象引用的副本，但它指向同一个对象，所以方法
内部的修改会影响原数组或对象。
### 4.5.1 基本类型参数的值传递
示例代码：
```Java
class PassByWhat {
void go(int z) {
z = z + 7; // 仅在方法内修改，不影响原值
}
public static void main(String[] args) {
PassByWhat p = new PassByWhat();
int x = 7;
p.go(x);
System.out.println(x); // 输出仍然是 7
}
}
```
解释：
go() 方法接收的是 z，它是 x 的副本。
z = z + 7; 不会影响 x，因为 x 的值没有被直接修改，修改的只是 z 这个副本。
### 4.5.2 数组作为参数传递
虽然 Java 仍然是 pass-by-value，但如果传递的是数组，情况有所不同：
```Java
public class PassByTest {
public void mutate(int[] array) {
array[0] = 0; // 直接修改了原数组
}
public static void main(String[] args) {
int[] nums = {1, 2, 3};
PassByTest p = new PassByTest();
p.mutate(nums);
System.out.println(nums[0]); // 输出 0
}
}
```
解释：
mutate() 方法接受的是 array，它是 nums 引用的副本，但仍然指向原始数组。修改 array[0] 会影响 nums[0]，因为 array 和 nums 指向的是同一个数组对象。
关键点总结：
Java 传递所有参数都是值传递（pass-by-value）。
对于基本数据类型，方法内部的修改不会影响原变量。
对于对象和数组，传递的是引用的副本，但引用指向的对象本身仍然可以被修改。
这意味着：
如果想让数组不被方法修改，可以在方法内部创建一个新数组并操作，而不是直接修改传入的数组。
如果需要真正的深拷贝（deep copy），要使用 Arrays.copyOf() 或 clone() 方法来创建新数组。
### 4.5.4 总结
|类型|传递方式|方法内修改影响原变量？|
|---|---|---|
|int、double 等基本数据类型|值传递（复制值）|不影响|
|对象引用（包括数组）|值传递（复制引用）|影响对象内容|
推荐做法：
基本数据类型：不需要担心方法内部修改。
数组或对象：如果不想修改原数据，需手动创建副本。
这部分内容在理解 Java 方法参数传递和避免意外修改数据时非常重要！
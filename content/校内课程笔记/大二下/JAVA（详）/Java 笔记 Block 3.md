Java 笔记 Block 3
## 8 接口
### 8.1 接口的定义和作用
接口是一个100% 抽象的类，它不能被实例化。用来表示一组行为，比如 Flyable 接口表示会飞的生物。接口中方法默认就是 public abstract，即使不写也是这样。接口中可以定义常量（public static final），不能定义普通变量。
|比较项|接口|抽象类|
|---|---|---|
|方法实现|没有（Java 8 前）  <br>Java 8 后可以有 default 和 static 方法|可以有部分方法实现|
|变量|只能有 public static final 常量|可以有普通变量|
|继承|可以多继承（实现多个接口）|只能单继承|
|实例化|都不能实例化|都不能实例化|
如果接口中的方法已经在父类中被实现了，那子类就不需要再实现。但如果还没实现，那子类就必须来实现这个方法，或者它也要是 abstract。下面是接口定义和应用的例子：
```Java
public interface Flyable { 
public abstract void fly(); // OR public void fly();  
// Even if you don’t declare the method abstract or  
// public, it is!!! 
} 
public class FlyingSquirrel extends Creature  
implements Flyable { 
public void fly() { 
// some code 
} 
public void run(int duration) { 
// some code 
} 
}
```
Java8的两种方法实现：
- default 方法（默认方法）
允许在接口中写出方法的实现，用于向旧接口添加新功能，不影响原来的实现类。
```Java
interface Flyable {
default void fly() {
System.out.println("Default flying...");
}
}
```
可以被实现类重写（override） 保证了向后兼容（backward compatibility）
- static 方法（静态方法）
接口中定义的工具方法，只能通过接口名调用。
```Java
interface MathUtil {
static int square(int x) {
return x * x;
}
}
```
类似工具函数（utility method）不能被实现类重写
### 8.2 多个接口中出现同名方法或同名常量（变量）
### 8.2.3 如果父接口中有同名的方法
- 参数不同 → 认为是重载（overloading），都保留
```Java
interface Father {
void say(String msg);
}
interface Mother {
void say(int times);
}
interface Child extends Father, Mother {}
```
重载：在同一个类中，多个方法的名字相同，但是参数不同（参数个数不同，或参数类型不同）。编译器会根据你传的参数来自动选择调用哪个方法。
- 有返回值不同 → 报错！（因为编译器分不清）
```Java
interface Father {
int say();
}
interface Mother {
String say(); // ❌ 报错：返回值不同，方法名和参数都一样
}
```
- 方法完全相同 → 只保留一个版本即可（不会冲突）
### 8.2.4 如果父接口中有同名常量（final 变量）
常量不会冲突，两个都保留，你只需要用接口名来区分。
```Java
interface Father {
int age = 50;
}
interface Mother {
int age = 40;
}
interface Child extends Father, Mother {}
public class Demo {
public static void main(String[] args) {
System.out.println(Father.age); // 50
System.out.println(Mother.age); // 40
}
}
```
注意：这里 Child.age 是不允许的，因为有歧义，必须写成 Father.age 或 Mother.age 来明确指的是哪个。
## 9 GUI
### 9.1 基础
GUI（Graphical User Interface，图形用户界面）是一种让用户通过图形组件（如按钮、窗口、菜单等）与程序交互的方式。相比命令行界面（CLI），GUI 更直观、更易于使用。
GUI的三大核心：
1. Component（组件）
    - 是用户可以看到并与之交互的对象。
    - 比如：按钮（JButton）、文本框（JTextField）、标签（JLabel）等。
2. Container（容器）
    - 是可以包含其他组件的组件。
    - 常见容器：JFrame, JPanel。
    - 它们用来“组织”组件。
3. Event（事件）
    - 是用户的操作触发的动作，比如点击鼠标、按下键盘。
    - GUI 程序要能“监听”和“响应”这些事件，才能实现交互功能。
创建GUI的流程：
4. 创建 组件（比如按钮）
5. 把这些组件放进 容器（比如 JFrame 或 JPanel）
6. 编写代码来响应用户产生的 事件（比如点击按钮）
![image1 5|image1 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%205.png)
如图：
- 最外层是一个 Frame（窗口）
- 里面有一个 Panel（面板）
- 面板里放了 Label, TextField, 和 Buttons，它们都是组件（Components）
![image2 4|image2 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%204.png)
### 9.2 Component
### 9.2.1 JLabel：文本标签
来在界面上显示只读文本。
创建时可指定初始文本和对齐方式：
```Java
// 文本居右对齐
JLabel myLabel = new JLabel("你好，Swing！", JLabel.RIGHT);
```
其中第二个参数可以是 JLabel.LEFT、JLabel.CENTER、JLabel.RIGHT 等水平对齐常量。
动态读写文本：
```Java
String s = myLabel.getText(); // 取出当前文本
myLabel.setText("新内容"); // 修改显示的文本
```
### 9.2.2 JButton：按钮
一个可点击的按钮，显示文本（或图标），用户每次点击都会产生一个 ActionEvent。
创建：
```Java
JButton myButton = new JButton("点我试试");
```
外观：
- 默认有一个边框（border），在不同 Look-and-Feel 下样式各异。
- 除了文字，还可以传入图标：
```Java
Icon icon = new ImageIcon("icon.png");
JButton iconButton = new JButton("保存", icon);
```
响应点击：
- 给按钮注册一个 ActionListener，在 actionPerformed 中编写点击逻辑：
```Java
myButton.addActionListener(e -> {
System.out.println("按钮被点了！");
});
```
### 9.3 Container
容器分为两种：
- top-level Containers：任何 Swing 应用程序中都必须至少有一个这样的容器。
- General-purpose Containers：存在于大多数 Swing 应用程序中。
Frame 容器，它是最常用的顶级窗口之一。它是一个带边框、标题栏（title bar）、可调整大小的窗口，也可以附加菜单栏（menu bar）。与命令行窗口不同，Frame 提供图形化的界面元素。有两种使用方式：
- 继承（extend Frame）：在自己的类中直接 class MyApp extends Frame，这样子类本身就是一个窗口，更常见。
- 实例化（new Frame()）：在其他类里创建 Frame f = new Frame();，不那么常用，但逻辑上同样可以构建窗口 。
![image3 4|image3 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%204.png)
Frame 的默认属性：
- 大小为 0×0：创建后窗口“看不见”也没有尺寸，需调用 setSize(int width, int height) 来设置尺寸。
- 初始不可见：窗口对象创建后默认 visible = false，需调用 setVisible(true) 才会显示出来 。
可以通过 setTitle(String title) 改变窗口标题栏上的文字，例如：
```Java
Frame f = new Frame();
f.setTitle("我的第一个窗口");
```
这样在标题栏中就会显示 "我的第一个窗口" 。
综合起来，要创建并显示一个基本的 AWT Frame，大致流程是：
![image4 4|image4 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%204.png)
这样就能得到一个可见、可调整大小，并带有标题栏的窗口。
### 9.4 Event
当程序收到某种预定义的信号时，就会触发一个事件（event）。事件处理（Event Handling）是捕获（get）事件并对其作出响应（handle）的整个过程。
基本流程：
1. 注册监听器（listener）：告诉组件“当发生某种事件时，请通知我”。
2. 触发事件：用户点击、输入或系统信号到来时，事件对象被创建并派发给已注册的监听器。
3. 回调处理：监听器接口的方法被调用，例如 actionPerformed(ActionEvent e)、mouseClicked(MouseEvent e) 等，在这里编写具体的响应逻辑。
每个事件(event)都需要一个 source 和一个 listener
- 事件源（Event Source）：能够把用户动作（点击、关闭窗口等）或系统信号（定时器到期）“转换”为事件对象的组件/对象。比如点击的 JButton、输入回车的 JTextField、关闭的 JFrame。
- 监听器接口（Listener Interface）：用户代码与事件源之间的“桥梁”，定义了回调方法的签名；实现了这个接口，就相当于告诉事件源“发生事件时，请调用我这里的代码”，具体如以下表格。
- 事件对象（Event Type）：回调方法接收的参数，封装了发生时的上下文（比如鼠标位置、按键代码、哪个窗口被关闭等）。即在“事件发生时”自动创建并传给你的那个对象，里面装着这次事件的所有上下文信息（谁触发、什么时候、在哪里、按了什么键/鼠标按钮、带什么命令……），让你的监听器能据此做出恰当的响应。
匹配关系：
- 每一种事件类型（例如 MouseEvent、ActionEvent、WindowEvent）都有一个对应的监听器接口（MouseListener、ActionListener、WindowListener）。
- 实现接口时，必须提供该接口中所有方法的具体实现（或使用适配器类如 MouseAdapter、WindowAdapter 只覆写需要的方法）。
|事件源（动作）|监听器接口|事件类型对象|
|---|---|---|
|用户点击按钮、在文本框中按回车，或选择菜单项|ActionListener|ActionEvent|
|用户关闭一个顶级窗口（例如 JFrame）|WindowListener|WindowEvent|
|用户在组件上按下鼠标按钮|MouseListener|MouseEvent|
|（或）用户在组件上拖拽或移动鼠标|MouseMotionListener|MouseEvent|
|用户在组件上移动鼠标（仅移动、未按键）|ComponentListener|ComponentEvent|
|组件获得焦点（例如被点击或用 Tab 键切入）|FocusListener|FocusEvent|
编写一个事件处理器（以按钮的 ActionEvent 为例），通常分三步：
1.实现监听器接口
```Java
// 让你的类成为一个 ActionListener
public class MyHandler implements ActionListener {
// … 还会在第 3 步定义 actionPerformed 方法 …
}
```
2.在组件上注册监听器
```Java
JButton btn = new JButton("点我");
btn.addActionListener(new MyHandler());
```
3.定义回调方法
```Java
@Override
public void actionPerformed(ActionEvent e) {
// 这里写“按钮被点击后要做的事”
System.out.println("按钮被点击！");
}
```
完成以上三步后，当用户在界面上“点击按钮”这一动作发生时：
- JButton 会将这个动作封装成一个 ActionEvent 对象，
- 派发给所有已注册的 ActionListener，
- 然后它们的 actionPerformed(...) 方法就被调用，执行你在里面写好的逻辑。
一个具体实现的例子：
![image5 4|image5 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image5%204.png)
### 9.5 布局管理器（LayoutManager）
### 9.5.1 定义
一个接口，规定了“在容器中如何给各个组件分配位置和尺寸”的方法。当容器大小改变（或第一次显示）时，布局管理器会负责计算每个子组件的大小和位置，并执行放置动作。
Java 自带的常用实现：
- FlowLayout（流式布局）：组件按添加顺序水平排列，遇边界就换行。
- BorderLayout（边界布局）：分为 North/South/East/West/Center 五区。
- GridLayout（网格布局）：按指定行列等分空间。
- BoxLayout（盒式布局）：沿 X 轴或 Y 轴线性排列。
- 还有更高级的 GridBagLayout、GroupLayout 等。
```Java
JPanel panel = new JPanel();
panel.setLayout(new BorderLayout()); // 给面板指定一个 BorderLayout
panel.add(btn, BorderLayout.SOUTH); // 把按钮放在南边
```
组件（Component）、容器（Container）和布局管理器（LayoutManager）协同：
1. 创建容器（JFrame 或 JPanel）→
2. 设置布局管理器（如 panel.setLayout(new GridLayout(2,2))）→
3. 向容器添加子组件（panel.add(button)）→
4. 布局管理器 根据规则自动给这些组件定位置、定大小→ 最终形成窗体上的界面。
给一个容器（通常是 JPanel 或 JFrame 的内容面板）替换或指定它的布局管理器（LayoutManager）实例：
方法一：分两步走
- Step 1： 创建一个布局管理器实例
```Java
FlowLayout flow = new FlowLayout();
```
- Step 2： 调用容器的 setLayout(...) 方法，传入这个布局
```Java
JPanel p = new JPanel();
p.setLayout(flow);
```
方法二：一步到位
Java 的大多数容器（例如 JPanel）都提供了一个带 LayoutManager 参数的构造器，你可以直接在创建时指定：
```Java
JPanel p = new JPanel(new FlowLayout());
```
布局管理器一定要在向容器中 添加任何组件之前 设定好，否则新加入的组件可能会使用容器的默认布局，不会按照你想要的方式排列。
### 9.5.2 FlowLayout
待补充
### 9.5.3 GridLayout
待补充
## 10 垃圾回收
### 10.1 堆和栈
堆（Heap）：
- 用于存放通过 new 关键字创建的 对象；
- 实例变量（Instance variables） 存放在堆中；
- 堆内存由 垃圾回收器（Garbage Collector, GC） 管理；
- 堆内的对象直到没有任何引用指向它时，才会被 GC 回收。
栈（Stack）
- 存放方法调用的信息（如局部变量、参数等）；
- 每次调用方法，会压入一个“栈帧（Stack Frame）”，方法结束则弹出；
- 变量的作用域和生命周期主要由栈控制。
![image6 4|image6 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image6%204.png)
|变量类型|存放位置|生命周期说明|
|---|---|---|
|局部变量|栈|所属方法运行时存在，方法结束即消失|
|实例变量|堆|对象存在期间一直有效|
![image7 4|image7 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image7%204.png)
Dog 类展示了 size 和 name 是实例变量，而 maxSpeed 是局部变量。
一个方法被调用时，它会被压入调用栈的顶部（top of Stack），方法执行完（遇到右花括号 } 结束）后，其对应的栈帧会被弹出栈。栈帧里保存了这个方法执行的所有局部变量和当前执行状态（比如执行到哪一行）。如下：
```Java
public void doSomething() {
boolean b = true;
ready(10);
}
public void ready(int x) {
int y = x * 24;
// more code here
}
```
当 doSomething() 被调用：
- 一个新的栈帧被压入栈中；
- 局部变量 b = true 被存储在这个栈帧中；
- 然后它调用了 ready(10)，于是 ready() 方法也被压栈。
当 ready(10) 被调用：
- 又一个新的栈帧被压入栈中（在栈顶）；
- 它有参数 x = 10，局部变量 y = x * 24 = 240。
![image8 4|image8 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image8%204.png)
在 Java 中创建一个子类对象时，它不仅拥有自己的成员变量，还会在内存中包含其父类所有的成员变量和结构，这是继承机制在内存层面上的体现。
![image9 4|image9 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image9%204.png)
### 10.2 对象与变量的生命周期
### 10.2.1 对象的生存期（Object Life）
- 对象是否“活着”完全取决于是否还有引用变量指向它；
- 换句话说：只要引用存在，对象就不会被垃圾回收器 GC 回收。
Java 中对象是“动态分配”的（dynamically allocated）使用 new 关键字创建对象时，JVM 在运行时从堆（Heap）中分配内存，类似于 C 语言中的 malloc() 函数。内存随着程序运行而增长和收缩，每次创建新对象都占用新的内存，如果没有及时释放，会造成内存膨胀。如以下所示：
```Java
for (long i = 0; i < 10000000; i++) {
Date d = new Date();
}
```
这段代码中，在每次循环中都创建了一个新的 Date 对象，但变量 d 是局部变量，每次循环结束都会被覆盖或丢弃，所以之前的对象就变成没有引用的垃圾（unreachable objects）；它们会被 Java 的 垃圾回收器 GC 回收。
如果一个对象的引用被移除或覆盖，这个对象就再也无法访问。因为它仍然占用堆内存，但程序再也不能用它，此时它就变成垃圾，成为 GC 的目标。当对象只被一个引用指向，且这个引用在栈中时，如果这个方法执行完后，该栈帧消失，引用也随之消失，它就会变成它就变成“eligible for GC”。
有三种对象失去引用的方式：
- 引用变量超出作用域（goes out of scope）：
```Java
public void doSomething() {
Car myCar = new Car(); // 一旦方法结束，myCar 超出作用域，Car 对象无引用
}
```
- 将引用变量赋值给另一个对象：
```Java
Car myCar = new Car();
myCar = new Car(); // 原来的 Car 对象没有任何引用，变成“垃圾”
```
- 显式将引用变量设置为 null：
```Java
Car myCar = new Car();
myCar = null; // 现在该对象没有任何引用
```
将引用变量设置为 null，意味着它不再指向任何对象，如果对一个 null 引用使用点操作符（.），会抛出 NullPointerException 异常，Java 中的实例引用变量默认值是 null，如果你没有手动初始化它们。
示例：
```Java
public class Student {
String name; // 默认 null
int age; // 默认 0
boolean isMScStudent;// 默认 false
char gender; // 默认 '\u0000'
public static void main(String[] args) {
Student aStudent = null;
System.out.println("Student name? " + aStudent.name);
// ↑ 会报 NullPointerException，因为 aStudent 是 null
}
}
```
### 10.2.2 变量的生命周期（Variable Lifetime）
- 不论是基本类型（primitive）还是引用类型（reference），生命周期一致；
- 但局部变量（local）和实例变量（instance）的生命周期不一样。
|变量类型|生命周期说明|示例|
|---|---|---|
|局部变量（local）|只在方法执行时存在，出了方法就被销毁|int x = 10;|
|实例变量（instance）|只要对象存在就存在|private String name;|
示例如下：
```Java
public class Dog {
private String name; // 实例变量：在整个对象生命周期内都存在
public void setName(String dogName) {
this.name = dogName; // dogName 是局部变量
// dogName 在方法结束后就被销毁
}
public void sleep() {
int x = 10; // x 是 sleep 方法的局部变量
}
}
```
- name 是对象的一部分，存储在堆中，随着 Dog 对象的生命周期存在；
- dogName 和 x 是临时变量，只在各自的方法中“可见并存在”。
“变量是否还活着”与“是否还能访问它”不完全等价。变量必须在作用域（scope）内，才能访问；但内存中可能还存在。
局部变量（Local Variable）的作用域（Scope）：
- 局部变量只能在它所声明的方法内部被访问；
- 即使变量仍然“活着”，只要不在声明它的方法中，就不能使用它。
## 11 字符串
### 11.1 字符串介绍
在 Java 中，字符串（String）不是基本数据类型，而是一个 对象（object）。和 C 语言类似，字符串字面量用双引号（”）括起来。例如："Hello" 是一个有效的字符串字面量。实际上，字面量 "Hello" 是 String 类的一个对象。
Java 自动导入了java.lang，是 Java 核心类库的一部分，包含了 Java 编程语言的基础类，如 Object, String, Math 等。
### 11.2 字符串的特性
### 11.2.1 不可变性 immutable
不可变（immutable） 意思是：字符串一旦创建，内容不能更改。
例如：
```Java
String s = "0";
for (int x = 1; x < 10; x++) {
s = s + x;
}
```
这段代码每次循环都会生成一个新的 String 对象。
### 11.2.2 字符串常量池 String Pool
String Pool 是 JVM 中专门用来存储 字符串字面量 的内存区域。
当你写：
```Java
String s1 = "hello";
String s2 = "hello";
```
JVM 不会为第二个 "hello" 再创建新对象，而是直接让 s2 指向 s1 指向的同一个对象。垃圾回收器（Garbage Collector）不会清理 String Pool 中的内容，所以这些对象会一直存在，直到 JVM 关闭。
例如，以下是普通对象与字符串对象在赋值和修改时的行为差异：
- 一般对象的行为：
```Java
Rabbit r1 = new Rabbit();
r1.setName("Benji");
Rabbit r2 = r1;
r2.setName("Blinky");
System.out.println(r1.getName());
System.out.println(r2.getName());
```
创建了一个 Rabbit 对象 r1，名字为 "Benji"。把 r1 的引用赋给 r2，此时 r1 和 r2 指向同一个对象。改变 r2 的名字，其实也就改变了 r1 指向的对象的名字。
输出结果：
```Java
Blinky
Blinky
```
- 字符串对象的行为：
```Java
String s1 = "Sherlock";
String s2 = s1;
s2 = "Holmes";
System.out.println(s1);
System.out.println(s2);
```
s1 指向字符串 "Sherlock"。s2 = s1 之后，s2 也指向 "Sherlock"。但 s2 = "Holmes" 会让 s2 指向一个新的字符串对象 "Holmes"，而不是修改原来的 "Sherlock" 对象（因为字符串是不可变的）。s1 仍然指向原来的 "Sherlock"。
输出结果：
```Java
Sherlock
Holmes
```
|行为|普通对象 (Rabbit)|字符串 (String)|
|---|---|---|
|引用复制|两个变量指向同一个对象|两个变量最初指向同一个对象|
|修改内容|任一变量修改，另一个也受影响|赋值新字符串后，变量指向新对象，互不影响|
|输出结果|两个都输出 Blinky|分别输出 Sherlock 和 Holmes|
### 11.2 字符串类
Java 重载了 + 运算符，用于 字符串拼接（concatenation）。
例如：
```Java
String s = "Hello" + "World"; // 输出 "HelloWorld"
```
同时，String 是一个对象（不是基本类型）因此，可以对字符串调用方法，
例如：
```Java
s.length(), s.charAt(0), s.substring(1, 3) 等
```
类似数组，字符串的索引也是从 0 开始，到 length() - 1 结束。
```Java
String s = "Cat";
s.charAt(0); // 返回 'C'
```
String 类有以下构造方法：
|构造方式|说明|
|---|---|
|String s = "HelloWorld!";|直接使用字面量创建字符串|
|String s = new String("HelloWorld!");|显式用构造器创建相同字符串|
|String s = new String();|创建一个空字符串|
|char[] Cat_Array = {'t','i','g','e','r','s'};|字符数组|
|String s = new String(Cat_Array);|将整个字符数组转为字符串，结果为 "tigers"|
|String s = new String(Cat_Array, 1, 2);|从索引 1 开始取 2 个字符，结果为 "ig"|
### 11.3 字符串类常用方法
|方法名|作用|参数|返回值|示例/说明|
|---|---|---|---|---|
|length()|获取字符串长度|无|int|"Hello".length() → 5|
|charAt(index)|获取指定位置字符|int index|char|"Java".charAt(2) → 'v'|
|indexOf(ch) / indexOf(str)|查找字符或子串首次出现位置|char / String|int（不存在返回 -1）|"Hello".indexOf('l') → 2|
|lastIndexOf(ch) / lastIndexOf(str)|查找最后一次出现的位置|char / String|int|"Hello".lastIndexOf('l') → 3|
|equals(str)|比较字符串内容是否相等|String|boolean|"abc".equals("ABC") → false|
|equalsIgnoreCase(str)|忽略大小写比较|String|boolean|"abc".equalsIgnoreCase("ABC") → true|
|compareTo(str)|按字典序比较字符串|String|int（<0、=0、>0）|"cat".compareTo("dog") → < 0|
|substring(begin) / substring(begin, end)|截取子串|int / int, int|String|"Monkeys".substring(3) → "keys"|
|concat(str)|拼接字符串|String|String|"Hello".concat("World") → "HelloWorld"|
|toUpperCase() / toLowerCase()|大小写转换|无|String|"cat".toUpperCase() → "CAT"|
|toString()|转换为字符串|无|String|Double.toString(12.3) → "12.3"|
|split(regex)|使用正则表达式分割字符串|String|String[]|"a:b:c".split(":") → ["a", "b", "c"]|
|getChars(i, j, A, k)|将部分字符复制到字符数组中|起始/结束索引，目标数组，写入起始索引|void|"abcde".getChars(1, 4, A, 0) → {'b','c','d'}|
|replace(oldChar, newChar)|替换字符|char, char|String|"goose".replace('o', 'e') → "geese"|
### 11.4 StringBuffer 与 StringBuilder 类：可变字符串
Java 中 String 是不可变对象，每次修改都会创建新对象，效率低。如果需要频繁拼接、插入、删除字符串，使用 StringBuffer 或 StringBuilder 更高效。
核心区别：
|类名|是否线程安全|效率|推荐使用场景|
|---|---|---|---|
|StringBuffer|✅ 是线程安全的（同步）|慢|多线程环境|
|StringBuilder|❌ 不是线程安全的|快|单线程环境|
StringBuilder 与 StringBuffer 提供相同的方法，区别在于：StringBuilder 的方法不是 synchronized（同步的）。
StringBuffer 每次空间不足时会重新分配内存，为了提高效率，Java 默认多分配 16 个字符空间。
### 11.5 Character 类
Character 类是一个包装类（Wrapper Class），用于封装基本数据类型 char 的对象操作。属于 java.lang 包，无需手动导入即可使用。用于处理单个字符，支持很多静态方法进行判断和比较。是 char 的对象封装版本。
常用静态方法（静态方法直接通过类调用）：
|方法名|功能说明|示例|
|---|---|---|
|isLetter(char c)|判断是否是字母|'a' → true|
|isDigit(char c)|判断是否是数字|'3' → true|
|isUpperCase(char c)|判断是否是大写字母|'A' → true|
|isLowerCase(char c)|判断是否是小写字母|'z' → true|
|isLetterOrDigit(char c)|是否是字母或数字|'?' → false|
示例：
```Java
Character myCharacter = new Character('c');
```
这是一个封装了字符 'c' 的对象。
对比与比较方法：
```Java
myCharacter.compareTo(new Character('f')); // 返回 -3
myCharacter.compareTo(new Character('a')); // 返回 2
myCharacter.equals(new Character('e')); // 返回 false
```
- compareTo() 按 Unicode 值比较（'c' - 'f' = -3）。
- equals() 判断字符值是否一致。
其他操作：
```Java
char c = myCharacter.charValue(); // 解包，得到原始的 char 值 'c'
```
|特性|char|Character|
|---|---|---|
|类型|基本数据类型|包装类|
|是否为对象|❌ 否|✅ 是|
|支持方法调用|❌ 不能直接调用方法|✅ 支持丰富的静态/实例方法|
|使用场景|简单字符存储|判断、转换、比较等复杂操作|
### 11.6 StringTokenizer 类
是一个过时类（legacy class），不多赘述。
### 11.7 Scanner 类
Scanner 类属于 java.util 包。可以:
- 以自定义分隔符读取字符串中的token；
- 解析原始数据类型（如 int、double）；
- 读取控制台输入。
示例 1：按单词分隔符读取（支持整个单词作为分隔符）
```Java
String s = "Let your heart guide you.";
Scanner myScanner = new Scanner(s);
myScanner.useDelimiter("you");
while (myScanner.hasNext()) {
System.out.println(myScanner.next());
}
```
输出：
```Java
Let
r heart guide
.
```
useDelimiter("you") 表示以单词 "you" 作为分隔符。
示例 2：扫描整数并计算总和
```Java
String s = "1 10 100 1000";
Scanner myScanner = new Scanner(s);
int sum = 0;
while (myScanner.hasNext()) {
sum += myScanner.nextInt();
}
System.out.println("Sum = " + sum);
```
输出：
```Java
	Sum = 1111
```
每个整数作为一个 token 读取并相加。
示例 3：读取用户输入（控制台）
```Java
System.out.print("Please enter an int value: ");
Scanner myScanner = new Scanner(System.in);
int i = myScanner.nextInt();
```
从用户输入中读取一个整数值。
### 11.8 String.format() 及其格式说明符（Format Specifier）
String.format() 格式说明符结构的完整语法如下：
```Java
%[argument_index$][flags][width][.precision]type
```
|组件|说明|
|---|---|
|%|格式说明符的起始标记|
|[argument_index$]|指定使用第几个参数（从 1 开始）|
|[flags]|额外格式控制，如添加逗号、左对齐、补零等|
|[width]|最小宽度，不足会补空格|
|[.precision]|精度：小数点后保留位数（用于浮点数）|
|type|格式类型，如 %f 表示浮点，%d 表示整数，%c 表示字符，%x 表示十六进制|
示例如下：
```Java
String.format("I have %,6.2f bugs to fix", 12345.6789);
```
%,6.2f 的意思是：
- ,：加入千位分隔符（如 12,345）
- 6：最小宽度为 6（若不够会补空格）
- .2：保留 2 位小数
- f：浮点数
输出结果：
```Java
I have 12,345.68 bugs to fix
```
同时也支持多参数
常见格式类型对照表
|类型|含义|示例结果|
|---|---|---|
|%d|整数|123|
|%f|浮点数|12.34|
|%x|十六进制|7b（表示十进制 123）|
|%c|字符|'A'|
|%s|字符串|"Hello"|
其中，printf() vs println() 的区别：
```Java
System.out.printf("Using printf: %s %s has %d %s.\n",
firstName, lastName, numPets, petType);
System.out.println("Using println: " +
firstName + " " + lastName + " has " +
numPets + " " + petType + ".");
```
输出：
```Java
Using printf: John Doe has 7 chickens.
Using println: John Doe has 7 chickens.
```
区别说明：
|方法|特点|
|---|---|
|printf()|使用格式化字符串，更优雅、可控制格式|
|println()|用 + 拼接字符串，直接输出|
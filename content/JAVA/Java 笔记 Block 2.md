Java 笔记 Block 2
## 5 数组
在 Java 语言中，数组（Array）是一种用于存储固定大小的同类型元素的容器。数组可以存储基本数据类型（如 int、double）或对象（如 String、Person 类的实例）。
### 5.1 数组的概念
- 数组是引用类型，在内存中存储的是对象的引用（地址）。
- 数组是定长的，一旦创建，大小不能更改。
- 数组的索引从 0 开始，最后一个元素的索引是 length - 1。
- 数组可以存储基本数据类型或对象。
- 数组是一个对象，即使它是基本数据类型数组。
### 5.2 数组的声明
在 Java 中，数组可以用以下两种方式声明：
一般推荐使用第一种方式
```Java
// 第一种：数据类型 + 方括号 + 数组名
int[] arr1;
// 第二种：数据类型 + 数组名 + 方括号
int arr2[];
```
### 5.3 数组的创建
数组必须先 分配内存 才能使用。
（1）静态初始化（声明的同时初始化）
（2）动态初始化（先声明，后初始化）
```Java
int[] arr = {1, 2, 3, 4, 5}; // 自动推导数组大小
String[] names = {"Alice", "Bob", "Charlie"};
int[] arr = new int[5]; // 创建一个长度为 5 的数组，默认值为 0
double[] prices = new double[3]; // 创建一个长度为 3 的数组，默认值为 0.0
```
### 5.4 数组的常见操作
### 5.4.1 数组的访问，修改和遍历
和C语言一样
### 5.4.2 获取数组长度
```Java
System.out.println(arr.length); // 获取数组长度
```
### 5.4.3 数组排序
Java 提供了 Arrays.sort() 方法排序：
```Java
import java.util.Arrays;
int[] arr = {5, 3, 8, 1, 2};
Arrays.sort(arr);
System.out.println(Arrays.toString(arr)); // [1, 2, 3, 5, 8]
```
### 5.5 主函数的数组
public static void main(String[] args) 说明main()方法接收一个字符串数组 (String[] args) 作为参数。args 是一个数组，可以通过索引（如args[0]）访问其元素，且如：
```Java
public static void main(String[] args) {
System.out.println(args[0]); // 打印数组的第一个值
}
```
这段代码会打印命令行传递的第一个参数。
args.length 可以获取传递给main()方法的参数个数，如：
```Java
public static void main(String[] args) {
System.out.println(args.length);
}
```
### 5.6 对象数组
1. 声明对象数组 java复制编辑Rabbit[] bunnies;
    - 这里声明了一个Rabbit类型的数组bunnies，但此时只是创建了一个引用变量，并未实际分配数组的内存空间。
    - 可以理解为bunnies充当了一个“控制器”，指向一组Rabbit对象。
2. 创建对象数组 java复制编辑bunnies = new Rabbit[7];
    - 这行代码创建了一个长度为7的Rabbit数组，但注意此时数组中的每个元素（每只兔子）仍然是null，还没有真正的Rabbit对象。
    - 这个数组存储的是Rabbit对象的引用，而不是实际的Rabbit对象。
3. 示意图说明
    - bunnies变量是一个引用，指向了Rabbit[7]数组。
    - 数组中的每个槽位（索引0到6）都可以存放一个Rabbit对象的引用。
    - 但刚创建时，这些槽位是空的（默认值为null），需要手动初始化。
### 5.6.1 如何真正创建并初始化每个Rabbit对象？
这样，每个bunnies[i]都指向一个真正的Rabbit对象，数组才算真正可以使用。
```Java
for (int i = 0; i < bunnies.length; i++) {
bunnies[i] = new Rabbit(); // 给每个数组元素创建一个Rabbit对象
}
```
### 5.6.2 Tips：
- 对象数组和基本类型数组的区别：
    - int[] nums = new int[7]; 直接创建了存储int值的数组，数组元素自动初始化为0。
    - Rabbit[] bunnies = new Rabbit[7]; 仅创建了存储Rabbit对象引用的数组，但未初始化对象，需要手动创建Rabbit实例。
- 先声明，再创建，再初始化：
    1. Rabbit[] bunnies; // 声明数组
    2. bunnies = new Rabbit[7]; // 创建数组（但元素是null）
    3. bunnies[i] = new Rabbit(); // 逐个创建对象
### 5.7 对象数组的重要方法
### 5.7.1 toString()
直接打印对象数组的元素，如：
```Java
for (int i = 0; i < racers.length; i++) {
System.out.println(racers[i]);
}
```
这样打印racers[i]时，默认会调用Object类的toString()方法，输出类似：
```Java
Rabbit@3e25a5
Rabbit@923e30
Rabbit@9cab16
```
这些值是对象的哈希码地址，而不是我们想要的兔子信息，原因是如果类没有重写toString()方法，Java默认使用Object类的toString()方法，它返回对象的类名 + 内存地址。
如果我们重写toString方法，如以下所示：
```Java
public class Rabbit {
// Rabbit类的其他内容（构造函数、属性等）
public String toString() {
return this.getName() + " is a " + this.getFurType() +
" Rabbit that runs at " + this.getSpeed() + " km/hr.";
}
}
```
这里，我们重写了toString()方法，使其返回具体的兔子信息：
- 兔子的名字（getName()）
- 兔子的毛发类型（getFurType()）
- 兔子的奔跑速度（getSpeed()）
我们就有正确的输出，如下所示：
```Java
Bugs is a Fluffy Rabbit that runs at 150 km/hr.
Bunny is a Long-haired Rabbit that runs at 145 km/hr.
Bob is a Shaggy Rabbit that runs at 125 km/hr.
```
这样，每当我们打印racers[i]时，Java就会调用我们自定义的toString()方法，而不是默认的Object.toString()方法。
tips:
打印基本数据类型数组的时候不需要重写
### 5.7.2 arraycopy()
如果直接复制，如下所示：
  
问题：
- 这种方式并不会真正复制数组的内容，而只是复制了数组的引用。
- racers2 和 racers 指向同一个数组对象，对racers2的修改也会影响racers。
- 这样会导致不期望的数据修改，如果一个数组变量改变了内容，另一个也会同步变化。
- racers 和 racers2 都指向同一块内存。
- 只是复制了引用（reference），没有创建新的对象！
正确的复制方法：
1.用一个循环去复制元素，如下：
```Java
int[] nums2 = new int[nums.length]; 
for (int i=0; i<nums.length; i++) { 
nums2[i] = nums[i]; 
}
```
2. 用arraycopy复制元素
System.arraycopy() 是 Java System 类的一个静态方法，用于在数组之间高效复制元素。
```Java
System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length);
```
|参数|作用|
|---|---|
|src|源数组（要从哪个数组复制）|
|srcPos|源数组的起始索引（从哪里开始复制）|
|dest|目标数组（要复制到哪个数组）|
|destPos|目标数组的起始索引（从哪里开始粘贴数据）|
|length|要复制的元素数量|
参数解析
使用实例如下：
```Java
int[] nums = {1, 2, 3, 4, 5};
int[] nums2 = new int[3];
System.arraycopy(nums, 1, nums2, 0, 3);
```
结果如下：
```Java
	nums2 = [2, 3, 4] // 从 nums[1] 开始复制 3 个元素
```
## 6 JavaDoc
### 6.1 Javadoc 的作用
- Javadoc 是 Java 的文档生成工具，可以用于 生成代码的“维护手册”。
- 运行 javadoc 工具可以解析 Java 源代码中的声明和文档注释（Doc comments），并生成一组 HTML 文档。
### 6.2 Javadoc 文档注释的结构
Javadoc 注释由两部分组成：
1. 描述（Description）：对类或方法的作用进行说明。
2. 标签（Tags）：提供额外的信息，例如作者、参数、返回值等。
示例:
```Java
/**
* 这是一个 Javadoc 文档注释的示例。
*
* @tag 这是标签部分的注释
*/
```
### 6.3 常见的 Javadoc 标签
在 Javadoc 中，标签必须按照特定的顺序出现：
|标签|适用范围|说明|
|---|---|---|
|@author|类、接口|指定作者|
|@version|类、接口|版本信息|
|@param|方法、构造函数|说明参数|
|@return|方法|说明返回值|
|@exception|方法|说明可能抛出的异常|
|@see|所有|参考相关内容|
|@since|所有|说明自哪个版本起可用|
|@serial|序列化字段|说明序列化属性|
|@deprecated|所有|标注已弃用的代码|
### 6.4 生成 Javadoc 文档
可以使用 javadoc 命令在 终端/命令行 生成 Java 文档：
```Java
javadoc -d docs file.java
```
- d docs 表示生成的 HTML 文档存放在 docs 目录下。
- file.java 是 Java 源代码文件。
如何查看 Javadoc 文档：
- 生成 Javadoc 后，可以用 浏览器 打开 docs 目录中的 index.html 文件查看文档。
### 6.5 Javadoc 示例
```Java
/**
* 该类用于从 0 计数到指定的数字。
*
* @author Laurissa Tokarchuk
* @version 1.0
*/
public class CountTo {
/**
* 计数方法，从 0 开始计数到指定的数字。
*
* @param countTo 计数的目标数字
*/
public void count(int countTo) {
for (int i = 0; i < countTo; i++) {
System.out.println("Count = " + (i + 1));
}
}
public static void main(String[] args) {
new CountTo().count(5);
}
}
```
解释：
- @author 说明作者。
- @version 说明版本。
- @param 说明方法的参数 countTo。
### 6.6 总结
- Javadoc 是 Java 官方推荐的代码文档生成工具。
- 通过 /** ... */ 语法编写 Javadoc 文档注释。
- Javadoc 标签按特定顺序排列，可用于类、方法、字段 等。
- 使用 javadoc 命令 自动生成 HTML 格式的 API 文档，方便阅读和维护。
## 7 类的继承和抽象类
### 7.1 类的聚合 Aggregation
- 聚合表示 “has-a” 关系（“拥有”关系）。
- 在 Java 中，没有特殊的关键字 来表示聚合。
- 对象作为实例变量 存在于另一个类中。
```Java
public class RangeRover {
public Tire[] array = new Tire[4];
public void drive() {
// do driving things ...
}
}
```
代码解析：
- RangeRover 类中有一个 Tire[] 数组，表示该车拥有四个轮胎对象。
- drive() 方法表示汽车的驾驶功能（这里没有具体实现）。
图示中，4 个轮胎可能看起来一样（相同的状态），但它们是独立的对象，彼此不同。多个对象可能有相同的状态，但它们仍然是不同的对象，这意味着每个对象在内存中都有自己的地址，即使它们的数据相同。
### 7.2 类的继承 Inheritance
继承（Inheritance）是一种父类（Superclass）和子类（Subclass）的关系。继承在 Java 中使用 extends 关键字，如以下所示：
父类 Doctor
```Java
public class Doctor {
boolean worksAtHospital;
void treatPatient() {
// perform a checkup
System.out.println("checkup");
}
}
```
子类 FamilyDoctor
```Java
public class FamilyDoctor extends Doctor {
boolean makesHouseCalls;
void giveAdvice() {
// perform a checkup
System.out.println("advise");
}
}
```
- FamilyDoctor 继承 Doctor，表示家庭医生。
- makesHouseCalls 属性表示家庭医生是否上门出诊。
- giveAdvice() 方法表示医生给病人建议（advise）。
- FamilyDoctor没有重写 treatPatient() 方法，因此它继承 Doctor 的 treatPatient()，调用时仍会执行 "checkup"。
### 7.2.1 方法重写（Overriding）和新增方法
方法重写（Method Overriding） 允许子类提供与父类相同的方法签名，但不同的实现。 必须满足：
1. 方法名、参数列表相同（必须匹配）。
2. 返回类型相同（Java 5+ 允许协变返回类型）。
3. 访问权限不能比父类更严格（但可以更宽松）。
4. 不能重写 final 方法。
5. 只能重写 非静态 方法（static 方法属于类本身，不能被子类覆盖）。
如下所示：
子类 Surgeon
```Java
public class Surgeon extends Doctor {
void treatPatient() {
// perform surgery
System.out.println("surgery");
}
void makeIncision() {
// make incision
System.out.println("incise");
}
}
```
- Surgeon 继承 Doctor，表示外科医生。
- 重写（Override）了 treatPatient() 方法：
    - Doctor 的 treatPatient() 进行 检查（checkup）。
    - Surgeon 的 treatPatient() 进行 手术（surgery），覆盖（override） 了父类的方法。
- 新增方法 makeIncision()：
    - makeIncision() 是外科医生特有的功能，父类 Doctor 没有这个方法。
### 7.3 访问修饰符（Access Modifiers）对继承的影响
|public|public 变量和方法 可以被子类继承，子类可以直接访问它们。|
|---|---|
|protected|protected 变量和方法 可以被子类继承，但在不同包中，只有子类可以访问。|
|---|---|
|private|private 变量和方法 不能被子类继承，子类无法直接访问它们。|
|---|---|
示例 1: 父类 Parent 和子类 Child
```Java
public class Parent {
protected double cash;
protected void spendMoney(double amount) {
cash -= amount;
}
}
```
- cash 和 spendMoney()都是 protected，意味着：
    - 子类可以继承并访问它们。
    - 同一包内的其他类也可以访问。
    - 不同包的非子类无法访问。
示例 2: 子类 Child
```Java
public class Child extends Parent {
private void buyGadgets(double amount) {
this.spendMoney(amount);
}
}
```
- Child 继承了 Parent。
- buyGadgets() 是 private，意味着它只能在 Child 内部使用。
- buyGadgets() 调用了 spendMoney()，这是允许的，因为 spendMoney() 是 protected，可以被子类继承和访问。
示例 3: 另一个类 AnotherClass
```Java
public class AnotherClass {
public static void main(String[] args) {
Parent p = new Parent();
p.spendMoney(1000000.32); // ✔️✖️
Child c = new Child();
c.buyGadgets(50.94); // ❌❌
}
}
```
访问权限检查：
1. p.spendMoney(1000000.32);
    - ✔️ 允许 如果 AnotherClass 在 Parent 的同一包中。
    - ✖️ 不允许 如果 AnotherClass 在不同包中，因为 spendMoney() 是 protected，而 AnotherClass 不是 Parent 的子类。
2. c.buyGadgets(50.94);
    - ❌ 不允许，因为 buyGadgets() 是 private，只能在 Child 内部使用，不能在 AnotherClass 访问。
结论：
✅ public 方法和变量可以被子类继承和访问（任何地方都能访问）。
✅ protected 方法和变量可以被子类继承，但只能在同包内或子类中访问。
✅ private 方法和变量不能被子类继承，子类甚至无法访问它们。
✅ 不同包的非子类不能访问 protected 方法。
这些规则对于设计良好的 封装（Encapsulation） 和 继承层次结构（Inheritance Hierarchy） 非常重要。
### 7.4 多态 Polymorphism
多态指用 父类（superclass）引用 来指向 不同子类（subclass）对象。
如果 Rabbit 和 Turtle 是 Creature 的子类，我们可以：
用父类 Creature 引用子类对象：
```Java
Creature c = new Rabbit();
```
创建一个 Creature 类型的数组，里面装各种子类对象：
```Java
Creature[] cArray = new Creature[7];
cArray[0] = new Rabbit();
cArray[1] = new Turtle();
cArray[2] = new Rabbit();
// 依此类推...
```
![image1 4|image1 4.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%204.png)
图中那排“桶” 就是这个数组的视觉表示：
- 每个桶是一个 Creature 引用。
- 每个桶里放的是不同的对象（Rabbit 或 Turtle）。
注意：
多态不能调用子类特有的方法，即必须在父类里有定义。如果没有定义，只有强制类型转换后才能调用：
```Java
// 父类
public class Creature {
public void run() {
System.out.println("I run like a generic creature.");
}
}
// 子类 Rabbit，重写 run()，并有自己的 sleep() 方法
public class Rabbit extends Creature {
@Override
public void run() {
System.out.println("I run like a Rabbit!");
}
public void sleep() {
System.out.println("I sleep like a Rabbit.");
}
}
// 测试类
public class CreatureTest {
public static void main(String[] args) {
Creature c = new Rabbit(); // 多态：父类引用指向子类对象
// ✅ 调用重写的方法 —— 成功
c.run(); // 输出: I run like a Rabbit!
// ❌ 尝试调用子类特有方法 —— 编译错误
// c.sleep(); // 编译失败：Creature 中没有 sleep()
// ✅ 使用类型转换 —— 成功
if (c instanceof Rabbit) {
Rabbit r = (Rabbit) c;
r.sleep(); // 输出: I sleep like a Rabbit.
}
}
}
```
### 7.5 抽象类
抽象类是不能被实例化的类，它通常用作父类，为子类提供统一的结构（属性 + 方法）。
- 抽象类可以包含：
    
    - 普通方法（有方法体）
    - 抽象方法（没有方法体，子类必须实现）
    
    ```Java
    public abstract class Creature {
    // 一些属性和方法
    }
    ```
    
正确使用抽象类的方式：
你可以让子类继承它，并创建子类对象：
```Java
Creature bCreature = new Rabbit(); // ✅ 正确
bCreature.run(5, true); // 调用的是 Rabbit 的实现
```
抽象类让你可以：
- 强制子类必须实现某些行为（如果你定义了抽象方法）
- 提供通用属性和默认实现（比如 swim() 方法）
- 统一管理所有子类对象（比如 Creature[] 或 ArrayList<Creature>）
### 7.6 “mega”类
Java 中每一个类，不管你有没有写 extends，都会自动继承 Object 类。
Object类包含四个方法，分别是：
- equals() 确定一个对象是否等于另一个对象
我不能直接如下去比较：
```Java
Rabbit r1 = new Rabbit();
Rabbit r2 = new Rabbit();
if (r1 == r2) {
System.out.println(“yes”);
}
else {
System.out.println(“no”);
}
```
这样比较的是内存里的地址，而不是对象的状态。所以我们要用equals：
```Java
Rabbit r1 = new Rabbit();
Rabbit r2 = new Rabbit();
if (r1.equals(r2)) {
System.out.println(“yes”);
}
else {
System.out.println(“no”);
}
```
- toString()允许打印对象
记住：如果不覆盖从类继承的方法，就只能获得对象的地址。
```Java
Turtle t = new Turtle();
System.out.println(t);
```
Outputs:Turtle@7r234f
- hashCode() 是每个对象的唯一标识，通常基于其内存地址
```Java
Rabbit r = new Rabbit();
System.out.println(r.hashCode())
```
Outputs:8348748
- getClass() 返回对象的类
```Java
Rabbit r = new Rabbit();
System.out.println(r.getClass());
```
Outputs:class Rabbit
### 7.7 构造器链
### 7.7.1 简介
当创建一个对象时，如果它的类有父类，那么不仅会调用子类的构造方法，还会自动调用父类的构造方法，这就是构造器链。当一个新对象被创建时，它继承树（inheritance tree）中的所有构造器都必须被运行，使用 new 会触发构造器的“连锁反应”，只有当所有父类构造器都执行完，对象才算“完全形成”。例如：
```Java
class Animal {
public Animal() {
System.out.println("Animal constructor");
}
}
class Dog extends Animal {
public Dog() {
System.out.println("Dog constructor");
}
}
public class Test {
public static void main(String[] args) {
Dog myDog = new Dog();
}
}
```
输出结果：
```Java
Animal constructor 
Dog constructor
```
说明构造器调用顺序是：父类先初始化，再初始化子类。
### 7.7.2 super()
super()用来显式调用父类的构造方法；在子类构造方法中写 super()，等价于“先初始化父类部分”。其必须是构造方法的第一行语句，不能出现在构造方法的后面。如果你没有写任何构造方法，编译器会自动生成无参构造器并添加 super()；如果你写了构造方法，但没写 super()，编译器会默认添加对父类无参构造器的调用（前提是父类必须有无参构造器）。
我们可以可以给 super() 传参数，调用父类的有参构造方法：
```Java
public class Creature {
private String name;
public Creature(String aName) {
this.name = aName;
}
public String getName() {
return this.name;
}
}
public class Rabbit extends Creature {
public Rabbit(String name) {
super(name); // ✔️ 调用父类构造器，传入参数
}
}
```
执行：
```Java
Rabbit aRabbit = new Rabbit("Bunny");
System.out.println(aRabbit.getName())
```
输出：
```Java
	Bunny
```
说明参数通过 super(name) 传递给了 Creature 的构造器，完成了继承中的初始化链。
### 7.7.3 this()
用来在一个构造器中调用本类的另一个构造器（即构造器重载之间互相调用）,必须是构造方法的第一行语句。

> 一个构造方法中只能调用 this() 或 super() 其中之一，而且必须是第一条语句，不能同时存在！
|特性|this()|super()|
|---|---|---|
|调用对象|当前类的其他构造器|父类的构造器|
|是否必须第一行|✅ 是|✅ 是|
|是否可以同时使用|❌ 不能！只能选一个||
|编译器行为|会根据 this(...) 跳转|默认添加 super() 如果你没写|
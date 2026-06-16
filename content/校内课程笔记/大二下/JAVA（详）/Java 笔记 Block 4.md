Java 笔记 Block 4
## 12 Math 类
Math 类中不存储任何对象的状态，所有方法都只依赖参数，不依赖对象自身。
Java 的 Math 类构造方法是 private 的，这意味着不能创建 Math 类对象
|方法|功能|输入类型|返回类型|
|---|---|---|---|
|Math.random()|生成 [0.0, 1.0) 的随机值|无|double|
|Math.abs(x)|返回绝对值|int, double 等|同输入类型|
|Math.round(x)|四舍五入|float, double|int or long|
|Math.min(a,b)|返回较小值|多种数值类型|同输入类型|
|Math.max(a,b)|返回较大值|多种数值类型|同输入类型|
|方法|功能|
|---|---|
|Math.sqrt(x)|平方根|
|Math.pow(a, b)|a 的 b 次方|
|Math.log(x)|自然对数（ln）|
|Math.log10(x)|以10为底的对数|
|Math.exp(x)|e 的 x 次方|
|Math.floor(x)|向下取整（不大于 x 的最大整数）|
|Math.ceil(x)|向上取整（不小于 x 的最小整数）|
|Math.toRadians(x)|角度转弧度|
|Math.toDegrees(x)|弧度转角度|
|Math.sin(x) 等|三角函数，参数是弧度|
## 13 Radom类
Random 类的基本用法如下：
```Java
import java.util.Random; // 导入 Random 类
public class RandTest {
public static void main(String[] args) {
Random r = new Random(); // 创建随机数生成器对象
float aRandomFloat = r.nextFloat(); // 生成一个 [0.0, 1.0) 范围的随机浮点数
int aRandomInt = r.nextInt(); // 生成一个任意 int 范围内的随机整数
System.out.println("A random float is " + aRandomFloat);
System.out.println("A random int is " + aRandomInt);
}
}
```
常用 Random 方法：
|方法|返回值类型|说明|
|---|---|---|
|nextInt()|int|任意 int 范围|
|nextInt(int bound)|int|返回 [0, bound) 区间的整数|
|nextFloat()|float|返回 [0.0, 1.0) 间的浮点数|
|nextDouble()|double|返回 [0.0, 1.0) 间的双精度数|
|nextBoolean()|boolean|随机布尔值（true 或 false）|
|nextLong()|long|任意 long 值|
|特性|Math.random()|Random 类|
|---|---|---|
|类型|static 方法|需要创建对象|
|用法|Math.random()|new Random().nextInt() 等|
|默认返回|double [0.0, 1.0)|方法多，返回类型多样|
|可否重复使用同一对象|无（每次调用）|可以重复使用对象，提高效率|
|支持种子设置（for测试复现）|❌ 不支持|✅ 支持（new Random(seed)）|
## 14 Wrapper类
### 14.1 介绍
包装类是 Java 中为每种基本数据类型（primitive type）提供的“对象形式”。它们允许你把一个基本类型（如 int）当作对象来使用。
|基本类型|包装类|
|---|---|
|int|Integer|
|double|Double|
|char|Character|
|boolean|Boolean|
|byte|Byte|
|short|Short|
|long|Long|
|float|Float|
Wrapping（装箱）：把基本类型 → 对象
```Java
int i = 10;
Integer iWrapped = new Integer(i); // 手动装箱
```
现在你就可以把 iWrapped 当作对象使用，比如放进集合里：
```Java
ArrayList<Integer> list = new ArrayList<>();
list.add(iWrapped);
```
Unwrapping（拆箱）：把对象 → 基本类型
```Java
int unWrapped = iWrapped.intValue(); // 拆箱为基本类型
```
每个包装类都有对应的方法：
- intValue()、doubleValue()、charValue()、booleanValue() 等。
### 14.2 Autoboxing/Unboxing
Autoboxing 是指 Java 会自动将基本类型（如 int）转换为对应的包装类（如 Integer）。Unboxing 是反过来：把包装类对象自动转为基本类型。
```Java
ArrayList<Integer> list = new ArrayList<>();
list.add(3); // 自动装箱：int → Integer
int one = list.get(0); // 自动拆箱：Integer → int
```
|场景|Autoboxing|Unboxing|
|---|---|---|
|赋值|Integer i = 1;|int x = i;|
|方法调用|take(Integer i) 可传 int|返回 Integer 可赋值给 int|
|集合操作|list.add(5) 自动转为对象|list.get(0) 可直接赋给 int|
### 14.3 静态方法 parse
包装类（如 Integer, Double, Boolean 等）提供了静态方法来把字符串转换为对应的基本类型，这些方法通常以 parseXxx() 命名。
例如：
```Java
String str1 = "10";
int i = Integer.parseInt(str1); // → 10
String str2 = "123.45";
double d = Double.parseDouble(str2); // → 123.45
String str3 = "true";
boolean b = new Boolean(str3).booleanValue(); // → true
```
解析失败会抛出异常：
```Java
String anotherStr = "ten";
int anotherInt = Integer.parseInt(anotherStr); // ❌ 抛出 NumberFormatException
```
|包装类|方法|说明|
|---|---|---|
|Integer|parseInt(String)|返回 int|
|Double|parseDouble(String)|返回 double|
|Boolean|parseBoolean(String)|返回 boolean（true/false）|
|Long|parseLong(String)|返回 long|
|Float|parseFloat(String)|返回 float|
### 14.4 静态导入 Static Imports
在 Java 中，静态导入允许你直接使用类中的 static 方法或字段，而不需要前缀类名。
如果使用普通语法：
```Java
System.out.println("square root is " + Math.sqrt(4.0));
```
使用静态导入：
```Java
import static java.lang.System.out;
import static java.lang.Math.*;
out.println("square root is " + sqrt(4.0));
```
- System.out 简化为 out
- Math.sqrt(...) 简化为 sqrt(...)
### 14.5 和Number类的关系
所有数值类型的包装类（如 Integer, Double, Float, Long, Short, Byte）都是抽象类 Number 的子类。
我们可以：
```Java
Number num = new Integer(10);
```
- Integer 是 Number 的子类，因此可以用父类类型接收子类对象（多态）；
- 这在需要“统一表示不同数值类型”的地方非常有用，比如泛型集合、通用方法。
去哦们可以使用常量MIN_VALUE 和 MAX_VALUE：
```Java
System.out.println(Long.MIN_VALUE); // -2^63
System.out.println(Integer.MAX_VALUE); // 2147483647
```
这些常量是静态的，可以方便地表示类型的上下界值。
同时，提供了丰富的静态工具方法，用于：
- 不同进制之间转换。
- 从其他类型转换；
- 与 String 互转；
例如：
```Java
int i = 181;
System.out.println("Hex = " + Integer.toHexString(i)); // b5
System.out.println("Binary = " + Integer.toBinaryString(i)); // 10110101
```
## 15 Recursion（递归）和 Iteration（迭代）
|特性|Recursion（递归）|Iteration（迭代）|
|---|---|---|
|基本定义|方法调用自身以解决子问题|使用循环结构（如 for、while）重复执行代码块|
|控制结构|if（用于 base case） + 方法调用|for / while / do-while 循环|
|终止条件（Stopping Condition）|通常是 base case（如 n == 0 或 n == 1）|条件表达式（如 i < n）|
|空间效率（内存）|通常需要更多内存 → 每次调用会用一个新栈帧|通常只用固定量内存（除非使用额外数据结构）|
|速度性能|可能较慢（函数调用开销大），但有时更直观|通常更快，效率高|
|可读性 / 可维护性|对某些问题（如树、图、数学表达式）更自然，代码更短更直观|逻辑简单的问题用迭代往往更清晰|
|适合解决的问题类型|树结构、分治问题、数学定义（如阶乘、斐波那契、汉诺塔）|基本计数、线性搜索、求和等常规过程|
|可能的问题|易出错：若无终止条件或写错 → 可能无限递归（StackOverflowError）|若边界条件写错，可能进入无限循环|
|Java 示例|factorial(n) = n × factorial(n-1)|for (int i = 1; i <= n; i++) result *= i;|
|尾递归优化（某些语言）|支持尾递归优化（Java 不支持）|不适用|
## 16 Exception Handling
### 16.1 介绍
错误的常见原因（Causes of Error Situations）有以下几条：
- 实现错误（Incorrect implementation）例如程序没有按照规范完成：比如逻辑写错、条件判断失误。
- 不合适的对象请求（Inappropriate object request）比如访问一个不存在的数组下标，如 arr[10] 当数组长度只有5。
- 不一致或不恰当的对象状态（Inconsistent object state）通常在类继承、对象初始化不完全、状态未同步等场景下发生。
运行时错误最难处理，原因是：这些错误只有在程序实际运行时才会暴露出来，难以预测和防范。大多数编程语言在语法级别上 并不强制程序员处理异常（例如 C/C++），但 Java 强制你要么处理（catch），要么声明（throws）异常。
Java 的异常机制：构造关键字
Java 程序员应当声明所有可能发生的错误或异常情况（errors or unusual circumstances），这些被声明出来的异常，称为：exceptions。比如：一个方法可能在执行过程中遇到文件找不到的情况，就需要用 throws IO Exception 明确指出这一点。
任何使用包含异常声明的类或方法的代码，有两种选择：
- catch 捕获异常 —— 通过 try-catch 块；
- declare 声明不处理异常 —— 通过 throws 继续往上传递。
旦异常发生且被某个 catch 块捕获（caught）：控制权就会转移到该 catch 块中，在那里可以写代码来处理该异常，比如打印错误信息、关闭资源等。
|功能|关键词|
|---|---|
|检测 & 处理异常|try catch finally|
|抛出 & 声明异常|throw throws|
### 16.2 try/catch/finally
示例组合：
```Java
try {
// open file and read data
} catch (IOException e) {
System.err.println("Error reading file: " + e);
} finally {
// close file stream
}
```
- try { ... } 块：try { ... } 块：保护这段代码执行过程中若出现异常。作用：可以被后面的 catch 块捕获。
- catch (ExceptionType e) { ... } 块：每个 catch 语句块用于处理一个特定类型的异常，以有多个 catch 来分别处理不同的异常类型。作用：报告并从异常中恢复（report and recover）
- finally { ... } 块：无论 try 中是否发生异常，finally 中的代码总会执行。
示例：
```Java
public class TestExceptions {
public static void main(String[] args) {
RiskyClass rc = new RiskyClass();
for (int i = 0; i < args.length; i++) {
try {
rc.checkFileName(args[i]);
} catch (Exception e) {
System.err.println("" + e + " at " + i);
}
}
}
}
```
- 定义类 RiskyClass，其中 checkFileName(String s) 方法可能抛出异常；
- main() 方法从命令行参数中读取多个文件名；
- 每个文件名都通过 try-catch 块处理异常；
- 如果遇到非法文件名，如 /etc/passwd，抛出异常，并输出：
```Java
java.lang.Exception: bad filename at 1
```
### 16.3 Exception类
Java 允许开发者根据自己的需要定义新的异常类型，以增强错误表达能力和程序结构清晰度。本质上和普通类一样（like any other class），但必须继承自 Exception 类。
```Java
public class MyException extends Exception {
// 无参构造方法
public MyException() {
super(); // 调用父类 Exception 的构造方法
// 这里可以加入其他逻辑，如日志记录等
}
// 带字符串参数的构造方法（可传入异常信息）
public MyException(String s) {
super(); // 注意：此处应为 super(s); 传递信息
// 可扩展更多处理逻辑
}
}
```
示例：定义自定义异常类
创建一个 Date 类型的类表示公历（Gregorian calendar）中的日期。如果输入的日期无效（如负数、13月、32日等），就使用自定义异常 InvalidDateException 来处理。
自定义异常类代码：
```Java
public class InvalidDateException extends Exception {
public InvalidDateException() {
super("Invalid date: please try again ...");
}
}
```
- 继承自 Exception；
- 调用父类构造器并传入错误信息；
- 该类用来提示用户日期输入不合法。
类定义：
```Java
public class MyDate {
private int year, month, day;
public MyDate() {
year = 1900;
month = 1;
day = 1;
}
public MyDate(int day, int month, int year) throws InvalidDateException {
setDate(day, month, year);
}
```
- MyDate 类存储年月日；
- 如果构造参数非法，将抛出 InvalidDateException。
setDate(...) 检查并抛出异常：
```Java
public void setDate(int day, int month, int year) throws InvalidDateException {
if (year < 0)
throw new InvalidDateException();
else
this.year = year;
if (month < 0 || month > 12)
throw new InvalidDateException();
else
this.month = month;
if (day < 0 || day > 31)
throw new InvalidDateException();
else
this.day = day;
}
```
- 对输入参数进行基本范围校验；
- 如果无效，立即 throw new InvalidDateException()。
主程序 TestMyDate：
```Java
public class TestMyDate {
public static void main(String[] args) throws InvalidDateException {
MyDate d = new MyDate(10, 11, -1980);
}
}
```
- 向 MyDate 构造函数传入非法年份（负数）；
- 由于 main 方法用 throws 把异常继续往上传递，而没有 try-catch 捕获，程序运行时会崩溃并打印堆栈信息。
程序输出：
```Java
java TestMyDate
Exception in thread "main" InvalidDateException: Invalid date: please try again ...
at MyDate.setDate(MyDate.java:14)
at MyDate.<init>(MyDate.java:10)
at TestMyDate.main(TestMyDate.java:3)
```
- 清晰显示错误发生的位置和异常信息；
- 演示了没有捕获异常时的默认处理方式。
### 16.3 Checked/Unchecked exceptions
- 检查型异常（Checked）：如 IOException，必须用 throws 显式声明或用 catch 捕获。
- 非检查型异常（Unchecked）：如 NullPointerException，是 RuntimeException 的子类，编译器不会强制处理。
## 17 Assertions 断言
断言是 Java 语句，用于在程序中检查一个你认为“应该成立”的条件。表达形式是布尔表达式（Boolean expression）：
```Java
int speed = getSpeed();
assert speed >= 0 : "Speed should never be negative!";//如果断言失败，会java.lang.AssertionError，并显示指定信息。
```
默认情况下 Java 禁用断言，需要在运行时加上 -ea（enable assertions）参数：
```Java
java -ea MyProgram
```
示例：
断言失败（Assertion Fails）
```Java
public class Test {
public static void main(String[] args) {
int i;
int sum = 0;
for (i = 0; i <= 10; i++) {
sum = sum + i;
}
assert (i == 10) : "i is " + i;
}
}
```
- 注意循环条件：i <= 10，所以当循环结束时，i == 11；
- 断言写的是：i == 10，这个是 false；
- 因此触发断言失败，程序抛出：
```Java
	java.lang.AssertionError: i is 11
```
以下代码：
```Java
public class Foo {
public void m1(int value) {
assert 0 <= value;
System.out.println("OK");
}
public static void main(String[] args) {
Foo foo = new Foo();
System.out.print("foo.m1(1): ");
foo.m1(1);
System.out.print("foo.m1(-1): ");
foo.m1(-1);
}
}
```
当运行java –ea Foo时输出：
```Java
foo.m1(1): OK
foo.m1(-1): Exception in thread "main" java.lang.AssertionError
at Foo.m1(Foo.java:3)
at Foo.main(Foo.java:11)
```
## 18 IO
### 18.1 介绍
程序中的数据（变量、数组、对象等）在程序结束后会丢失。如果需要保存这些数据，就需要将它们写入磁盘上的文件。有两种保存数据的方式：
- 序列化（Serialization）：只能被 Java 程序读取；
- 使用文本文件（File）：可以被其他程序读取，例如 Excel 可读取 .csv 文件。
I/O（输入/输出）：
- 输入：程序从外部“读取”数据（例如文件、网络）。
- 输出：程序向外部“写入”数据。
Java 使用 “流（Stream）” 的概念来处理这些输入输出数据。流（Stream） 是一种数据通道，可以从某个地方读取数据（source），也可以向某个地方写入数据（destination）。Java 使用 “流（Stream）” 的概念来处理这些输入输出数据。
Java I/O 机制基于流：
- 可以是输入流（input stream）：从外部读取信息。
- 可以是输出流（output stream）：向外部写出信息。
![image1 6|image1 6.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image1%206.png)
### 18.2 java.io.File类
是一个 Java 标准库中的类，不是用来读写文件内容的，而是表示文件或目录在磁盘中的“路径”和“信息”，相当于一个“文件对象”。
一个完整的文件名由 目录路径（path）+ 文件名（file name） 组成。例如：
```Java
c:\Work\JavaPrograms\MyFirstJavaProgram.java
```
- c:\Work\JavaPrograms\ 是目录路径
- MyFirstJavaProgram.java 是文件名
java.io.File 类的作用：
|方法|作用|
|---|---|
|.exists()|文件是否存在|
|.canRead()|是否可读|
|.canWrite()|是否可写|
|.getAbsolutePath()|获取完整绝对路径|
|.getName()|获取文件名|
|.getPath()|获取路径字符串（构造时的原样）|
特点：
- 是一个包装类（wrapper class），包装了路径信息。
- 它屏蔽了不同操作系统的差异，比如 Windows 用 \，Linux 用 /，但 File 类内部会自动处理。
- 如果你用 new File("something.txt") 创建一个 File 对象，即使文件不存在，也不会报错！因为你只是创建了一个路径引用，而不是实际操作文件。
例子：
```Java
import java.io.File;
public class FileDemo {
public static void main(String[] args) {
File file = new File("myfile.txt");
System.out.println("Exists? " + file.exists()); // 文件是否存在
System.out.println("Is file? " + file.isFile()); // 是不是文件
System.out.println("Can read? " + file.canRead()); // 是否可读
System.out.println("Absolute path: " + file.getAbsolutePath()); // 获取绝对路径
}
}
```
### 18.3 使用 FileReader 和 FileWriter（配合 BufferedReader / BufferedWriter）进行文本文件的读写操作
### 1 介绍
文件操作必须遵守的3个步骤：
- Open file（打开文件）：通过创建流对象来打开文件，如 new FileReader(...)。
- Perform operations（执行操作）：读取：如 .readLine()、.read()；写入：如 .write()、.newLine()。
- Close file（关闭文件）：所有流类都应调用 .close()。注意：文件操作可能抛出异常，应放入 try-catch 中处理。
### 2 读取文本文件
- FileReader: 表示文件对象，用于基础字符读取。
- BufferedReader: 包装 FileReader，提供 readLine() 方法，读取整行文本，效率高。
- 组合使用构成：文本输入流（Text File Input Stream）
提供的方法：
- read()：读一个字符
- read(char[] cbuf)：读一段字符数组
- read(char[], off, len)：读部分字符数组
- close()：关闭流
特点：如果文件不存在，会抛出 FileNotFoundException
例子1：
```Java
import java.io.*; // 导入所有 I/O 相关类，包括 FileReader、BufferedReader、IOException 等
public class FileReadTest { // 定义主类 FileReadTest
public static void main(String args[]){ // 主方法入口
String fileName = "input.txt"; // 定义要读取的文件名
String contents = ""; // 定义字符串用于存储读取结果
try {
FileReader fileReader = new FileReader(fileName); // 创建 FileReader 对象读取字符文件
BufferedReader bufferedReader = new BufferedReader(fileReader); // 包装 FileReader，提高效率
contents = bufferedReader.readLine(); // 读取文本文件中的一行内容（如果有）
bufferedReader.close(); // 关闭 BufferedReader（同时也会关闭底层的 fileReader）
fileReader.close(); // 显式关闭 fileReader（虽然可略写，但更安全）
}
catch (IOException e) { // 捕获所有 IO 异常，包括文件不存在或读取失败
System.out.println("Errors occured"); // 打印错误提示
System.exit(1); // 退出程序
}
System.out.println(contents); // 打印读取到的内容（如果读取成功）
}
}
```
BufferedReader：是一个带缓冲的字符输入流，提供了非常实用的方法：readLine()：一次读取一整行文本，而不是单个字符。如果已经读到文件末尾，readLine() 会返回 null。
例子2：
```Java
// other code ... // 其他代码（可能是变量声明或方法调用等）
int sum = 0; // 初始化 sum 为 0，用于累加整数
String fileName = "input.txt"; // 要读取的文件名为 input.txt
try {
FileReader fileReader = new FileReader(fileName); // 创建 FileReader 从文件读取字符
BufferedReader bufferedReader = new BufferedReader(fileReader); // 用 BufferedReader 包装，支持按行读取
String oneLine = bufferedReader.readLine(); // 读取第一行数据
while (oneLine != null) { // 如果当前行不是 null（即没读到文件结尾）
sum = sum + Integer.parseInt(oneLine); // 将该行转换为整数并加入 sum 总和
oneLine = bufferedReader.readLine(); // 继续读取下一行
}
bufferedReader.close(); // 关闭 BufferedReader 流
fileReader.close(); // 关闭 FileReader 流
}
catch (IOException e) { // 捕获所有 I/O 异常
System.out.println("Errors occured"); // 出错时打印提示
System.exit(1); // 程序退出
}
System.out.println(sum); // 输出所有行数字的总和
// other code ... // 后续代码
```
### 3 写入文本文件
- FileWriter: 表示输出目标文件，基础写入能力。
- BufferedWriter: 包装 FileWriter，提供 write()、newLine() 方法，效率更高。
- 组合使用构成：文本输出流（Text File Output Stream）
提供的方法：
- write(int c)：写一个字符
- write(char[])、write(String)：写多个字符或字符串
- 可传入 append = true 参数选择追加写入
特点：如果文件不存在，会自动创建一个新文件。
例子1：
```Java
// other code ... // 其他代码（比如变量声明）
try {
FileReader fileReader = new FileReader(fileName); // 创建 FileReader，从文件中读取字符
BufferedReader bufferedReader = new BufferedReader(fileReader); // 包装 FileReader，提供 readLine 等高级方法
String oneLine = bufferedReader.readLine(); // 读取文件的第一行
while (oneLine != null) { // 只要还有内容，就继续读取
contents = contents + oneLine; // 把当前行追加到 contents 字符串中（未加换行符）
oneLine = bufferedReader.readLine(); // 读取下一行
}
bufferedReader.close(); // 关闭 BufferedReader（内部也会关闭 FileReader）
fileReader.close(); // 显式关闭 FileReader（多余但安全）
}
// 注意：此处没有 catch 语句块，实际使用建议加上
// other code ... // 后续代码（例如打印内容）
```
BufferedWriter：是一个带缓冲的字符输出流。提供了newLine()：写入一个系统默认的换行符（比如 Windows 是 \r\n，Linux 是 \n）。
例子2：
```Java
// other code ... // 其他代码，比如变量声明、方法调用等
String contents = "Welcome to BUPT."; // 要写入文件的字符串内容
String fileName = "output.txt"; // 目标输出文件名
try {
FileWriter fileWriter = new FileWriter(fileName); // 创建 FileWriter，用于向文件写字符
BufferedWriter bufferedWriter = new BufferedWriter(fileWriter); // 包装 FileWriter，提升效率并支持写行操作
bufferedWriter.write(contents); // 写入字符串到文件中（不会自动换行）
bufferedWriter.close(); // 关闭 BufferedWriter（会自动刷新缓存并关闭底层流）
fileWriter.close(); // 显式关闭 FileWriter（安全做法，即使上面已自动关闭）
}
catch (IOException e) { // 捕获文件写入过程中的任何 I/O 异常
System.out.println("Errors occured"); // 出错时输出提示信息
System.exit(1); // 程序异常退出
}
// other code ... // 后续逻辑代码
```
## 19 Java’s Collection Classes
### 19.1 介绍
Java 中的 Collection 是 “把多个元素组织成一个整体的对象”，可以用来 存储（store）、检索（retrieve）、操作（manipulate） 数据。Java 提供了一套集合框架（Java Collections Framework），包含：
- 接口（interfaces）：定义行为，比如 List、Set 等
- 实现类（implementations）：比如 ArrayList、HashSet 等
- 算法（algorithms）：比如排序、搜索等
![image2 5|image2 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image2%205.png)
- Set：不允许重复元素；是数学上集合的建模。
- List：有序集合，可按下标访问，允许重复；
- Map：用键值对（key-value）存储数据；每个 key 只能对应一个 value；不允许重复 key。
|接口 (Interfaces)|哈希表实现|可变数组实现|树实现|链表实现|哈希表 + 链表实现|
|---|---|---|---|---|---|
|Set|HashSet||TreeSet||LinkedHashSet|
|List||ArrayList||LinkedList||
|Queue||||||
|Deque||ArrayDeque||LinkedList||
|Map|HashMap||TreeMap||LinkedHashMap|
### 19.2 ArrayList
是一个可变长数组（Resizable Array），创建时不需要指定大小：
```Java
ArrayList<String> myArrayList = new ArrayList<String>();
```
可以通过 .add() 方法动态添加元素，不用指定位置：
```Java
anotherArrayList.add(b);
```
|特性|数组（Array）|ArrayList|
|---|---|---|
|长度|固定|可变（自动扩容）|
|类型|基本语法结构|类（在 java.util 中）|
|添加元素|需指定索引|可直接使用 .add()|
|灵活性|较差|更灵活，功能强大|
### 19.3 Map 和 HashMap
Map 是一种 键值对（key-value） 结构的数据容器，用途类似字典（dictionary）或表格中的“索引-值”映射。特点：
- 不能有重复的 key
- 每个 key 对应一个 value
- key 类似“索引”，但不是数字，而是可以是任意对象（如字符串）
HashMap 是 Map 的一个实现类，位于 java.util 包中，作用：快速地插入、删除、查找键值对。特点：
- 查找速度快（基于哈希表）
- 不保证顺序（插入顺序可能与输出顺序不同）
|操作|方法|示例|
|---|---|---|
|添加键值对|put(key, value)|map.put("dog", "Woof");|
|查找值|get(key)|map.get("dog") → “Woof”|
|判断是否有键|containsKey(key)|map.containsKey("cat")|
|删除键值对|remove(key)|map.remove("mouse")|
|键值数量|size()|map.size()|
例子：
```Java
import java.util.*;
public class HashMapTester {
public static void main(String[] args) {
Map<String, String> petSounds = new HashMap<String, String>();
petSounds.put("cat", "Meow");
petSounds.put("mouse", "Squeak");
petSounds.put("dog", "Woof");
petSounds.put("guineaPig", "Squeak");
System.out.println("map = " + petSounds);
String val = petSounds.get("dog");
System.out.println("Value for key 'dog' is: " + val);
}
}
```
- put(key, value)：插入键值对。
- get(key)：根据 key 查找对应的 value。
- System.out.println()：输出整个 map，格式可能是：
```Java
map = {mouse=Squeak, cat=Meow, guineaPig=Squeak, dog=Woof}
Value for key 'dog' is: Woof
```
### 19.4 Enumeration和Iterator
Enumeration 是 Java 中的一个实用接口（utility interface），用于按顺序访问集合中的元素，也就是“枚举”元素。
对列表中的每个元素做某些事情,如：
```Java
Vector<String> v = new Vector<>();
v.add("apple");
v.add("banana");
Enumeration<String> e = v.elements();
while (e.hasMoreElements()) {
System.out.println(e.nextElement());
}
```
|特性|描述|
|---|---|
|功能|遍历集合元素（读取）|
|常用方法（2个）|hasMoreElements()、nextElement()|
|不能用于修改集合|只能读取，不能删除元素|
|代表过去|在 Java 2（JDK 1.2）之前使用较多|
|被谁替代了？|被 Iterator 接口取代（功能更强大）|
Iterator 是一个接口，用于遍历集合（如 ArrayList、HashSet 等）中的元素。它是对 Enumeration 的改进版本，支持泛型、可删除元素，更强大、灵活。
|方法|作用说明|
|---|---|
|hasNext()|判断是否还有下一个元素（返回 true/false）|
|next()|返回下一个元素|
|remove()|删除上一个通过 next() 返回的元素（不是所有集合都支持）|
注意：remove() 方法不是所有集合都支持，某些集合会抛出 UnsupportedOperationException。
例如：
```Java
ArrayList<String> alist = new ArrayList<String>();
// 假设我们已经向 alist 添加了一些字符串
for (Iterator<String> it = alist.iterator(); it.hasNext(); ) {
String s = it.next(); // 获取下一个元素
System.out.println(s); // 打印该元素
}
```
- alist.iterator()：获取 ArrayList 的迭代器。
- it.hasNext()：判断是否还有元素。
- it.next()：获取下一个元素。
|特性|Enumeration|Iterator|
|---|---|---|
|方法数量|2 个（只能读）|3 个（可读可删）|
|可否删除元素？|❌ 不能|✅ 可以（.remove()）|
|是否支持泛型？|❌ 不支持|✅ 支持|
|是否推荐使用？|❌ 不推荐（过时）|✅ 推荐|
### 19.5 二维数组
Java 中的二维数组是“数组的数组”。
- 声明方式：int[][] nums = new int[5][4];意思是有5行，每行是一个含4个整数的数组。
- 声明规则：必须指定第一维（行数）：✅ new int[5][] 是合法的；不能只写空括号：❌ new int[][] 是不合法的。
对象数组的二维数组：比如：Square[][] board = new Square[2][3];是引用的二维数组（数组中每个格子是指向对象的引用）。
![image3 5|image3 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image3%205.png)
![image4 5|image4 5.png](https://pluto-1385601074.cos.ap-beijing.myqcloud.com/img/image4%205.png)
例子1：
```Java
char[][] pic = new char[6][6];
for (int i = 0; i < 6; i++) {
for (int j = 0; j < 6; j++) {
if ((i == j) || (i == 0) || (i == 5))
pic[i][j] = '*';
else
pic[i][j] = '.';
}
}for (int i = 0; i < 6; i++) {
for (int j = 0; j < 6; j++)
System.out.print(pic[i][j]);
System.out.println();
}
```
整个 pic[6][6] 被填充：
- ：当 i==j（对角线），或者在第0行（i==0）或第5行（i==5）
- .：其他位置
最终输出如下：
```Java
****** ← 第0行全是 '*'
.*.... ← 第1行：只有 pic[1][1] 是 '*'
..*... ← 第2行：只有 pic[2][2] 是 '*'
...*.. ← 第3行：只有 pic[3][3] 是 '*'
....*. ← 第4行：只有 pic[4][4] 是 '*'
****** ← 第5行全是 '*'
```
例子2：
```Java
import java.util.ArrayList;
public class TwoDArrayListTester {
public static void main(String[] args) {
// 创建二维 ArrayList
ArrayList<ArrayList<Integer>> topList = new ArrayList<>();
// 初始化每一行（添加3个空的 ArrayList）
for (int i = 0; i < 3; i++) {
topList.add(new ArrayList<Integer>());
}
// 向每个子列表中添加元素：值为 i + j
for (int i = 0; i < 3; i++) {
for (int j = 0; j < 3; j++) {
topList.get(i).add(i + j);
}
}
// 打印二维 ArrayList 的内容
for (int i = 0; i < 3; i++) {
for (int j = 0; j < 3; j++) {
System.out.print(topList.get(i).get(j) + " ");
}
System.out.println();
}
}
}
```
输出结果：
```Java
0 1 2
1 2 3
2 3 4
```
## 20 排序
Java 中可以使用自己实现的排序算法，也可以使用内置的 Collections.sort()。一共提到了三种排序方法：
- 选择排序（Selection Sort）：每次从未排序的部分中找出最大（或最小）值，放到末尾（或开头）。
- 插入排序（Insertion Sort）：把数组分为“已排序”和“未排序”两部分；每次从未排序中取出一个元素，插入到前面的有序部分合适的位置。
- 冒泡排序（Bubble Sort）：重复遍历数组，相邻两个元素比较并交换，把最大的“冒”到最后。
冒泡排序例子：
伪代码：
```Java
boolean changed = true;
do {
changed = false;
for (int j = 0; j < list.length - 1; j++) {
if (list[j] > list[j + 1]) {
swap list[j] with list[j + 1];
changed = true;
}
}
} while (changed);
```
Java具体实现：
```Java
public class BubbleSortDemo {
public static void bubbleSort(double[] list) {
boolean changed = true;
do {
changed = false;
for (int j = 0; j < list.length - 1; j++) {
if (list[j] > list[j + 1]) {
double temp = list[j];
list[j] = list[j + 1];
list[j + 1] = temp;
changed = true;
}
}
} while (changed);
}
public static void main(String[] args) {
double[] arr = {5.0, 4.4, 1.9, 2.9, 3.4, 2.9, 3.5};
bubbleSort(arr);
for (double num : arr) {
System.out.print(num + " ");
}
}
}
```
## 21 Comoarable接口
在面向对象编程（OOP）中，我们也可能需要比较同一个类的对象，我们可以实现Comparable 接口：对象内部实现 compareTo() 方法并定义“自然顺序”（natural order）。
compareTo() 方法介绍（来自 String 类）：
```Java
int compareTo(Object o)
```
返回值解释：
- 0：表示相等；
- < 0：当前对象“小于”被比较对象；
- > 0：当前对象“大于”被比较对象。
使用 Comparable 的关键点：让类实现接口
```Java
class Employee implements Comparable<Employee>
```
- 实现 compareTo() 方法，定义自然顺序（比如根据工资 salary 排序）；
- 只需要实现一个方法，但只能有一个默认排序方式。
在 Java 中，Collections.sort()是定义在java.util.Collections中的静态方法。
这是一个 静态泛型方法：它要求 list 中的元素 T 必须实现 Comparable<T> 接口，会对这个 list 进行就地排序（in-place sort），不会返回新列表，实际排序算法通常是优化后的 MergeSort（归并排序） 或 TimSort（改进版）——这在底层由 Arrays.sort() 配合 Comparable 实现。
例子：
```Java
import java.util.*;
public class Employee implements Comparable<Employee> {
int empID;
String eName;
double salary;
static int i; // 用于自动生成 empID
// 无参构造方法
public Employee() {
empID = i++;
eName = "unknown";
salary = 0.0;
}
// 带参构造方法
public Employee(String name, double sal) {
empID = i++;
eName = name;
salary = sal;
}
// compareTo 方法：按工资比较
public int compareTo(Employee o1) {
if (this.salary == o1.salary) return 0;
else if (this.salary > o1.salary) return 1;
else return -1;
}
// 打印格式
public String toString() {
return "EmpID = " + empID + "\n" +
"Ename = " + eName + "\n" +
"Salary = " + salary;
}
// 主函数进行排序并打印
public static void main(String[] args) {
List<Employee> ts1 = new ArrayList<Employee>();
ts1.add(new Employee("Tom", 40000.00));
ts1.add(new Employee("Harry", 20000.00));
ts1.add(new Employee("Maggie", 50000.00));
ts1.add(new Employee("Chris", 70000.00));
Collections.sort(ts1); // 根据 compareTo 排序
for (Employee emp : ts1) {
System.out.println(emp + "\n");
}
}
}
```
输出：
```Java
EmpID = 1
Ename = Harry
Salary = 20000.0
EmpID = 0
Ename = Tom
Salary = 40000.0
EmpID = 2
Ename = Maggie
Salary = 50000.0
EmpID = 3
Ename = Chris
Salary = 70000.0
```
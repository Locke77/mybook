### 1. java语言概述

名词解释:

JDK(java development kit) java开发工具包 

JRE(java runtime environment) java运行时环境

JVM(java virtual machine) java虚拟机

**java语言的主要特性:**

* 面向对象
  * 两个基本概念：类、对象
  * 三大特性：封装、继承、多态
* 健壮性
  * 吸收了C/C++语言的优点，但去掉了其影响程序健壮性的部分（如指针、内存的申请与释放等），提供了一个相对安全的内存管理和访问机制
* 跨平台性
  * 跨平台性：通过Java语言编写的应用程序在不同的系统平台上都可以运行。“Write once , Run Anywhere”
  * 原理：只要在需要运行 java 应用程序的操作系统上，先安装一个Java虚拟机 (JVM Java Virtual Machine) 即可。由JVM来负责Java程序在该系统中的运行。

**public class 的类名必须与文件名一致 **

JVM主要内存区域:

每个线程专有: 程序计数器, Java虚拟机栈

本地方法栈

所有线程公用: 堆内存, 方法区(永久代), 直接内存(NIO使用)

在jdk1.8中移除整个永久代，取而代之的是一个叫元空间（Metaspace）的区域

[参考资料](https://www.cnblogs.com/jiyukai/p/6665199.html)

[参考资料2](https://www.cnblogs.com/ityouknow/p/5610232.html)

### 2. 基本语法

#### 2.1 关键字 & 标识符

* 关键字：被Java语言赋予了特殊含义，用做专门用途的字符串（单词）

* 保留字：

* 标识符：凡是自己可以起名字的地方都叫标识符

* 命名的规则：（一定要遵守，不遵守就会报编译的错误）
  由26个英文字母大小写，0-9 ，_或 $ 组成  
  数字不可以开头。
  不可以使用关键字和保留字，但能包含关键字和保留字。
  Java中严格区分大小写，长度无限制。
  标识符不能包含空格。

* Java中的名称命名规范：（不遵守，也不会出现编译的错误）
  包名：多单词组成时所有字母都小写：xxxyyyzzz
  类名、接口名：多单词组成时，所有单词的首字母大写：XxxYyyZzz
  变量名、方法名：多单词组成时，第一个单词首字母小写，第二个单词开始每个单词首字母大写：xxxYyyZzz
  常量名：所有字母都大写。多单词时每个单词用下划线连接：XXX_YYY_ZZZ

#### 2.2 变量

* 变量的分类

  存在的位置的不同：成员变量（属性、 Field） (存在于类内部，方法体的外部)和局部变量(方法体的内部、构造器的内部、代码块的内部、方法体或构造器的形参部分) 

数据类型的不同：
基本数据类型（8 种)
整型： byte(1 个字节)、 short(2个字节)、 int（默认值类型, 4个字节）、 long（后缀是 l 或 L, 8个字节）。
浮点型： float（后缀是 f 或 F, 4个字节）和 double（默认值类型, 8个字节）。
布尔型： boolean （只有两个值： true 和 false，绝对不会取值为 null）
字符型： char（1 个字符, 占2个字节）
引用数据类型： 类（比如： String 字符串类型）、接口、数组 

* 变量的声明, 初始化, 与作用域

* 自动类型转化&强制类型转化（重点）（不包含 boolean 型，及 String 型）
  强制类型转化时，可能会损失精度。
  
* 进制
  进制之间的转化：
  会将-128 到 127 范围内的十进制转化为二进制 & 能将一个二进制数转换为十
  进制数（延伸：十进制、二进制、八进制、十六进制）

  对于几类基本类型的数据的某个具体值，能够用二进制来表示。同时，如果给
  出一个数据的二进制，要能够会
  转化为十进制！
  正数：原码、反码、补码三码合一。
  负数：原码、反码、补码的关系。**负数在计算机底层是以补码的形式存储的**

#### 2.3 运算符

算术运算符
赋值运算符
比较运算符（关系运算符） 

逻辑运算符
“&”和“&&”的区别： &：当左端为 false 时，右端继续执行
&&：当左端为 false 时，右端不再执行

“|”和“||”的区别： |：当左端为 true 时，右端继续执行
||：当左端为 true 时，右端不再执行

位运算符(不存在<<<)
<< 左移    >> 右移    >>> 无符号右移       & 与     | 或      ^异或     ~取反

三元运算符 
(条件表达式)? a : b
当表达式为true时, 运算后的结果为a, 当表达式的结果为false时, 运算后的结果为b; 
三元运算符与 if-else 语句的联系
1）三元运算符可以简化 if-else 语句
2）三元运算符一定要返回一个结果。结果的类型取决于表达式 1 和 2 的类
型。（表达式 1 和 2 是同种类型的）
3） if-else 语句的代码块中可以有多条语句。 

#### 2.4 流程控制

顺序结构

分支结构

if - else  

if - else if - else

switch  case

循环结构

for   while   do-while(程序至少执行一次)

#### 2.5 关键字： break & continue 

* break
  1.使用范围：循环结构或 switch-case 结构中。
  2.在循环结构中：一旦执行到 break，代表结束当前循环。

* continue
  1.使用范围：循环结构
  2.在循环结构中：一旦执行到 continue,代表结束当次循环。
  相同点：如果 break 或 continue 后面还有代码，那么这些代码将不会被执行。所
  以当有代码，编译会出错！

* 使用标签，实现结束指定“层次”的循环。

#### 2.6 数组

数组的声明： int[] i ; String[] str; Animal[] animal;
数组的初始化：
①动态初始化： i = new int[4]; //i[0]开始，至 i[3]结束。默认初始化值都为 0;
i[0] = 12;i[1] = 34;....
②静态初始化： str = new String[]{"北京","尚硅谷","java0715 班"};
//也是先有默认初始化赋值，然后显示的初始化，替换原来的默认初始化值
//对于引用数据类型来说，默认初始化值为 null。
//对于基本数据类型来说: byte、short、int ：0 long :0L float : 0.0F double :
0.0 char :'\u0000' boolean : false 引用类型： null 

二维数组

数组常用的算法：最大值、最小值、和、平均数、 排序（涉及数据结构中各
种排序算法）、复制、反转。 

面试前看一看排序, [文件夹](file:D:\Study\B_Java学习视频\01尚硅谷20天java核心技术教程\尚硅谷_宋红康_JavaSE课件\尚硅谷_宋红康_第2章_基本语法)

### 3. 面向对象

1.（了解） 面向对象  vs 面向过程   例子：人开门；把大象装冰箱

2.面向对象的编程关注于类的设计！
1）一个项目或工程，不管多庞大，一定是有一个一个类构成的。
2）类是抽象的，好比是制造汽车的图纸。
     而具体的一辆一辆的车，是根据图纸制造的，实际上就是类的实例化

3.完成一个项目（或功能）的思路
1）所要完成的功能对应的类的对象是否存在。
2）若存在，则通过对象直接调用对应的类中的属性或方法即可
3）若不存在，需要创建类的对象。甚至说，类都不存在，就需要设计类。

4.面向对象编程的三条主线：
1）类及类的构成成分：属性  方法 构造器  代码块 内部类
2）面向对象编程的特征：封装性  继承性 多态性  （抽象性）
3）其它的关键字：this super package import static final abstract interface ...

#### 3.1 类及对象

1.关于于类的设计

2.类的组成成分：
   1） 属性（成员变量，Field）
   2）方法（成员方法，函数，Method）

2.1属性：
    成员变量 vs 局部变量

相同点：1.遵循变量声明的格式： 数据类型 变量名 = 初始化值

​		2.都有作用域

不同点：1.声明的位置的不同 ：成员变量：声明在类里，方法外

​		局部变量：声明在方法内，方法的形参部分，代码块内

​		2.成员变量的修饰符有四个：public private protected 缺省

​		局部变量没有修饰符，与所在的方法修饰符相同。

​		3.初始化值：一定会有初始化值。

​		成员变量:如果在声明的时候，不显式的赋值，那么不同数据类型会有不同的默认初始化值。

​		byte short int long ==>0

​		float double ==>0.0

​		char ==>空格

​		boolean ==>false 

​		引用类型变量==>null

​		局部变量：一定要显式的赋值。（局部变量没有默认初始化值）

​		4.二者在内存中存放的位置不同:成员变量存在于堆空间中；局部变量：栈空间中

总结：关于变量的分类：1）按照数据类型的不同：基本数据类型（8种）  & 引用数据类型

​					2）按照声明的位置的不同：成员变量 & 局部变量

2.2 方法：提供某种功能的实现

1）实例：public void eat(){//方法体}

public String getName(){}

public void setName(String n){}

格式：权限修饰符 返回值类型（void:无返回值/具体的返回值） 方法名(形参){}

2)关于返回值类型：void：表明此方法不需要返回值

有返回值的方法：在方法的最后一定有return + 返回值类型对应的变量

记忆：void 与return不可以同时出现一个方法内。像一对“冤家”。

3)方法内可以调用本类的其他方法或属性，但是不能在方法内再定义方法！


3.面向对象编程的思想的落地法则一：
1）设计并创建类及类的成分
2）实例化类的对象
3）通过“对象.属性”或"对象.方法"的形式完成某项功能

4.类的初始化的内存解析
4.1  内存划分的结构：
      栈(stack):局部变量 、对象的引用名、数组的引用名
      堆(heap):new 出来的“东西”（如：对象的实体，数组的实体），含成员变量
      方法区:含字符串常量
      静态域：声明为static的变量

4.2 理解的基础上，学会基本的创建的类的对象在内存中的运行。

#### 3.2 方法的重载

方法的重载（overload）

要求：1.同一个类中 2.方法名必须相同 3.方法的参数列表不同（①参数的个数不同②参数类型不同）

补充：方法的重载与方法的返回值类型没有关系！

//如下的四个方法构成重载
//定义两个int型变量的和
public int getSum(int i,int j){
	return i + j;
}
//定义三个int型变量的和
public int getSum(int i,int j,int k){
	return i + j + k;
}
//定义两个double型数据的和
public double getSum(double d1,double d2){
	return d1 + d2;
}

//定义三个double型数组的和
public void getSum(double d1,double d2,double d3){
	System.out.println(d1 + d2 + d3);
}
//不能与如上的几个方法构成重载
//	public int getSum1(int i,int j,int k){
//		return i + j + k;
//	}
//	public void getSum(int i,int j,int k){
//		System.out.println(i + j + k);
//	}

//以下的两个方法构成重载。
public void method1(int i,String str){
	
}
public void method1(String str1,int j){
	
}

#### 3.3 可变个数形参的方法

可变个数的形参的方法：

1.格式：对于方法的形参： 数据类型 ... 形参名

2.可变个数的形参的方法与同名的方法之间构成重载

3.可变个数的形参在调用时，个数从0开始，到无穷多个都可以。

4.使用可变多个形参的方法与方法的形参使用数组是一致的。

5.若方法中存在可变个数的形参，那么一定要声明在方法形参的最后。

6.在一个方法中，最多声明一个可变个数的形参。


```java 
//如下四个方法构成重载
//在类中一旦定义了重载的可变个数的形参的方法以后，如下的两个方法可以省略
//	public void sayHello(){
//		System.out.println("hello world!");
//	}
//	public void sayHello(String str1){
//		System.out.println("hello " + str1);
//	}
//可变个数的形参的方法
	public void sayHello(String ... args){
		for(int i = 0;i < args.length;i++){
			System.out.println(args[i] + "$");
		}
		//System.out.println("=====");
	}

	public void sayHello(int i,String ... args){
	//public void sayHello(String ... args,int i){
		System.out.println(i);
		for(int j = 0;j < args.length;j++){
		System.out.println(args[j] + "$");
	}
}
public void sayHello1(String[] args){
	for(int i = 0;i < args.length;i++){
		System.out.println(args[i]);
	}
}
```

 

#### 3.4 java的值传递机制

​	方法的参数传递（**重点、难点**）


 * 形参：方法声明时，方法小括号内的参数

 * 实参：调用方法时，实际传入的参数的值

   

   规则：java中的参数传递机制：值传递机制

 * 1）形参是基本数据类型的：将实参的值传递给形参的基本数据类型的变量

 * 2）形参是引用数据类型的：将实参的引用类型变量的值（对应的堆空间的对象实体的首地址值）传递给形参的引用类型变量。

#### 3.5 构造器

一、类的第三个成员：构造器(constructor 构造方法)   construction  CCB  ICBC   oop

constructor:建造者 

构造器的作用：①创建对象 ②给创建的对象的属性赋值



1.设计类时，若不显式声明类的构造器的话，程序会默认提供一个空参的构造器.

2.一旦显式的定义类的构造器，那么默认的构造器就不再提供。

3.如何声明类的构造器。格式：权限修饰符  类名(形参){ }

4.类的多个构造器之间构成重载

二、类对象的属性赋值的先后顺序：①属性的默认初始化 ②属性的显式初始化  2.5 代码块 ③通过构造器给属性初始化

④通过"对象.方法"的方式给属性赋值

#### 3.6 this关键字

this：
1.使用在类中，可以用来修饰属性、方法、构造器
2.表示当前对象或者是当前正在创建的对象
3.当形参与成员变量重名时，如果在方法内部需要使用成员变量，必须添加this来表明该变量时类成员
4.在任意方法内，如果使用当前类的成员变量或成员方法可以在其前面添加this，增强程序的阅读性
5.在构造器中使用“this(形参列表)”显式的调用本类中重载的其它的构造器
   >5.1 要求“this(形参列表)”要声明在构造器的首行！
   >5.2 类中若存在n个构造器，那么最多有n-1构造器中使用了this。

#### 3.7 package&import

package:声明源文件所在的包，写在程序的第一行。

每“.”一次，表示一层文件目录。

包名都要小写。

import:

1)显式导入指定包下的类或接口

2)写在包的声明和源文件之间

3)如果需要引入多个类或接口，那么就并列写出

4)如果导入的类是java.lang包下的，如：System String Math等，就不需要显式的声明。

5)理解.*的概念。比如java.util.*;

6)如何处理同名类的导入。如：在util包和sql包下同时存在Date类。

**7)import static 表示导入指定类的static的属性或方法**

8)导入java.lang.*只能导入lang包下的所有类或接口，不能导入lang的子包下的类或接口

### 4. 面向对象(二) 继承性

* 通过"class A extends B"类实现类的继承。

子类：A  父类（或基类 SuperClass）：B

* 子类继承父类以后，父类中声明的属性、方法，子类就可以获取到。

明确：当父类中有私有的属性或方法时，子类同样可以获取得到，只是由于封装性的设计，使得子类不可以直接调用罢了。

子类除了通过继承，获取父类的结构之外，还可以定义自己的特有的成分。

extends：子类是对父类功能的“扩展”，明确子类不是父类的子集。

* java中类的继承性只支持单继承：一个类只能继承一个父类。反之，一个父类可以有多个子类。

* 子父类是相对的概念。


#### 4.1 方法的重写

方法的重写   

1.前提：有子类继承父类

2.子类继承父类以后，若父类的方法对子类不适用，那么子类可以对父类的方法重写(override overwrite)、覆盖、覆写。

3.重写的规则：  1)要求子类方法的“返回值类型 方法名 （参数列表）”与父类的方法一样

2)子类方法的修饰符不能小于父类方法的修饰符

3)*若父类方法抛异常，那么子类方法抛的异常类型不能大于父类的。

4)*子父类的方法必须同为static或同为非static的。

* **方法的重载与重写的区别？**
  重载：“两同一不同”：同一个类，同一个方法名，不同的参数列表。 注：方法的重载与方法的返回值无关！
           >构造器是可以重载的
  重写：（前提：在继承的基础之上，子类在获取了父类的结构以后，可以对父类中同名的方法进行“重构”）
          方法的返回值，方法名，形参列表形同；权限修饰符不小于父类的同名方法；子类方法的异常类型不大于父类的；
          两个方法要同为static或同为非static。



#### 4.2关键字super

1.super，相较于关键字this，可以修饰属性、方法、构造器

2.super修饰属性、方法：在子类的方法、构造器中，通过super.属性或者super.方法的形式，显式的调用父类的指定
属性或方法。尤其是，当子类与父类有同名的属性、或方法时，调用父类中的结构的话，一定要用“super.”

3.通过“super(形参列表)”，显式的在子类的构造器中，调用父类指定的构造器！

  >任何一个类(除Object类)的构造器的首行，要么显式的调用本类中重载的其它的构造器“this(形参列表)”或显式的调用父类中
  >指定的构造器“super(形参列表)”,要么默认的调用父类空参的构造器"super()"
  >建议在设计类时，提供一个空参的构造器！
  >
  >构造器中super(形参) 和this(形参)都必须写在首行, 因此super和this在构造器中不能同时出现

#### 4.3 子类对象实例化的全过程

当jvm加载子类时, 会首先执行父类的静态代码块, 然后执行子类的静态代码块 (静态代码块只会在类加载的时候执行一次); 然后创建对象时, 会优先调用父类的代码块, 然后调用父类的构造方法, 再调用子类的代码块, 子类的构造方法.

``` java
public class CSuper {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.setAge(10);
        d.setName("小明");
        d.setHostName("花花");
        System.out.println("name:" + d.getName() + " age:" + d.getAge()
                + "hostName:" + d.getHostName());
        System.out.println(d.toString());
        new Dog();
    }
}
// 生物
class Creator {
    private int age;
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    public Creator() {
        super();
        System.out.println("this is Creator's constructor");
    }
    static {
        System.out.println("this is Creator's static block.");
    }
    {
        System.out.println("this is Creator's block.");
    }
}
// 动物类
class Animal extends Creator {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public Animal() {
        super();
        System.out.println("this is Animal's constructor");
    }
    static {
        System.out.println("this is Animal's static block.");
    }
    {
        System.out.println("this is Animal's block.");
    }
}
// 狗
class Dog extends Animal {
    private String hostName;
    public String getHostName() {
        return hostName;
    }
    public void setHostName(String hostName) {
        this.hostName = hostName;
    }
    public Dog() {
        super();
        System.out.println("this is Dog's constructor");
    }
    static {
        System.out.println("this is Dog's static block.");
    }
    {
        System.out.println("this is Dog's block.");
    }
}
```

#### 4.4 面向对象特征三----多态

1.多态性的表现：①方法的重载与重写   ②子类对象的多态性
2.使用的前提：①要有继承关系 ②要有方法的重写
3.格式：Person p = new Man();//向上转型
            // 虚拟方法调用：通过父类的引用指向子类的对象实体，当调用方法时，实际执行的是子类重写父类的方法
	    p1.eat();
	    p1.walk();
	   // p1.entertainment();
	
4.程序运行分为编译状态和运行状态。
 * 对于多态性来说，编译时，"看左边"，将此引用变量理解为父类的类型

 * 运行时，"看右边",关注于真正对象的实体：子类的对象。那么执行的方法就是子类重写的。

   编译时，认为p是Person类型的，故只能执行Person里才有的结构，即Man里特有的结构不能够调用

* 子类对象的多态性，并不使用于属性。

5.关于向下转型：
   ①向下转型,使用强转符：()
   ②为了保证不报ClassCastException，最好在向下转型前，进行判断： instanceof
// 若a是A类的实例，那么a也一定是A类的父类的实例。
if (p1 instanceof Woman) {
	System.out.println("hello!");
	Woman w1 = (Woman) p1;
	w1.shopping();
}

if (p1 instanceof Man) {
	Man m1 = (Man) p1;
	m1.entertainment();
}

#### object类

1.java.lang.Object 类，是所有类的根父类！

2.Object类仅有一个空参的构造器  public Object(){  }

3.关于方法：
  ① equals(Object obj)

```java
public boolean equals(Object obj) {
        return (this == obj);
}
```

// 1.基本数据类型：根据基本数据类型的值判断是否相等。相等返回true，反之返回false
// 注：两端数据类型可以不同，在不同的情况下，也可以返回true(例如1和1.0相等)。
// 2.引用数据类型：比较引用类型变量的地址值是否相等。
//equals():

>①只能处理引用类型变量②在Object类，发现equals()仍然比较的两个引用变量的地址值是否相等
>像String 包装类 File类 Date类这些重写Object类的equals()方法，比较是两个对象的
>//"实体内容"是否完全相同。
>若我们自定义一个类，希望比较两个对象的属性值都相同的情况下返回true的话，就需要重写Object类的
> equals(Object obj)方法

② toString()方法
当我们输出一个对象的引用时，会调用toString()方法。
1.

```java
public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

当我们没有重写Object类的toString()方法时，打印的就是对象所在的类，以及对象实体在堆空间的位置
2.一般我们需要重写Object类的toString()方法，将此对象的各个属性值返回。
3.像String类、Date、File类、包装类都重写了toString()方法。

### 5. 面向对象(三)

#### 5.1 static关键字

 1.static:静态的，可以用来修饰属性、方法、*代码块（或初始化块）、*内部类

2. static修饰属性（类变量）:

 * 1.由类创建的所有的对象，都共用这一个属性

 * 2.当其中一个对象对此属性进行修改，会导致其他对象对此属性的一个调用。vs 实例变量（非static修饰的属性，各个对象各自拥有一套副本）

 * 3.类变量随着类的加载而加载的，而且独一份

 * 4.静态的变量可以直接通过“类.类变量”的形式来调用

 * 5.类变量的加载是要早于对象。所以当有对象以后，可以“对象.类变量”使用。但是"类.实例变量"是不行的。

 * 6.类变量存在于静态域中。

   

   static修饰方法（类方法）:

 * 1.随着类的加载而加载，在内存中也是独一份

 * 2.可以直接通过“类.类方法”的方式调用

 * 3.内部可以调用静态的属性或静态的方法，而不能调用非静态的属性或方法。反之，非静态的方法是可以调用静态的属性或静态的方法

 * **静态的方法内是不可以有this或super关键字的！**

 * 注：静态的结构(static的属性、方法、代码块、内部类)的生命周期要早于非静态的结构，同时被回收也要晚于非静态的结构

#### 单例模式

单例模式：
解决的问题：如何只让设计的类只能创建一个对象
如何实现：饿汉式  &  懒汉式

```java
//饿汉式1
class Bank{
	//1.私有化构造器
	private Bank(){}
	//2.创建类的对象，同时设置为private的，通过公共的来调用，体现封装性
	//4.要求此对象也为static的
	private static Bank instance = new Bank();
	//3.此公共的方法，必须为static 
	public static Bank getInstance(){
		return instance;	
	}
}

//饿汉式2
class Bank{
	//1.私有化构造器
	private Bank(){}
	//2.创建类的对象，同时设置为private的，通过公共的来调用，体现封装性
	//4.要求此对象也为static的
	private static Bank instance = null;
	static{
		instance  = new Bank();	
	}
	//3.此公共的方法，必须为static 
	public static Bank getInstance(){
		return instance;	
	}
}

//懒汉式
class Bank{
	private Bank(){}	
	private static Bank instance = null;
	public static Bank getInstance(){
	if(instance == null){//可能存在线程安全问题的！
		instance = new Bank();		
	}	
	return instance;
}
}
```

#### 代码块

代码块：是类的第4个成员
作用：用来初始化类的属性
分类：只能用static来修饰。

​	**静态代码块**：

* 1.里面可以有输出语句

 * 2.随着类的加载而加载，而且只被加载一次

 * 3.多个静态代码块之间按照顺序结构执行

 * 4.静态代码块的执行要早于非静态代码块的执行。

 * 5.静态的代码块中只能执行静态的结构(类属性，类方法)

   

   **非静态代码块：**

 * 1.可以对类的属性(静态的 & 非静态的)进行初始化操作，同时也可以调用本类声明的方法(静态的 & 非静态的)

 * 2.里面可以有输出语句

 * 3.一个类中可以有多个非静态的代码块，多个代码块之间按照顺序结构执行

 * 4.每创建一个类的对象，非静态代码块就加载一次。

 * 5.非静态代码块的执行要早于构造器

   

   **关于属性赋值的操作：**
   ①默认的初始化
   ②显式的初始化或代码块初始化(此处两个结构按照顺序执行) 
   ③构造器中；
   —————————以上是对象的属性初始化的过程—————————————
   ④通过方法对对象的相应属性进行修改

#### 抽象 abstract

abstract：抽象的，可以用来修饰类、方法

1.abstract修饰类：抽象类

​	1)不可被实例化

​	2)抽象类有构造器 (凡是类都有构造器)

​	3)抽象方法所在的类，一定是抽象类。

​	4)抽象类中可以没有抽象方法。

当我们设计一个类，不需要创建此类的实例时候，就可以考虑将其设置为抽象的，由其子类实现这个类的抽象方法以后，就行实例化



2.abstract修饰方法：抽象方法

​	1)格式：没有方法体，包括{}.如：public abstract void eat();

​	2)抽象方法只保留方法的功能，而具体的执行，交给继承抽象类的子类，由子类重写此抽象方法。

​	3)若子类继承抽象类，并重写了所有的抽象方法，则此类是一个"实体类",即可以实例化

​	4)若子类继承抽象类，没有重写所有的抽象方法，意味着此类中仍有抽象方法，则此类必须声明为抽象的！

#### 接口Interface

接口（interface）  是与类并行的一个概念

1.接口可以看做是一个特殊的抽象类。是常量与抽象方法的一个集合(默认带有public static修饰符)，不能包含变量、一般的方法。

2.接口是没有构造器的。

3.接口定义的就是一种功能。此功能可以被类所实现（implements）。

比如：class CC extends DD implements AA

4.实现接口的类，必须要重写其中的所有的抽象方法，方可实例化。若没有重写所有的抽象方法，则此类仍为一个抽象类

5.类可以实现多个接口。----java 中的类的继承是单继承的

6.**接口与接口之间也是继承的关系，而且可以实现多继承**

​         5,6描述的是java中的继承的特点。

7.接口与具体的实现类之间也存在多态性

8.面向接口编程的思想

#### 工厂方法设计模式

#### 代理模式

#### 内部类

类的第5个成员：内部类

1.相当于说，我们可以在类的内部再定义类。外面的类：外部类。里面定义的类：内部类

2.内部类的分类：成员内部类（声明在类内部且方法外的）  vs 局部内部类(声明在类的方法里)

3.成员内部类：

​	3.1是外部类的一个成员：①可以有修饰符（4个）②static final ③可以调用外部类的属性、方法

​	3.2具体类的特点：①abstract ②还可以在其内部定义属性、方法、构造器

4.局部内部类：

5.关于内部类，大家掌握三点：

​	①如何创建成员内部类的对象（如：创建Bird类和Dog类的对象）

​	②如何区分调用外部类、内部类的变量(尤其是变量重名时)

​		重名时可以通过 外部类名点this点属性 例如 People.this.name

​	③局部内部类的使用 （见TestInnerClass1.java）

### 6. 异常处理

**1.体系结构**
   java.lang.Object
           |----java.lang.Throwable
    			|-------java.lang.Error：错误，java程序对此无能为力，不显式的处理
 			|-------java.lang.Exception:异常。需要进行处理
 				|------RuntimeException:运行时异常
					|-----ArrayIndexOutOfBoundsException/NullPointerException/ArithmeticException/ClassCastException
				|------非RuntimeException:编译时异常
				
2.因为java程序分为javac.exe和java.exe两个过程，在每个过程中，都有可能出现异常。故分为编译时异常、运行时异常
  2.1 对于运行时异常比较常见，可以不显式的来处理。
  2.2 对于编译时异常，必须要显式的处理
        编译时异常，不是说有异常才处理，而是存在异常的隐患，必须在编译前，提示程序，万一出现异常，如何处理！

**2.如何处理异常？**
   java 中的“抓抛模型”

1."抛"：当我们执行代码时，一旦出现异常，就会在异常的代码处生成一个对应的异常类型的对象，并将此对象抛出。(自动抛出   / 手动抛出)

 * 一旦抛出此异常类的对象，那么程序就终止执行

 * 此异常类的对象抛给方法的调用者。

   2."抓"：抓住上一步抛出来的异常类的对象。如何抓？即为异常处理的方式

   java 提供了两种方式用来处理一个异常类的对象。



**处理的方式一：**

   ```java
   try{
   
   //可能出现异常的代码
   
   }catch(Exception1 e1){
   
   //处理的方式1
   
   }catch(Exception2 e2){
   
   //处理的方式2
   
   }finally{
   
   //一定要执行的代码 
   
   }
   ```

   注：1.try内声明的变量，类似于局部变量，出了try{}语句，就不能被调用

   ​	2.finally是可选的。

   ​	3.catch语句内部是对异常对象的处理：

   ​			getMessage();  printStackTrace();

   4.可以有多个catch语句，try中抛出的异常类对象从上往下去匹配catch中的异常类的类型，一旦满足就执行catch中的代码。执行完，就跳出其后的多条catch语句

   5.如果异常处理了，那么其后的代码继续执行。

   6.若catch中多个异常类型是"并列"关系，孰上孰下都可以。若catch中多个异常类型是"包含"关系，须将子类放在父类的上面，进行处理。否则报错！

   7.finally中存放的是一定会被执行的代码，不管try中、catch中是否仍有异常未被处理，以及是否有return语句。

   8.try-catch是可以嵌套的。

   

   **处理方式二：**

在方法的声明处，显式的使用throws + 异常类型

   ```java
    public void method1()  throws Exception1 e1,Exception2 e2{
   	//可能出现异常（尤其是编译时异常，一定要处理）
    }
   public void method2() throws Exception1 e1,Exception2 e2{
   	method1();
   }
    public void method3(){
   try{
   	method2();
    }catch(Exception1 e1){
   	System.out.println(e1.getMessage());    
   }catch(Exception2 e2){
   	System.out.println(e2.getMessage());    
   }
    }
   public static void main(String[] args){
   对象1.method3();//不会再出现上述的Exception1和Exception2的异常！
   }
   ```

   

   **3.如何手动的抛出一个异常？**
   在方法的内部，可以使用  throw + 异常类对象，来手动的抛出一个异常！

```java
 //比较两个圆的半径的大小。
   public int compareTo(Object obj) throws Exception{
   	if(this == obj){
   		return 0;
   	}
   	else if(obj instanceof Circle){
   		Circle c = (Circle)obj;
   		if(this.radius > c.radius){
   			return 1;
   		}else if(this.radius == c.radius){
   			return 0;
   		}else{
   			return -1;
   		}
   	}else{
   		//return -2;
   		//手动的抛出一个异常
   		//throw new Exception("传入的类型有误！");
   		//throw new String("传入的类型有误！");
   		throw new MyException("传入的类型有误！");
   	}
   }
```


   **4.如何自定义一个异常类？**

手动的抛出一个异常，除了抛出的是现成的异常类的对象之外，还可以抛出一个自定义的异常类的对象！
如何自定义一个异常类呢？

```java
//1.自定义的异常类继承现有的异常类
//2.提供一个序列号，提供几个重载的构造器
public class MyException extends Exception{
	static final long serialVersionUID = -70348975766939L;
	public MyException(){}
	public MyException(String msg){
		super(msg);
	}
}
```

**finally一定会执行, 如果try或者catch里有return 会在return前执行, 如果finally里return了, 则直接跳出了方法不会再去执行try和catch里的return了.**

```java
public class TestFinally {
	public static void main(String[] args) {
		int i = method1();
		System.out.println(i);
	}	
	public static int method1(){
		try{
			System.out.println(10/0);
			return 1;			
		}catch(Exception e){
			e.printStackTrace();
			return 3;
		}finally{
			System.out.println("我是帅哥！");
			return 2;
		}
	}	
}
```

上面的方法返回值是2, 而不是1或者3.

**5. “5个关键字搞定异常处理！”  其中，要区分：throw与throws的区别？**

### 7. 集合

1.对象的存储：①数组（基本数据类型  & 引用数据类型）  ②集合（引用数据类型）
    >数组存储数据的弊端：长度一旦初始化以后，就不可变；真正给数组元素赋值的个数没有现成的方法可用。
2.集合框架
**Collection接口** ：

​	方法：

​		①add(Object obj),addAll(Collection coll),size(),clear(),isEmpty();
​		②remove(Object obj),removeAll(Collection coll),retainAll(Collection coll),equals(Object obj),contains(Object obj) containsAll(Collection coll),hashCode()
​		③ iterator(),toArray();

|------List接口：存储有序的，可以重复的元素.---相当于“动态”数组
		新增的方法：删除remove(int index) 修改set(int index,Object obj) 获取get(int index)插入add(int index,Object obj)
		添加进List集合中的元素（或对象）所在的类一定要重写equals()方法

​	|------ArrayList（主要的实现类）
​	|------LinkedList（更适用于频繁的插入、删除操作）
​	|------Vector（古老的实现类、线程安全的，但效率要低于ArrayList）

|------Set接口：存储无序的，不可重复的元素。---相当于高中的“集合”概念

​		Set使用的方法基本上都是Collection接口下定义的。

​		添加进Set集合中的元素所在的类一定要重写equals() 和 hashCode()。要求重写equals() 和 hashCode()方法保持一致。
​		1.无序性：无序性！= 随机性。真正的无序性，指的是元素在底层存储的位置是无序的。
​		2.不可重复性：当向Set中添加进相同的元素的时候，后面的这个不能添加进去。

​	|------HashSet（主要的实现类）
​	|------LinkedHashSet(是HashSet的子类，当我们遍历集合元素时，是按照添加进去的顺序实现的；频繁的遍历，较少的添加、插入操作建议选择此)
​	|------TreeSet（可以按照添加进集合中的元素的指定属性进行排序）
​		要求TreeSet添加进的元素必须是同一个类的！
​		两种排序方式：自然排序：①要求添加进TreeSet中的元素所在的类implements Comparable接口
​							②重写compareTo(Object obj)，在此方法内指明按照元素的哪个属性进行排序
​							③向TreeSet中添加元素即可。若不实现此接口，会报运行时异常
​					定制排序：①创建一个实现Comparator接口的实现类的对象。在实现类中重写Comparator的compare(Object o1,Object o2)方法
​							②在此compare()方法中指明按照元素所在类的哪个属性进行排序
​							③将此实现Comparator接口的实现类的对象作为形参传递给TreeSet的构造器中
​							④向TreeSet中添加元素即可。若不实现此接口，会报运行时异常
​		要求重写的compareTo()或者compare()方法与equals()和hashCode()方法保持一致。
**Map接口**：存储“键-值”对的数据 

key是不可重复的，使用Set存放。value可以重复的，使用Collection来存放的。一个key-value对构成一个entry(Map.Entry)，entry使用Set来存放。
添加、修改 put(Object key,Object value)  删除remove(Object key)  获取get(Object key) size() / keySet() values()  entrySet()

|-----HashMap：主要的实现类，可以添加null键，null值
      	|-----LinkedHashMap：是HashMap的子类，可以按照添加进Map的顺序实现遍历
      	|-----TreeMap：需要按照key所在类的指定属性进行排序。要求key是同一个类的对象。对key考虑使用自然排序 或 定制排序
      	|-----Hashtable：是一个古老的实现类，线程安全的，不可以添加null键，null值不建议使用。
      		|-----子类：Properties：常用来处理属性文件

Iterator接口：用来遍历集合Collection元素

Collections工具类：操作Collection及Map的工具类，大部分为static的方法。

附：Properties的使用
Properties pros = new Properties();
		pros.load(new FileInputStream(new File("jdbc.properties")));
		String user = pros.getProperty("user");
		System.out.println(user);
		String password = pros.getProperty("password");
		System.out.println(password);				
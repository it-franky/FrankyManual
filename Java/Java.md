[TOC]

# References

- 纸质书：《Java核心技术 卷I》 《Java核心技术 卷II》 《Java编程思想》

- 视频 ：马士兵Java基础

- Java知识体系图


# 环境

## JDK安装

JDK是 Java 语言的软件开发工具包，主要用于移动设备、嵌入式设备上的java应用程序。JDK是整个java开发的核心，它包含了JAVA的运行环境，JAVA工具和JAVA基础的类库。

下载安装JDK，选择安装目录。安装过程中会出现两次安装提示。第一次是安装JDK，第二次是安装JRE。建议两个都安装在同一个java文件夹中的不同文件夹中。

* JDK，Java SE 开发包。
* Windows或Linux：32位选择x86，64位选择x64。
* Linux：建议选择.tar.gz版本，可以在你希望的位置直接解压缩这个压缩包。

## 环境变量的配置

1.JAVA_HOME

jdk安装目录，以后要使用这个路径的时候，只需输入%JAVA_HOME%即可, 避免每次引用都输入很长的路径串; 

2.PATH

系统执行命令时要搜寻的路径。

把 %JAVA_HOME%\bin添加到PATH路径下, 这样, 我们在任何路径下就可以仅用java来执行命令了。

3.CLASSPATH

java在编译和运行时要找的class所在的路径。

java加载类(class or lib)路径，只有类在CLASSPATH中，java命令才能识别。设置为：.;%JAVA_HOME%\lib\，(要加.表示当前路径) 

设置CLASSPATH的目的是为了程序能找到相应的".class"文件, 举个例子: 编译一个JAVA程序---A.java, 会得到一个A.class的类文件,在当前目录下执行java A, 将会得到相应的结果(前提是已经设置CLASSPATH为".")。

现在, 把A.class移到别的目录下(例如:"e:\"), 执行java A, 将会抛出java.lang.NoClassDefFoundError异常,原因就是找不到.class文件, 现在你把CLASSPATH增加为:".;e:\"再运行java A, 结果一切正常， java命令通过CLASSPATH找到了.class文件! 

## Centos下安装JDK

1.卸载linux自带的OPENJDK

```shell
[root@blog ~]# rpm -qa | grep jdk
[root@blog ~]# yum remove java-1.7.0-openjdk
```

2.上传JDK，使用rpm命令进行安装

```shell
[root@blog ~]# rpm -ivh jdk-8u121-linux-x64.rpm 
```

3.JDK默认安装在/usr/java中,设置环境变量,在/etc/profile文件里面尾部添加：

```shell
#set java environment

export JAVA_HOME=/usr/java/default
export CLASS_PATH=./:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH

```

##  HelloWord.java

```java
public class HelloWorld
{
	public static void main(String [] args)
	{
		System.out.println("HelloWord");
	}
}
```

javac程序一个java编译器，它将.java文件编译成.class文件。java程序启动java虚拟机，虚拟机执行编译器放在class文件中的字节码。

## 安装库源文件和文档

1. 库源文件在JDK中以一个压缩文件src.zip的形式发布，必须将其解压缩后才能够访问源代码。建议将src.zip文件解压缩到一个javasrc目录中。提示：src.zip文件中包含了所有公共类库的源代码。要想获得更多的源代码（例如：编译器、虚拟机、本地方法以及私有辅助类），请访问网站：http://jdk8.java.net。

2. 文档包含在一个压缩文件中，它是一个独立于JDK的压缩文件。可以直接从网站http://www.oracle.com/technetwork/java/javase/downloads/下载这个文件名为jdk-*version*-docs-all.zip的压缩文件，其中version表示版本，如：8u121。解压缩这个文件，将doc目录重命名为一个更有描述性的名字，如javadoc。建议在浏览器中导航到javadoc/api/index.html，将这个页面增加到书签。


# 数据类型，运算符，控制流程

# 异常处理

## 概念

运行期出现的错误，javac xxx.java时出现的错误不再考虑，观察错误的名字和行号最重要。

## 一个图

Throwable

- Error：处理不了的错误

- Exception：可以处理

	- RuntimeException：可以处理，也可以不处理

	- 如IOException  ：必须cath

## 五个关键字

try catch finally throw throws

## 先逮小的，再逮大的

## 异常和重写的关系

重写的方法如果抛出异常了，必须抛出一样的异常或者不抛异常

# 数组

## 概述

数组可以看成是多个相同类型数据组合，对这些数据的统一管理；数组变量属引用类型，数组也可以看成是对象，数组中的每个元素相当于该对象的成员变量；数组中的元素可以是任何数据类型，包括基本类型和引用类型。

## 一维数组

声明方式：

>type var []  或 type [] var

例如：

```java
int a1 []; int [] a2;
double b [];
Person [] p1; String s1[];
```

**注意：Java语言中声明数组时不能指定其长度（数组中元素的个数），例如：int a [5] //非法**

Java中使用关键字new创建数组对象，格式为：

>数组名 = new 数组元素类型 [数组元素个数]

```java
public class Test {
	public static void main(String args[]) {
		int [] s;
		s = new int[5];
		for (int i = 0;i<5;i++) {
			s[i] = 2 * i + 1;
		}
	}
}
```

内存分析：

![](http://olke8cow1.bkt.clouddn.com/java_20170928222807.gif)

元素为引用数据类型的数组

```java
public class Test {
	public static void main(String args[]) {
		MyDate[] days;
		days = new MyDate[3];
		for(int i = 0; i<3; i++) {
			days[i] = new MyDate(2017,9,i+1);
			System.out.println(days[i]);
		}
	}

}
class MyDate {
	int year; int month; int day;
	MyDate(int y,int m,int d){
		year = y;
		month = m;
		day =d;
	}
	public String toString() {
		return ""+year+month+day;		
	}
}
```

**注意：元素为引用数据类型的数组中的每一个元素都需要实例化。**

内存分析：

![](http://olke8cow1.bkt.clouddn.com/Java_20170928230008.gif)

## 数组初始化

- 动态初始化：数据定义与数组元素分配空间和赋值的操作分开进行。

```java
int a[];
a = new int[3];
a[0] = 3;a[1]=9;a[2]=8;
```

-  静态初始化：在定义数组的同时就为数组元素分配空间并赋值。

```java
int a [] = {3,9,8};
```

- 数组元素的默认初始化：数组是引用类型，它的元素相当于类的成员变量，因此数组分配空间后，每个元素也被按照成员变量的规则被隐式初始化。

```java
public class Test {
	public static void main(String args[]) {
		int a[] = new int[5];
		MyDate[] days = new MyDate[3];
		System.out.println(a[3]);
		System.out.println(days[2]);
	}
}
```

```
输出结果：0
		 null
```

## 数组元素的引用

1. 定义并用运算符new为之分配空间后，才可以引用数组中的每个元素，数组元素的引用方式为arrayName[index],index为数组元素下标，可以是整数常量或整型表达式。如：a[3],b[i],c[6*i]。

2. 数组元素下标从0开始,长度为n的数组的合法下标取值范围为0~n-1。

3. 每个数组都有一个属性length指明其长度，如：a.length。

## 错误: 找不到或无法加载主类 TestArgs

```java
package com.franky.array;

public class TestArgs {
	public static void main(String[] args) {
	    if(args.length<3){
	            System.out.println("Usage: java Test \"n1\" \"op\" \"n2\"");
	            System.exit(-1);
	    } 
	    double d1 = Double.parseDouble(args[0]);
	    double d2 = Double.parseDouble(args[2]);
	    double d = 0;
	    if(args[1].equals("+")) d = d1+d2;
	    else if(args[1].equals("-")) d = d1-d2;
	    else if(args[1].equals("x")) d = d1*d2;
	    else if(args[1].equals("/")) d = d1/d2;
	    else{
	        System.out.println("Error operator!"); 
	        System.exit(-1);
	    }   
	    System.out.println(d);
		}
}
```

测试程序时需要输入命令行参数，在程序同级目录下编译（javac）和执行（java）java 程序时，出现这种类型的错误：找不到或无法加载主类ClassName。

问题定位：首先排除是否是环境变量配置不当造成的问题，只要保证，命令行界面能够识别 javac/java 命令，就说明环境变量配置没有问题。
出现这种问题，往往是因为，java 源文件是Eclipse编辑的，文件中带有包名。

解决方案：就是去掉包名，重新编译执行；或者到包的上级目录下执行java  com.franky.array.TestArgs

## 二维数组

二维数组可以看成以数组为元素的数组。如：

    int a[][] = {{1,2},{3,4,5,6},{7,8,9}};

![](http://olke8cow1.bkt.clouddn.com/java_20171014163426.png)

Java中多维数组的声明和初始化应按从高维到低维的顺序进行，即从左到右。

```java
int a[][] = new int[3][];
a[0] = new int[2];
a[1] = new int[4];
a[2] = new int[3];

int t1[][] = new int[][4]; //非法
```

静态初始化

```java
int a[][] = {{1,2},{3,4},{5,6}};
int b[3][2] = {{1,2},{3,4},{5,6}};//非法
```

动态初始化

```java
int a[][] = new int[3][5];
int b[][] = new int[3][];

b[0] = new int[2];
b[1] = new int[3];
b[2] = new int[5];
```

## 数组的拷贝

### Class System

java.lang.System

    public final class System extends Object

#### Method and Description

    public static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length)

Copies an array from the specified source array, beginning at the specified position, to the specified position of the destination array.

##### Parameters:

- src - the source array.
- srcPos - starting position in the source array.
- dest - the destination array.
- destPos - starting position in the destination data.
- length - the number of array elements to be copied.

##### Throws:

- IndexOutOfBoundsException - if copying would cause access of data outside array bounds.
- ArrayStoreException - if an element in the src array could not be stored into the dest array because of a type mismatch.
- NullPointerException - if either src or dest is null.

### TestArrayCopy.java

```java
public class TestArrayCopy {
	public static void main(String args[]) {
		String[] s = { "Mircosoft", "IBM", "Sun", "Oracle", "Apple" };
		String[] sBak = new String[6];
		System.arraycopy(s, 0, sBak, 0, s.length);

		for (int i = 0; i < sBak.length; i++) {
			System.out.print(sBak[i] + " ");
		}

		System.out.println();
		int[][] intArray = { { 1, 2 }, { 1, 2, 3 }, { 3, 4 } };
		int[][] intArrayBak = new int[3][];
		System.arraycopy(intArray, 0, intArrayBak, 0, intArray.length);
		intArrayBak[2][1] = 100;
		//内存布局见下图

		for (int i = 0; i < intArray.length; i++) {
			for (int j = 0; j < intArray[i].length; j++) {
				System.out.print(intArray[i][j] + "  ");
			}
			System.out.println();
		}
	}
}
```

![](http://olke8cow1.bkt.clouddn.com/java_20171014174314.png)

# 对象与类

#### Java两种核心机制

![](http://olke8cow1.bkt.clouddn.com/Java_20170220203844.png)

* Java 虚拟机（Java Virtual Machine）

Java虚拟机可以理解成一个以字节码为机器指令的CPU；对于不同的运行平台，有不同的虚拟机；Java虚拟机机制屏蔽了底层运行平台的差别，实现了“一次编译，随处运行”。

![](http://olke8cow1.bkt.clouddn.com/Java_20170220204606.png)
 
* 垃圾收集机制（Garbage Collection）

Java语言消除了程序员回收无用内存空间的责任；它提供一种系统级线程跟踪存储空间的分配情况。并在JVM的空闲时，检查并释放那些可被释放的存储器空间。垃圾收集在Java程序运行过程中自动进行，程序员无法精确控制和干预。

#### 语法基础

一个源文件中最多只能有一个public类。其它类的个数不限，每个类对应生成一个.class文件。如果源文件中包含一个public类，它必需按该类名命名。

Java应用程序的执行入口是main()方法。它有固定的书写格式：

```java
public static void main(String args[]) {...}
```

Java语言严格区分大小写。

Java方法有一条条语句构成，每个语句以分号结束。

Java语言有三种注释：

```java
//用于单行注释

/*
用于多行注释
*/

/**
 *用于多行注释，且可以被doc工具解析
 *
 */
```
##### 标识符

Java对各种变量、方法和类等要素命名时使用的字符序列称为标识符。

Java标识符命名规则：
1.标识符由字母、下划线"_"、美元"$"或数字组成。
2.标识符应以字母、下划线、美元符开头。
3.Java标识符大小写第三，长度无限制。
4.Java标识符选取应注意”见名知意“且不能与Java语言的关键字重名。

##### 关键字

Java中一些赋以特定的含义，用作专门用途的字符串称为关键字(keyword)。

所有Java关键字都是小写英文。

Java Language Keywords

Here is a list of keywords in the Java programming language. You cannot use any of the following as identifiers in your programs. The keywords *const* and *goto* are reserved, even though they are not currently used. *true*, *false*, and *null* might seem like keywords, but they are actually literals; you cannot use them as identifiers in your programs.
abstract 	continue 	for 	new 	switch
assert*** 	default 	goto* 	package 	synchronized
boolean 	do 	if 	private 	this
break 	double 	implements 	protected 	throw
byte 	else 	import 	public 	throws
case 	enum**** 	instanceof 	return 	transient
catch 	extends 	int 	short 	try
char 	final 	interface 	static 	void
class 	finally 	long 	strictfp** 	volatile
const* 	float 	native 	super 	while
* 	  	not used
** 	  	added in 1.2
*** 	  	added in 1.4
**** 	  	added in 5.0

goto和const虽然从未使用，但也作为Java关键字保留。


##### Java常量

Java的常量值用字符串表示，区分为不同的数据类型

123-整型常量，3.14-实型常量，'a'-字符常量，true/false-逻辑常量，'helloword'字符串常量

“常量”这个名词还会用在另外其它语境中表示值不可变的变量，参见final关键字

##### Java变量
变量是程序中最基本的存储单元，其要素包括变量名，变量类型和作用域

Java程序中每一个变量都属于特定的数据类型，在使用前必须对其声明，声明格式为：type varName=value;

从本质上讲，变量其实是内存中的一小块区域，使用变量名来访问这块区域，因此，每一个变量使用前必须要先申请（声明），然后必须进行赋值（填充内容），才能使用

##### 程序的执行过程

![](http://olke8cow1.bkt.clouddn.com/Java_20170220232922.png)

##### Java变量的分类
1.局部变量：方法或语句块内部定义的变量
2.成员变量：方法外部、类的内部定义的变量

注意：类外面（与类对应的大括号外面）不能有变量的声明

##### Java数据类型

1.基本数据类型变量
2.引用数据类型变量

![](http://olke8cow1.bkt.clouddn.com/Java_20170220234945.png)

基本数据类型：4类8种

逻辑型-boolen 

适用于逻辑运算，一般用于程序流程控制，只允许取值true或false，不可以0或非0的整数替代true和false。

文本型-char

char型数据用来表示通常意义上的“字符”，字符常量为用单引号括起来的单个字符: char eChar='a';

Java字符采用Unicode编码，每个字符占两个字节，因而可用十六进行编码形式表示。（Unicode是全球语言统一编码）

Java语言中还允许使用转义字符'\'来将其后的字符转变为其它的含义: char c2='\n' //代表换行符

整数型-byte,short,int,long 

各整数类型有固定的表数范围和字段长度，其不受具体操作系统的影响，以保证Java程序的可移植性
八进制整数常量以0开头，如：012
十六进行数以0x或0X开头，如:0x12

Java语言的整型常量默认为int型，声明long型常量可以后加'l'或'L'

        占存储空间   表数范围
byte    1字节        -128~127
short   2字节        -2^15~2^15-1
int     4字节        -2^31~2^31-1
long    8字节        -2^63~2^63-1

浮点型-float,double

与整数类型类似，Java浮点类型有固定的表数范围和字段长度，不受平台影响。
Java浮点类型常量有两种表示形式：十进制形式，科学记数法形式: 3.14e2
Java浮点型常量默认为double型，如要声明一个常量为float型，则需在数字后面加f或F，如：float f = 12.3f;

        占用存储空间  表数范围
float     4字节    -3.403E38~3.403E38              （小数点后7位就不精确了）
double    8字节    -1.798E308~1.798E308            （小数点后15位就不精确了）

##### 基本数据类型转换

1.boolean类型不可以转换为其他的数据类型

2.整型，字符型，浮点型的数据在混合运算中相互转换，转换时遵循以下原则：
  容量（表示的数大小）小的类型自动转换为容量大的数据类型；数据类型按容量大小排序为：
  byte,short,char->int->long->float->double
  byte,short,char之间不会相互转换，他们三者在计算时首先会转换为int型
  可以将整型常量直接赋值给byte,short,char等类型变量，而不需要进行强制类型转换，只要不超出其表数范围。

3.容量大的数据类型转换为容量小的数据类型时，要加上强制转换符，但可能造成精度降低或溢出，使用时要格外注意。

4.有多种类型的数据混合运算时，系统首先自动的将所有数据转换成容量最大的那一种数据类型，然后再进行计算。

5.实数常量（如：1.2）默认为double

6.整数常量（如：123）默认主为int
  
```java
package com.franky.base;

public class ConvertTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		int i1 = 123;
		int i2 = 456;
		double d1 = (i1+i2) * 1.2; //系统将转换为double型进行运算
		float f1 = (float) ((i1+i2) * 1.2); //需要加强制转换符
		byte b1 = 1; //这种可以，但不要超出表述范围
		byte b2 = 2;
		byte b3 = (byte)(b1+b2); //系统将转换为int型进行运算，需要强制转换符转换为byte
		
        double d2 = 1e200;
        float f2 = (float)d2; //超出范围，会产生溢出
        System.out.println(f2);//Infinity
        
        // 超出范围，int转换为byte会直接砍掉，但float不行，输出Infinity
        
        float f3 = 1.23f;//必须加f,1.23默认是double型,或者加(float)转换
        long l1 = 123;
        long l2 = 300000000000000000L;//必须加L,超出int范围
        float f = l1 + l2 + f3;//系统将转换为float型计算
        long l = (long)f; //强制转换会舍去小数部分（不是四舍五入,直接砍掉小数部分）
	}

}


```

##### 程序格式

1.大括号对齐
2.遇到{缩进，Tab/Shift + Tab
3.程序块之间加空行
4.并排语句之间加空格
5.运算符两侧加空格
6.{前面有空格
7.成对编程

##### 运算符

Java语言支持以下运算符：

1. 算术运算符：+,-,*,/,%,++,--
2. 关系运算符：>,<,>=,<=,==,!=
3. 逻辑运算符：!,&,|,^,&&,||
4. 位运算符：&,|,^,~,>>,<<,>>>
5. 赋值运算符：=
6. 扩展赋值运算符：+=，-=，*=，/=
7. 字符串连接运算符: +

++(--)
在前时先运算再取值
在后时先取值再运算


&-->逻辑与，&&-->短路与
||-->逻辑或，||-->短路或
逻辑与，逻辑或两边的表达式都会计算

短路与，短路或可根据第一个表达式得到结果，第二个表达式可以不计算
如： (1>3)&&(2>5) 根据 1>3即可判断结果为false，后面的不再计算

“+”除了用于算术加法运算外，还可用于对字符串进行连接操作
“+”运算符两侧的操作数中只要有一个是字符串类型，系统就会自动将另一个操作数转换为字符串然后再进行连接
当进行打印时，无论任何类型，都自动转换为字符串进行打印

```java
int c = 12;
System.out.println("c=" + c);

System.out.println(c);
```

##### 三目条件运算符

X ? Y : Z

其中X为boolean类型表达式，先计算X的值，若为true，则整个三目运算的结果为表达式Y的值，否则整个运算结果为表达式Z的值。

##### 分支/条件语句

根据不同条件，执行不同语句。
if
if .. else
if .. else if
if .. else if .. else if .. else
switch

##### 循环

重复执行某些动作
for
while
do .. while

break语句用于终止某个语句块的执行。用在循环语句体中，可以强行循环;

continue语句用于循环语句体中，用于终止某次循环过程，跳过循环体中continue语句下面未执行的循环，开始下一次循环过程;

##### swith语句（条件语句补充）
swith(){
	case xx :
             ……
	case xx :
             ……
	case xx :
             ……
	default :
	         ……
}
小心case穿透，推荐使用break语句

多个case可以合并到一起
case xx:
case yy:
        do something

default可以省略，但不推荐省略
swith
java中swith语句只能探测int类型值（byte,short,char可以转换为int，也可以）

##### 方法
Java的方法类似于其它语言的函数，是一段用来完成特定功能的代码片段，声明格式:
[修饰符1 修饰符2 ……] 返回值类型  方法名 (形式参数列表){
	Java 语句;
	……;
	……;
}

形式参数: 在方法被调用时用于接收外界输入的数据
实参: 调用方法时实际传给方法的数据
返回值: 方法在执行完毕后返还给调用它的环境的数据
返回值类型: 事先约定的返回值的数据类型，如无返回值，必须给出返回值类型void


Java语言中使用下述形式调用方法: 对象名.方法名(实参列表)

实参的数目、数据类型和次序必须和所调用方法声明的形参列表匹配

return语句终止方法的运行并指定要返回的数据

Java中进行函数调用中传递参数时，遵循值传递原则：
基本类型传递的是该数据值本身。引用类型传递的是对对象的引用，而不是对象本身。

##### 变量的作用域

##### 递归调用
递归调用指在方法执行过程中出现该方法本身的调用,如：

```java
public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		System.out.println(method(5));

	}
	
	public static int method(int n) {
		if (n == 1)
			return 1;
		else
			return n * method(n-1);
	}

}
```
#### OO（面向对象）

类是用于描述同一类型的对象的一个抽象的概念，类中定义了这一类对象所具有的静态和动态属性。

类可以看成一类对象的模板，对象可以看成该类的一个具体实例。



##### 成员变量
成员变量只可以是Java语言中任何一种数据类型（包括基本类型和引用类型）；在定义成员变量时可以对其初始化，如果不对其初始化，Java使用默认的值对其初始化。**而局部变量则必须进行初始化，否则编译报错**; 成员变量的作用范围为整个类体。


##### 访问控制
Java权限修饰符public protected private 置于类的成员定义前，用来限定其他对象对该类成员的访问权限。

修饰符 | 类内部 | 同一个包 | 子类 | 任何地方
---|---|---|---|---
private | Yes | | |
default | Yes | Yes | |
protected | Yes | Yes | Yes |
public | Yes | Yes | Yes | Yes 

对于class的权限修饰只可以用public和default。

1. public类可以在任意地方被访问

2. default类只可以被同一个包内部的类访问

##### 方法的重写

在子类中可以根据需要对基类中继承来的方法进行重写。

重写方法必须和被重写方法具有相同方法名称、参数列表和返回类型。

重写方法不能使用比被重写方法更严格的访问权限。

##### super关键字

在Java类中使用super来引用基类的成分。

##### 继承中的构造方法

子类的构造的过程中必须调用基类的构造方法。

子类可以在自己的构造方法中使用super(argument_list)调用基类的构造方法；使用this(argument\_list)调用本类的另外的构造方法；如果调用super，必须写在子类构造方法的第一行。

如果子类的构造方法中没有显示地调用基类构造方法，系统默认调用基类无参数的构造方法。

如果子类构造方法中既没有显式调用基类构造方法，而基类中又没有无参的构造方法，则编译出错。

##### 对象转型（casting）

一个基类的引用类型变量可以“指向”其子类的对象。

一个基类的引用不可以访问其子类对象新增加的成员（属性和方法）。

可以使用  引用变量instanceof类名  来判断该引用型变量所“指向”的对象是否属于该类或该类的子类。

子类的对象可以当作基类的对象来使用称作向上转型（upcasting），反之称为向下转型（downcasting）

##### Final关键字

1. final的变量的值不能够被改变（final的成员变量，final的局部变量[形参]）

2. final的方法不能够被重写

3. final的类不能够被继承

#### Exception

#### Array

#### 基础类

#### I/O Stream

#### Collection/Generic

#### Thread

#### TCP/UDP

#### GUI

#### Meta Data

#### Regular Expression
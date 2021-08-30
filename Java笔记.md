# Java笔记（暂无图床）

## 2.11 代码-class-执行

一.明确Java运行原理

![image-20210823000252029](D:\Coding\JavaNotes\Java笔记.assets\image-20210823000252029.png)

二.基本操作

1. 完成代码 
2. 打开文件所在位置（右键代码区）-在目录栏输入进入cmd窗口
3. 输入 javac 文件名.java  生成class文件
4. 输入 java 类名 运行主类

三.注意事项

1.注意主类名与文件名一致

2.运行的是主类 ——类名，**不要加后缀名**

3.注意编码格式中文需要gbk支持，右键cmd观察![image-20210823005611090](D:/Coding/JavaNotes/Java%E7%AC%94%E8%AE%B0.assets/image-20210823005611090.png)

4.注意程序运行的实质：1）编译器将.java文件编译成.class文件 2）java.exe运行装载到虚拟机JVM的**.class文件**

​	因此：**修改.java文件后需要重新编译**

## 2.13 Java 开发注意事项及细节说明

  1. Java程序的执行入口是main()方法，有固定格式

     ​	pubic static main(String[] args){ }

  2. Java严格区分大小写

  3. Java每条语句分号结尾

  4. 源文件最多只能有一个public类，且文件名必须与public类同名

  5. 非public的main方法：其他类个数不限，也可将main方法写在非public类里，然后运行非public类

  

```java
//1.public的类hello
  public class hello{
   //编写一个main方法
   public static void main(String[] args){
    System.out.println("hello walodo来个中文");
   }
  }
  //2.非主类cat
  class cat{
   //编写一个main方法
   public static void main(String[] args){
    System.out.println("mipa~");
   }
  }
  //3.非主类dog
  class dog{
   //编写一个main方法
   public static void main(String[] args){
    System.out.println("wowo");
   }
  }
```



  ### 常见bug

  错误: 类 hello 是**公共的**, 应在名为 hello.java 的文件中声明

  ​	文件名与主类名不统一

  错误: 仅当显式请求注释处理时才接受类名称 'hello'

  ​	执行编译时，文件后缀名不全

  错误: 进行语法分析时已到达文件结尾

  ​	没打分号或者是括号不全

## 2.14 格式化输出

注意转义字符

```java
class println{
	public static void main(String[] args){
		System.out.println("java Test\n书名\t作者\t价格\t销量\n三国\t罗贯中\t120\t1000");
	}
}
```



## 此处暂时省略文档注释的生成0024

一次多行注释用ctrl+/

## 3.5 加号的使用

当左右两边都是数值型的时候，做加法运算

当左右两边有一个是字符型，做拼接运算



## 数据类型

大类上分为：基本数据类型和引用数据类型

![image-20210825230600296](D:/Coding/JavaNotes/Java%E7%AC%94%E8%AE%B0.assets/image-20210825230600296.png)

整型四种变量的关系 4 2 8 1

float和long型常量在后加l

| 基本类型 | 大小    | 最小值    | 最大值         | 包装类型  |
| -------- | ------- | --------- | -------------- | --------- |
| boolean  | —       | —         | —              | Boolean   |
| char     | 16 bits | Unicode 0 | Unicode 216 -1 | Character |
| byte     | 8 bits  | -128      | +127           | Byte      |
| short    | 16 bits | - 215     | + 215 -1       | Short     |
| int      | 32 bits | - 231     | + 231 -1       | Integer   |
| long     | 64 bits | - 263     | + 263 -1       | Long      |
| float    | 32 bits | IEEE754   | IEEE754        | Float     |
| double   | 64 bits | IEEE754   | IEEE754        | Double    |
| void     | —       | —         | —              | Void      |



## focuses

### **1.自动换行验证**

### **2.为什么范围会减一1**，涉及到进制，原补码

### **3.自动装箱拆箱**

#### 数据存储

那么，程序在运行时是如何存储的呢？尤其是内存是怎么分配的。有5个不同的地方可以存储数据：

1. **寄存器**（Registers）最快的存储区域，位于 CPU 内部 [^2](https://github.com/Polumm/Java_learning/blob/main/OnJava8-master/docs/book/大多数微处理器芯片都有额外的高速缓冲存储器，但这是按照传统存储器而不是寄存器。)。然而，寄存器的数量十分有限，所以寄存器根据需求进行分配。我们对其没有直接的控制权，也无法在自己的程序里找到寄存器存在的踪迹（另一方面，C/C++ 允许开发者向编译器建议寄存器的分配）。
2. **栈内存**（Stack）存在于常规内存 RAM（随机访问存储器，Random Access Memory）区域中，可通过栈指针获得处理器的直接支持。栈指针下移分配内存，上移释放内存，这是一种快速有效的内存分配方法，速度仅次于寄存器。创建程序时，Java 系统必须准确地知道栈内保存的所有项的生命周期。这种约束限制了程序的灵活性。因此，虽然在栈内存上存在一些 Java 数据，特别是对象引用，但 Java 对象却是保存在堆内存的。
3. **堆内存**（Heap）这是一种通用的内存池（也在 RAM 区域），所有 Java 对象都存在于其中。与栈内存不同，编译器不需要知道对象必须在堆内存上停留多长时间。因此，用堆内存保存数据更具灵活性。创建一个对象时，只需用 `new` 命令实例化对象即可，当执行代码时，会自动在堆中进行内存分配。这种灵活性是有代价的：分配和清理堆内存要比栈内存需要更多的时间（如果可以用 Java 在栈内存上创建对象，就像在 C++ 中那样的话）。随着时间的推移，Java 的堆内存分配机制现在已经非常快，因此这不是一个值得关心的问题了。
4. **常量存储**（Constant storage）常量值通常直接放在程序代码中，因为它们永远不会改变。如需严格保护，可考虑将它们置于只读存储器 ROM （只读存储器，Read Only Memory）中 [^3](https://github.com/Polumm/Java_learning/blob/main/OnJava8-master/docs/book/一个例子是字符串常量池。所有文字字符串和字符串值常量表达式都会自动放入特殊的静态存储中。)。
5. **非 RAM 存储**（Non-RAM storage）数据完全存在于程序之外，在程序未运行以及脱离程序控制后依然存在。两个主要的例子：（1）序列化对象：对象被转换为字节流，通常被发送到另一台机器；（2）持久化对象：对象被放置在磁盘上，即使程序终止，数据依然存在。这些存储的方式都是将对象转存于另一个介质中，并在需要时恢复成常规的、基于 RAM 的对象。Java 为轻量级持久化提供了支持。而诸如 JDBC 和 Hibernate 这些类库为使用数据库存储和检索对象信息提供了更复杂的支持。

基本类型有自己对应的包装类型，如果你希望在堆内存里表示基本类型的数据，就需要用到它们的包装类。代码示例：

```Java
char c = 'x';
Character ch = new Character(c);
```



### **4.new why-when**

### **5.查阅API**

API (Application Programming Interface) 应用程序编程接口

Java 类的组织形式

![](D:/Coding/JavaNotes/Java%E7%AC%94%E8%AE%B0.assets/image-20210826000017445.png)

1.按组织结构查：JDK-包-类……

2.直接索引

[中文在线文档](www.matools.com)

### 6.int和float的细节

***float陷阱**：对*运算过后*的小数进行比较很危险！

**安全的写法**：应该是将:两个数的差值的绝对值，在某个精度范围内判断

```java
if(Math.abs(num1 - mum2) < 0.0001) 
```



### **7.字符型**与自动转换

C++中char占1个字节而**Java中char占两个字节！**

为什么？因为**Java中char对应的是Unicode码！**

​	汉字有对应的Unicode码，一个汉字可以用一个char表示

```java
//1.public的类hello
public class hello{
	//编写一个main方法
	public static void main(String[] args){
		System.out.println("hello walodo来个中文");
	}
}
//2.非主类cat
class cat{
	//编写一个main方法
	public static void main(String[] args){
		System.out.println("mipa~");
	}
}
//3.非主类char
class charTest{
	//编写一个main方法
	public static void main(String[] args){
		char a = 'a';//字符'a'
		System.out.println(a);
		char b = 97;//unicode码为97的字符
		System.out.println(b);
		char c = '宋';//字符'宋'
		System.out.println(c);
		char d = '9';//字符'9'
		System.out.println(d);
		char e = '\141';
		System.out.println(e);
		//以下非法：不知道为什么
		// char f = '\0x0061';
		// System.out.println(f);
		
		//建立字符与编码间的联系
		System.out.println((int)c);//输出字符'宋'的Unicode码：23435
		char f = 23435;//直接存'宋'的Unicode码
		System.out.println(f);//用Unicode码输出字符'宋'
		
		//char相当于一个整数，可以直接参与运算
		char g = 'a';
		System.out.println(g + 10);
	}
}

//4.格式化输出练习
//一次多行注释用ctrl+/
class println{
	public static void main(String[] args){
		System.out.println("java Test\n书名\t作者\t价格\t销量\n三国\t罗贯中\t120\t1000");
	}
}

//6.数据类型转化练习
class AutoConvertDetail{
	public static void main(String[] args){
		//java中默认浮点为double
		float a = 1.1f;
		//float b = 1.1;//这是错的，Java中浮点默认double，要想声明为float必需加
		
		//混合运算中，先全部转化成最大容量类型再计算
		int pre = 1;
		//char c = 1 + pre;//int大于char
		//float d = 1.1 + pre;//错，默认double
		double e = 1.1 + pre;//对

		//用一个具体数值声明byte时，先判断是否在范围内，在则可以
		//但是不能把变量付给byte
		byte f = 127;//-128-127
		byte g = pre;//错

		//byte,short,char不能自动互转
		//byte,short,char可以运算，但结果会转为int
		byte h = f + f;//错

	}
}
```



### **8.编码集**

### **9.自动转化与强制转化**

### **10.String类**

### **11.代码练习**

### **12.更改快捷键**

在首选项-按键绑定-默认中查找(ctrl+f)到原有快捷键，复制到首选项-按键绑定-用户中(记得更改好新的快捷键!)








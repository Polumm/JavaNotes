# Java笔记（暂无图床）

## 2.11 代码-class-执行

一.明确Java运行原理

![image-20210823000252029](D:\1VSCworkspace\TyporaImage\image-20210823000252029.png)

二.基本操作

1. 完成代码 
2. 打开文件所在位置（右键代码区）-在目录栏输入进入cmd窗口
3. 输入 javac 文件名.java  生成class文件
4. 输入 java 类名 运行主类

三.注意事项

1.注意主类名与文件名一致

2.运行的是主类 ——类名，**不要加后缀名**

3. 注意编码格式中文需要gbk支持，右键cmd观察

    ![image-20210823005611090](D:/1VSCworkspace/TyporaImage/image-20210823005611090.png)

4. 注意程序运行的实质：1）编译器将.java文件编译成.class文件 2）java.exe运行装载到虚拟机JVM的**.class文件**

    	因此：修改java文件后需要重新编译
## 2.13 Java 开发注意事项及细节说明

  1. Java程序的执行入口是main()方法，有固定格式

     ​	pubic static main(String[] args){ }

  2. Java严格区分大小写

  3. Java每条语句分号结尾

  4. 源文件最多只能有一个public类，且文件名必须与public类同名

  5. 非public的main方法：其他类个数不限，也可将main方法写在非public类里，然后运行非public类

  `//1.public的类hello
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
  }`

  ### 常见bug

  错误: 类 hello 是公共的, 应在名为 hello.java 的文件中声明

  ​	文件名与主类名不统一

  错误: 仅当显式请求注释处理时才接受类名称 'hello'

  ​	执行编译时，文件后缀名不全

  错误: 进行语法分析时已到达文件结尾

  ​	没打分号或者是括号不全

## 2.14 格式化输出

注意转义字符

`class println{
	public static void main(String[] args){
		System.out.println("java Test\n书名\t作者\t价格\t销量\n三国\t罗贯中\t120\t1000");
	}
}`




# java silver + java gold资料整理
[[Java金牌]]

# 拓展 JavaBatch
[[java batch]]
# 练习
[[how2j  SSM项目练习]]

## java silver 内容+java基础补充

## chp1

### 关于java编译的特征及不依赖OS的原因的解释:

C语言:编译型语言(一次性将source code转换为可执行的.exe文件); 使用的工具是编译器

Python之类的:解释性语言 将需要的部分转换为二进制语言 使用的工具是解释器

Java使用的是半编译半解释: source code1---字节码(中间文件)---jvm(virtual machine)虚拟机---jvm适应了各个os所以java可以任意系统运行.

### 环境变量与`-classpath`命令

Classpath就是环境变量的说法; -classpath就是javac里面设置的方式

-classpath:这个是javac的参数

 

设置用户类路径，它将覆盖CLASSPATH 环境变量中的用户类路径。若既未指定CLASSPATH 又未指定-classpath，则用户类路径由当前目录构成。

 

classpath是JVM用到的一个环境变量，它用来指示JVM如何搜索class。

 

因为Java是编译型语言，源码文件是.java，==而编译后的.class文件才是真正可以被JVM执行的字节码==。因此，JVM需要知道，如果要加载一个abc.xyz.Hello的类，应该去哪搜索对应的Hello.class文件。

 

所以，classpath就是一组目录的集合，它设置的搜索路径与操作系统相关。

Jvm在找.class后缀的文件时依次在这组目录的集合下面寻找,找不到就报错

设置CLASSPATH的方式

1. 直接在系统环境变量中设置, 但是会污染整个系统, 不推荐
2. 在启动jvm时设置classpath变量, 推荐

 

写法: 

`java -classpath .;C:\work\project1\bin;C:\shared abc.xyz.Hello`

这个点`.`表示了当前目录

或者是使用-classpath 的简单写法 -cp

`java -cp .;C:\work\project1\bin;C:\shared abc.xyz.Hello`

本质上就是指定了jvm找寻`.class`文件的路径

没有设置系统环境变量，也没有传入-cp参数，那么JVM默认的classpath为.，即当前目录：

### package相关考点

1.给class和interface提供空间

​	2.避免了class的重复命名

「パッケージ名.クラス名」は完全修飾クラス名と呼ばれる。因为开发中会用到别人写好的文件, 这样子可以避免重复名字

​	3.==如果没有指定package, 则属于无名package(不存在不属于package的class)==

​	4.命名一般使用地址名逆向, 例如jp.co.xxx; 但也不绝对

​	5.提供了制御access

因为有的修饰子 --- 其他不能用；有的其他能用 --- 所以将class file分包的话可以实现在package单位管理access程度

6.==属于无名package的文件只能access无名package内的file;==

#### java中主要提供的package

1. java.lang提供java的基本动作
2. java.io file的data读取入力出力
3. java.util复数object集合的package
4. java.text文字列 日期 数值等相关的package
5. java.lang是基本package不需要import也可以
6. 其余的import时候需要多行

### java中的access权限

|              | 同一个class | 同一个包中其他类 | 不同包子类 | 不同包无关class |
| ------------ | ----------- | ---------------- | ---------- | --------------- |
| Public       | o           | o                | o          | o               |
| Protected    | o           | o                | o          | x               |
| Default 不写 | o           | o                | x          | X               |
| Private      | o           | x                | x          | x               |

### enter point （java执行时的入口）

格式: `public static void main(String[] args){ }`; `args`是一个引数名可以变化

​	相当于是在开始的时候定义了一个字符串数组,为什么这么写的原因是,以前为了实现键盘录入, 在最开始的时候将信息存储在这里

​	要点: 1.公开(public); 2.不生成instance也可以(static静态保证了不实例化也可以使用); 3.没有return值(void); 

​	4.method名用main; 5.引数用String配列型(string[])接收; 也可以用长引数型接收

​	写作: `public static void main(String... args){ }`

5. `Public static void main(String args){ } `这样子写文法上没错不是compile error, 但执行时会有执行时error.



### 关于java命令行 compile和执行 的问题

用记事本等文件写的java source code需要用扩张子`.java`命名---cmd运行时---使用`javac file_name.java`进行compile---compile后file_name变成public宣言的class名字---`class_name.javac`---使用java运行这个文件:`java class_name `不加扩张子

当文件里有`main.java`和`mian.javac`时如果用`java main`执行没问题

但如果用`java main.java`执行就不可以; 会报错,说已经在该文件夹里存在javac编译后的class文件



#### java command 实行javac文件的语法

`java 完全修饰class文件名[引数1 引数2 引数3]`

*  这个命令是为了启动jvm---让jvm在指定的完全修饰class里面去找main方法---然后执行
* 当class是属于无名包时 --- 直接写class名就可以

a) Java command可以执行三种

i. 含有main method的class file

ii. Jar file内的main class

iii. Module含有的main class (java se 9开始搭载的机能)

* 引数之间使用空格隔开

*  [引数 引数 …]被称为启动parameter和commandline引数---可以省略---写了的话会当做main 方法的引数String[]收纳

*  Javac compile后的文件用java执行,执行的时候不带`.class`后缀; 在java11版本也可以不用javac编译直接用java.exe执行格式为 java xx.java

  * 这种被称为source file mode

  ##### source file mode执行模式

  Java se 11中可以不用javac command去compile就可以直接执行的source file mode被加入了

  例如: `java Sample.java a b c`这样的方法

  这样的source file mode其实也是执行了compile的, 只是没有将javac文件生成出来

  当扩张子是.java的时候执行source file mode没问题, 但是是别的格式时使用这个source file mode的话要用到source option

  

  ###### **Source option的解释及其使用会出现的问题**

  * java command 中的`-source`

  `-source `指的是我们的 Java 代码的语言版本和编译的 JDK 相匹配（例如，1.8代表JDK8）。我们所提供的版本值将限制源代码中使用的语言特性，使其符合各自的Java版本。

  `javac HelloWorld.java -source 1.6 -target 1.8`

  上面的命令的意思就是 程序的运行环境需要支持JDK 1.8 也就是 Java 8， 而源码中不能包含 Java 6 以上版本的语言特性，比如说 Lambda 表达式等等。

  简单说就是-source可以指定编译时的jdk版本,例如1.6,就是1.6及其以下, 这样的好处是可以使得编译时, 不会查询1.8等高级版本的功能节省时间

  

  ###### **`-source  option`与扩张子可以不为`.java`的情况**

  在上面介绍了source file mode来使得 jvm 运行, 但是其扩张子(后缀)一定要为`.java`

  不是`.java`时就需要使用到`-source option`来解决

  例如:

  ```java
  public class Sample{
  public static void main(String… args){
  for(String arg : args){
  System.out.println(arg);
  }}} 
  ```

  这个代码的public class宣言为Sample

  如果在cmd执行下面的代码

  `mv Sample.java Sample`  这一步将`.java`域名省略了(这个改名操作是在unix类os中的, windows的话则是`ren`)

  `java –source 11 Sample a b c ` 这样子也可以执行,说明`.java`在这个方式之下就变得不是必要的了

  `mv Sample Test.java`

  

  ###### **关于java为什么可以`source file mode`执行，以及`-source`执行非`.java`文件的原因**

  * **原因如下**==

  在单文件运行的情况下 Java 11 做了哪些改变

  1. Java 11 可以将单文件作为脚本来运行

  2. 文件名不在需要跟第一个公共类名相同

  3. 同一个文件下可以存在多个公共类

  4. 单文件下不再需要 class 文件

  这是因为==java在让自己像脚本语言靠拢==

  > 关于脚本语言层级
  >
  > <img src="C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20240413114144975.png" alt="image-20240413114144975" style="zoom:50%;" />

  脚本语言的特性是可以在文件第一行以` #! `开头，并指定运行命令，然后可以直接在终端中运行，比如 Python

  java因为本身的特性，`.java `后缀的文件不运行出现` #!`，所以要先修改名字
  
  * **以上为为什么会出现需要运行后缀名不是`.java`文件的原因**
  
  ```java
  $ mv Hello.java hello.sh
  $ chmod +x hello.sh
  ```
  
  这里的java文件后缀名已经换了 与之对应需要修改文件加入`#!`
  
  ```java
  #!/usr/bin/env java --source 11
  
  public class HelloWorld{
      public static void main(String args[]){
                  System.out.println("Hello World");
      }
  }
  ```
  
  直接将`-source`操作写在了文件里, 这样子就不用编译—直接执行—所以像脚本文件

  ```java
  $ java -Dtrace=true --source 11 hello.sh
  ```

  也可以这样子用java来执行这个文件
  
  或者直接用系统去执行
  
  ```java
  $ ./hello.sh
  Hello World
  ```
  
  不仅后缀扩张子不用为`.java`, 且连文件名都不需要和public宣言的类相同
  
  

#### 关于用command line启动java时给args录入文字

以a b c 为例子; 只要空格隔开就可以; 如果使用””的话例如 `a “b,c”`输出的就是

`	a b,c`

如果再加上 ¥” ¥”的话例如` a ¥”bc¥”`则会输出`a “bc”`

​	`java Sample.java hello world ¥`

* dollar符号的键入方式是
  * `alt+0165` or `shift+4`

​	双引号本身不作为文字; `¥”`只输入这个的话会打印`”`出来

### jvm jre jdk 等各自表示什么

#### jvm jre jdk基础

* jdk: java开发环境
  * 包括编译工具（javac.exe）打包工具（jar.exe）等

* jre: java执行环境
  * 包括java虚拟机和java程序所需的核心类库（主要是java.lang包）

* jvm: java虚拟机
* 大小顺序：
  * jdk>jre>jvm

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0pvdXJXb24vaW1hZ2UvbWFzdGVyL0phdmElRTclQUUlODAlRTQlQkIlOEIvSlZNJkpSRSZKREslRTUlODUlQjMlRTclQjMlQkIlRTUlOUIlQkUucG5n?x-oss-process=image/format,png)



#### javap

javap是JDK自带的反汇编器，可以查看java编译器为我们生成的字节码。通过它，我们可以对照源代码和字节码，从而了解很多编译器内部的工作。

`javap [ 命令选项 ] class. . .`

#### jmod

为了查询module构造的command

## 什么是字节码，使用字节码的好处

字节码：java源代码经过虚拟机编译器编译后产生的文件 --- 扩展为.class的文件

好处：

​	1. 字节码方式，一定程度解决传统解释型语言执行效率低的问题，同时保留了解释型语言的可移植的特点

**==注意==** java是给jvm虚拟机编译一个虚拟机能够理解的代码 --- java --> 编译器 -->jvm

## java数据类型相关

### 为什么是-128~127作为byte的取值范围

​	byte占用一个字节，一个字节是8个bit，2进制中的一位叫做1bit，每位用0或1表示能够有256个数据（2^8）



​	开头的为符号位，剩余的为数值位，符号位0为正



​	0111 1111 就是127，0000 0001就是1；0000 0000就是+0；与之相对的1000 0000就是-0

为了解决-0这个问题 --- 所以规定给-0 为 -128

 	但是`1111 1111`这样子的类容，计算机会识别为`-1`

* 识别为-1的原因 --- ==**原码 反码 补码**==

关于==原码 反码 补码==

1. 计算机存储有符号的整数都是存储他们的补码 --- java语言都是有符号位的
2. 正数和0的补码 反码是本身原码；
3. 复数的反码是符号位不变，其他位取反；补码是在反码的基础上加1（符号位不变）
4. 计算机用补码进行加法运算

eg：1000 0111 反码为 1111 1000 补码为1111 1001

原来的数字为-7 反码计算为 -120 相加刚好就是 111 1111 的范围

那么计算机处理 1111 1111的时候先减一（补码--》反码） 1111 1110

反码 --> 原码 1000 0001 就是-1

那么1000 0001就是-127



**为什么1000 0000 可以表示-128**

 这里我分析的是byte，它就8位。在无符号位的二进制中128的表示为1000 0000。有符号位的情况下byte好像无法表示+128或-128。

  如果我们假设现在byte不是占用8位，而是9位，最高位是符号位。那么-128就能够是1 1000 0000，其补码也是1 1000 0000，很神奇吧，一样的。-128的补码尾八位就是1000 0000。那就规定【1000 0000是-128的补码，且-128是没有原码和反码的，即不能利用1000 0000反推其原码和反码】。

 

10.如果你对9步的推导表示不太接受，那么简单就认为计算机规定了1000 0000就是-128，是一种人为设计没有什么道理可以言（据说是印度阿三设计的）。其实这么设计也是很巧妙的，在于：

  【其一】对于如果大于8位的有符号整数数据类型，-128的补码尾八位刚好是1000 0000。

  【其二】比如127（0111 1111）加1（0000 0001）刚好得到-128（1000 0000），-128（1000 0000）加1（0000 00001）等于-127（1000 0001）这样从-128~127的反码首尾相连,形成了一个闭环，就像时钟一样。  

  【其三】在计算机中减法运算可以转换成加法运算，比如8-1——>8+(-1)——>补码运算：(0000 1000) + (1111 1111) = (0000 0111) 刚好是7。-128+127——>(1000 0000) + (0111 1111) = （1111 1111）刚好是-1，-128的补码完美的适用于减法。

 

结论：

  【1】计算机中负数是用补码的形式保存、并用它参与加减法运算的，减法会被转换为加法，计算机中没有减法运算。

  【2】反码是为了解决减法运算，补码是为了解决反码产生的±0的问题。参考(https://blog.csdn.net/boatalways/article/details/17027573)

  【3】对人而言二进制所代表的值一定是从原码求出的，开头如果是1的二进制，一定要说明其是原码、反码还是补码。

  【4】在原码、反码、补码相互转换以及求对应的十进制求值时，符号位是绝不参与的，但是在加减过程中，是参与位运算的。

  【5】计算机中规定了+0对应的二进制就是0，那么-0就没有意义了，必须找一个数和它对应。

  【6】byte的最小值-128、short的最小值-32768、int的最小值-2147483648都是用对应的-0的原码来进行表示，这是人为规定的、人为规定的、人为规定的。但是这么规定又很巧妙，妙在上述10中的三点。

### String相关内容

String的生成方式

``````java
a)String q1 = new String("abc");
b)String q1 = "abc";
c)String q1 = String.valueOf("abc");

String[] arr = {new String("ad"),"22"}
``````



# java gold



# java 学习
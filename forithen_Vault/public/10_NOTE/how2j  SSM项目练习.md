# how2j  SSM项目练习前置学习

## Java内容复习

### 命令行运行java程序

* 文件名和class名不一致的时候 --- 不能javac编译

  * **原因：**在使用命令行的`javac`编译Java文件时，Java源文件的文件名应该与公共类的名称一致。这是因为Java编译器（`javac`）==默认会期望文件名与公共类名匹配==。如果文件名与公共类名不一致，编译器将无法正确识别和编译文件。

  * 解决方法：

    1. 将两者名称保持一致

    2. 使用`-d`选项指定编译输出目录，并使用`-classpath`选项指定类路径。这将允许您将编译输出放入指定目录，并将类路径指向该目录，以便编译器可以找到生成的类文件。

       ``````
       javac -d . MySource.java
       java -classpath . MyClass
       ``````

       在上述命令中javac编译后 --- 编译码名和公共类名保持了一致。

       `-d .` 将编译输出放在当前目录中，然后`-classpath .` 将类路径指向当前目录，使得编译器和运行时可以找到类文件。

### java基本知识点

#### java变量相关

##### 变量的八种基本类型

* 整型 4种
  * 从小到大 byte -- short -- int -- long
* 字符型
  * char
* 浮点型 2种
  * 小->大  float -- double
* 布尔型
  * boolean

###### 关于强制转换&&默认数字格式

``````java
	float f1 = 54.312; //会报错
	float f2 = 54312;
	float f3 = 54.312f;
``````

在Java中，浮点数字默认被解释为`double`类型，因此，如果直接将浮点赋值给`float`类型的变量时，会产生编译错误。

整数值默认被解释为`int`类型，而`int`可以直接赋值给`float`，因为`float`可以承载`int`的范围。

###### char类型的默认值

char类型的值默认是Unicode字符'\u0000'，它对应于ASCII值0，表示空字符或空格。这是char类型的初始值，如果你声明一个char类型的变量但没有显式地初始化它，然后就会被设置为默认值'\u0000'。

``````java
        //因为i2的值是在byte范围之外，所以就会按照byte的长度进行截取
        //i2的值是300，其对应的二进制数是 100101100
        //按照byte的长度8位进行截取后，其值为 00101100 即44
        b =(byte) i2;
        System.out.println(b);

        //查看一个整数对应的二进制的方法：
        System.out.println(Integer.toBinaryString(i2));
``````

* ``````java
  //如下
  short a = 1;
  short b = 2;
  //a+b 是什么数据类型
  ``````

``````java
public class NumType {

	public static void  getType(short x1,short x2) {
		Object o = x1+x2;
		System.out.println((o).getClass().toString());
	}
	public static void main(String[] args) {
		short a = 1;
		short b = 2;
		getType(a,b);
	}
}
``````

结果显示`class java.lang.Integer`为整数

###### **Java中进行二元与运算类型的提升规则 整数运算：**

如果两个操作数有一个为long，则结果也为long；      

没有long时，结果为int。即使操作数全为short、byte，结果也是int。 

浮点运算：        如果两个操作数有一个为double，则结果为double；        

只有两个操作数都是float，则结果才为float。 

**注意**：int 与 float 运算，结果为 float。

##### 字面量

给基本类型的变量赋值的方式叫做 **字面值**

##### 转义字符

``````java
//以下是转义字符
        char tab = '\t'; //制表符
        char carriageReturn = '\r'; //回车
        char newLine = '\n'; //换行
        char doubleQuote = '\"'; //双引号
        char singleQuote = '\''; //单引号
        char backslash = '\\'; //反斜杠
``````

##### final

``````java
    public void method1(final int j) {
        j = 5; //这个能否执行？
    }
``````

* 不能执行会报错 
  * final所声明的对象只能进行一次赋值，调用方法时总会提供参数值，就已经算第一次赋值了

如果参数是一个对象,final只是保证参数引用不能改变,但不会阻止修改对象内部的属性。 例如: ```java  public void method(final Student stu) {  stu.setName("John"); // 可以修改对象内部状态 } ``` 这个例子中,final防止的是把stu重新指向另一个Student对象,但不会阻止修改stu对象本身的属性。 所以,**用final关键字作为参数,主要是为了防止重新赋值参数引用,而不是防止修改参数状态**。

#### 表达式

* 以`;`结尾的一段代码，即为一个表达式
* 单独`;` 也是一个完整的表达式

###### 关于scanner用法

``````java
public class HelloWorld {
	 static Scanner sc = new Scanner(System.in);
	 static int x1 = sc.nextInt();
	 static int x2 = sc.nextInt();
	 
	 public static void main(String[] args) {
		System.out.println(x1+x2);
	}
}
``````

* 需要注意的是，如果在通过nextInt()读取了整数后，再接着读取字符串，读出来的是回车换行:"\r\n",因为nextInt仅仅读取数字信息，而不会**读取**回车换行"\r\n".

  所以，如果在业务上需要读取了整数后，接着读取字符串，那么就应该连续执行两次nextLine()，第一次是取走回车换行，第二次才是读取真正的字符串



###### 自增自减运算的先后顺序

i++; **先取值，再运算**
++i; **先运算，再取值**

<img src="C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230925173219479.png" alt="image-20230925173219479" style="zoom:50%;" />

int i = 1;

int j = ++i + i++ + ++i + ++i + i++;

j的值是多少 --- 13

###### 练习

``````java
import java.util.Scanner;

//使用Scanner收集你的身高体重，并计算出你的BMI值是多少
//BMI的计算公式是 体重(kg) / (身高*身高)
//比如体重是72kg, 身高是1.69，那么这位同学的BMI就是
//72 / (1.69*1.69) = ?

public class Bmi {
	static double weight;
	static double height;
	public static void main(String[] args) {
		double result = getBmi(weight,height);
		
		System.out.println("您的BMI值为： "+result);
	}
	public static double getBmi(double w,double h) {
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入您的体重kg");
		w = sc.nextDouble();
		System.out.println("请输入您的身高");
		h = sc.nextDouble();
		double bmi = w/(h*h);
		return bmi;
	}
}
``````

##### java的关系操作符

\> 大于
\>= 大于或等于
< 小于
<= 小于或等于
== 是否相等
==!= 是否不等==

##### java逻辑运算符

* ！ 表示取反

* ^   表示异或

  * 用于比较两个值，如果它们不相等，则结果为真（1），否则为假（0）。

  * A     B     A XOR B
    ------------------
    0     0       0
    0     1       1
    1     0       1
    1     1       0

###### 练习

``````java
int i = 1;
boolean b = !(i++ == 3) ^ (i++ ==2) && (i++==3);
System.out.println(b);
System.out.println(i);
``````

* i++先运算，再自增 -- 第一部分 (i++ == 3)为false --- (i++ ==2)为ture 由于！存在于第一部分 所以为ture ^ ture --- false --- &&右边不计算了
* i=3，b=false

``````java
		 int i = 1;
		 i+=++i;
		 System.out.println(i);
``````

* 输出的i为3 
  * 原因： i+=++i   ;   解析就是i= i + (++i);      等于号左边的看作是左边的整体,   等于号右边的看作是右边的整体,      整体上还是从左到右的,   只不过等于号赋值操作是从右到左



##### 三元操作符

``````java
public class HelloWorld {
	public static void main(String[] args) {
		int i = 5;
		int j = 6;
		int k = i < j ? 99 : 88;
		// 相当于
		if (i < j) {
			k = 99;
		} else {
			k = 88;
		}
		System.out.println(k);
	}
}
``````

练习通过[Scanner](https://how2j.cn/k/operator/operator-scanner/658.html)输入一个**1-7**之间的整数，使用三元操作符判断是工作日还是周末？

``````java
public class HelloWorld {
	static int num;
	public static void main(String[] args) {
		getDate(num);
	}
	public static void getDate(int num) {
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入一个1~7之间的整数");
		int x = sc.nextInt();
		String result = (x>=1 & x<=7)?"合理":"重新输入";
		System.out.println(result);
		num = ((result=="合理")?x:sc.nextInt());
		String judge;
		System.out.println(judge = ((num>5)?"休息":"工作"));		
	}
}
``````

#### 条件运算符

##### 练习

判断某一年是否为闰年
通过[Scanner](https://how2j.cn/k/operator/operator-scanner/658.html#step2143) 输入一个年份，然后判断该年是否是闰年

闰年判断标准(满足任何一个)

1. 如果能够被4整除，但是不能被100整除
2. 能够被400整除

``````java
public class Yearhandan {
	static int year;
	public static void main(String[] args) {
		judgeYear(year);
	}
	public static void judgeYear(int year) {
		Scanner sc = new Scanner(System.in);
		System.out.println("请输入一个年份");
		year = sc.nextInt();
		if(year%400 == 0) {
			System.out.println("闰年");
		}
		else if(year%4==0 & year%100!=0){
			System.out.println("闰年");
		}
		else {
			System.out.println("平年");
		}
	}
}
``````

##### switch

switch可以使用byte,short,int,char,String,enum

**注:** 每个表达式结束，都应该有一个break;
**注:** String在Java1.7之前是不支持的, Java从1.7开始支持switch用String的，编译后是把String转化为hash值，其实还是整数
**注:** enum是枚举类型，在[枚举](https://how2j.cn/k/class-object/class-object-enum/678.html)章节有详细讲解

**练习**通过[Scanner](https://how2j.cn/k/operator/operator-scanner/658.html#step2143) 输入月份，然后使用switch 判断季节	

``````java
public class Handan {
	static int month;
	public static void main(String[] args) {
		judge(month);
	}
	public static void judge(int year) {
		Scanner sc = new Scanner(System.in);
		
		while(true){
			System.out.println("请输入一个月份");
			int dummyMonth = sc.nextInt();
			if(dummyMonth>=1 & dummyMonth <=12) {
				month = dummyMonth;
				break;
			}else {
				System.out.println("请输入正确内容");
			}
		}
		switch(month) {
		case 1,2,3:
			System.out.println("spring");
		break;
		case 4,5,6:
			System.out.println("summer");
		break;
		case 7,8,9:
			System.out.println("autumn");
		break;
		case 10,11,12:
			System.out.println("winter");
		break;
		}		
	}
}
``````

##### while&do-while

###### 练习

通过[Scanner](https://how2j.cn/k/operator/operator-scanner/658.html#step2143) 获取一个整数，然后使用while计算这个整数的阶乘

N的阶乘等于 N* (N-1) * (N-2) * ... * 1

``````java
import java.util.Scanner;

public class Keisan {
	static int num;
	public static void main(String[] args) {
		keisan(num);
	}
	public static void keisan(int num) {
		Scanner sc = new Scanner(System.in);
		System.out.println("----- please input number ----- ");
		num = sc.nextInt();
		int count = num;
		while(num>1) {
			count*=(--num);
		}
		System.out.println(count);
	}
}
``````

##### for

###### practice

天朝有一个乞丐姓洪，去天桥要钱
第一天要了1块钱
第二天要了2块钱
第三天要了4块钱
第四天要了8块钱
以此类推

问题： 洪乞丐干10天，收入是多少？

``````java
public class Keisan {
	static int num =1;
	public static void main(String[] args) {
		keisan(num);
	}
	public static void keisan(int num) {
		int sum = 0;
		for (int i = 0; i < 10; i++) {
			sum += num;
			num *= 2;
		}
		System.out.println(sum);
	}
}
``````

##### 综合练习（循环）

``````java
//黄金分割点
//需求前置知识：关于链式数组的应用，将计算值放进去，并存储与之相关的分子分母的方式。

``````



#### 数组

* 数组是一个**固定长度**的，包含了**相同类型**数据或者具有互换性的 **容器**

##### 数组获取长度为什么使用`.length`而不是`.length() `

因为数组的长度是一个固定的属性，它在创建数组时就被确定了，而不是在运行时动态计算的。因此，使用属性而不是方法更符合数组的本质。

下面是一些关于为什么使用`length`属性的原因：

1. **性能：** 使用属性比调用方法更高效。属性的值可以在运行时立即获得，而不需要额外的方法调用开销。在大型数组上进行操作时，这可能会产生显著的性能差异。
2. **一致性：** Java编程语言中，数组是一个基本的数据结构，它的长度以属性的形式提供给开发者。与其他数据结构和集合不同，它不需要调用方法来获取其大小。使用`length`属性使Java的语法和习惯用法保持一致性。
3. **编译时检查：** 在编译时，编译器可以检查对数组长度的访问是否合法。如果您尝试使用`length()`方法而不是`length`属性，编译器将会报告错误，因为==**`length()`方法在数组上不存在**==。

##### 数组的声明&创建

###### 声明

int[] a; 声明了一个数组变量。 ---只声明并不会创建数组

###### 创建

创建数组的时候需指明数组的长度

new int[5]

###### 引用

如果变量代表一个数组，比如a,我们把a叫做**引用**
与基本类型不同
int c = 5; 这叫给c**赋值**为5
声明一个引用 int[] a;
a = new int[5];
让a这个引用，**指向**数组

==`a`中保存的是地址值==

##### 数组的三种创建方式

1. 静态

   * `int[] x1 = {};`
     * 要使用静态简便命名法`int[] a ={ }`的情况下,要注意的是, 必须要和变数宣言一起使用, 因为new创建实例`instance`时要根据`{ }`里的内容去确定`arr.length`的长度和次元等
   * `int[] x2  = new int[] {};`

   可以什么都不写`{}`中

   下列代码: `Item[] x = new Item[3];`没有赋值-->由于是参照类型-->默认值是`null`

   如果用`Item[i].method`-->执行时错误-->`NullPointerError`

2. 动态

   * `int[] x2 = new int[3];`
     * `System.out.print(clazz.getCanonicalName());` -- 结果输出的是”int[]”; 其中.getClass方法是object的方法

##### 练习

###### exec1

首先创建一个长度是5的数组
然后给数组的每一位赋予随机整数
通过for循环，遍历数组，找出最小的一个值出来

0-100的 随机整数的获取办法有多种，下面是参考办法之一:

`(int) (Math.random() * 100)`

`Math.random() `会得到一个0-1之间的随机浮点数，然后乘以100，并强转为整型即可。

``````java
public class ArrayPrac {
	static int[] x1 = new int[5];
	//动态数组创建方式
	public static void main(String[] args) {
		System.out.println("最小值为： "+checkMin(x1));
	}
	public static int checkMin(int[] x1) {
		int markNum = 100;
		for (int i = 0; i < x1.length; i++) {
//			x1[i] = (int)(Math.random()*100);
			//Math.random() 会得到一个0-1之间的随机浮点数
			//除了这个方法之外的方式
			Random r = new Random();
			x1[i] = r.nextInt(-1,100)+1;
			System.out.println("第"+i+"数是： "+x1[i]);
			//这个r的取值范围（-1，99） -- 所以要加1
			if (x1[i] < markNum) {
				markNum = x1[i];
			}
		}
		return markNum;
	}
}
``````

###### exec2

首先创建一个长度是5的数组,并填充随机数。

使用for循环或者while循环，对这个数组实现反转效果

``````java
public class ArrayPrac {
	static int[] x1 = new int[5];
	public static void main(String[] args) {
		int[] x3 = new int[5];
		x3 = checkMin(x1);
		for (int i = 0; i < x3.length; i++) {
			System.out.println(x3[i]);
		}
		System.out.println("-------end-------");
	}
	public static int[] checkMin(int[] x1) {
		int[] x2 = new int[5];
		for (int i = 0; i < x1.length; i++) {
			x1[i] = (int)(Math.random()*100);
			System.out.println("第"+i+"位数是： "+x1[i]);
			x2[x2.length -1-i] = x1[i];
		}
			return x2;
	}
}
``````

##### 数组排序

###### 选择法排序

选择法排序的思路：
**把第一位**和其他所有的进行比较，只要比第一位小的，就换到第一个位置来
比较完后，**第一位就是最小的**
然后再从**第二位**和剩余的其他所有进行比较，只要比第二位小，就换到第二个位置来
比较完后，**第二位就是第二小的**
以此类推

``````java
public class ArrayPrac {
	static Random r =new Random();
	static int a [] = new int[r.nextInt(4,9)+1];
	public static void main(String[] args) {
		chooseMin(fillNum(a));
		
	}
	//实现选择排序
	public static void chooseMin(int[] a) {
		for (int i = 0; i < a.length-1; i++) {
			//每一次给b赋值循环都需要重新定义一个记录变量。
			for (int j = i+1; j < a.length; j++) {
				if(a[i] > a[j]) {
					int temp = a[i];
					a[i] = a[j];
					a[j] = temp;
				}
			}
		}
		for (int j = 0; j < a.length; j++) {
			System.out.print(a[j]+"   ");
		}
	}
	//给数组填充值
	public static int[] fillNum(int[] a) {
		for (int i = 0; i < a.length; i++) {
			a[i] = (int)(Math.random()*100);
			System.out.println("第"+i+"位数是： "+a[i]);
		}
		return a;
	}
}
``````

###### 冒泡法排序

冒泡法排序的思路：
第一步：从第一位开始，把相邻两位进行比较
如果发现前面的比后面的大，就把大的数据交换在后面，循环比较完毕后，**最后一位就是最大的**
第二步： 再来一次，只不过不用比较最后一位
以此类推

``````java
public class HelloWorld {
    public static void main(String[] args) {
        int a [] = new int[]{18,62,68,82,65,9};
        //排序前，先把内容打印出来
        for (int i = 0; i < a.length; i++) {
            System.out.print(a[i] + " ");
        }
        System.out.println(" ");
        //冒泡法排序
      
        //第一步：从第一位开始，把相邻两位进行比较
        //如果发现前面的比后面的大，就把大的数据交换在后面
          
        for (int i = 0; i < a.length-1; i++) {
            if(a[i]>a[i+1]){  
                int temp = a[i];
                a[i] = a[i+1];
                a[i+1] = temp;
            }
        }
        //把内容打印出来
        //可以发现，最大的到了最后面
        for (int i = 0; i < a.length; i++) {
            System.out.print(a[i] + " ");
        }
        System.out.println(" ");
          
        //第二步： 再来一次，只不过不用比较最后一位
        for (int i = 0; i < a.length-2; i++) {
            if(a[i]>a[i+1]){  
                int temp = a[i];
                a[i] = a[i+1];
                a[i+1] = temp;
            }
        }
        //把内容打印出来
        //可以发现，倒数第二大的到了倒数第二个位置
        for (int i = 0; i < a.length; i++) {
            System.out.print(a[i] + " ");
        }
        System.out.println(" ");       
          
        //可以发现一个规律
        //后边界在收缩
        //所以可以在外面套一层循环
          
        for (int j = 0; j < a.length; j++) {
            for (int i = 0; i < a.length-j-1; i++) {
                if(a[i]>a[i+1]){  
                    int temp = a[i];
                    a[i] = a[i+1];
                    a[i+1] = temp;
                }
            }
        }
          
        //把内容打印出来
        for (int i = 0; i < a.length; i++) {
            System.out.print(a[i] + " ");
        }
        System.out.println(" ");       
    }
}
``````

###### 练习

首先创建一个长度是5的数组,并填充随机数。

首先用选择法正排序，然后再对其使用冒泡法倒排序

**注** 所谓的正排序就是从小到大排序，倒排序就是从大到小排序

``````java
public class ArrayPrac {
	static Random r =new Random();
	static int a [] = new int[r.nextInt(4,9)+1];
	public static void main(String[] args) {
		int b[] = fillNum(a);
		chooseMin(b);
		bubbleBack(b);
	}
	//实现选择排序 --- 正向排序
	public static void chooseMin(int[] a) {
		for (int i = 0; i < a.length-1; i++) {
			//每一次给b赋值循环都需要重新定义一个记录变量。
			for (int j = i+1; j < a.length; j++) {
				if(a[i] > a[j]) {
					int temp = a[i];
					a[i] = a[j];
					a[j] = temp;
				}
			}
		}
		for (int j = 0; j < a.length; j++) {
			System.out.print(a[j]+"   ");
		}
	}
	//bubble排序倒叙
	public static void bubbleBack(int[] a) {
		for (int j = 0; j < a.length-1; j++) {
			//将最小的数排到最后去 --- 所以需要将这个步骤重复a.length -1次
			for (int i = 0; i < a.length; i++) {
				if(i+1 == a.length) {
					break;
				}
				else if(a[i]<a[i+1]) {
					int temp = a[i];
					a[i] = a[i+1];
					a[i+1] = temp;
				}
					
			}
		}
		System.out.println(" ");
		System.out.println("----------------------------");
		for (int j = 0; j < a.length; j++) {
			System.out.print(a[j]+"   ");
		}
		
	}
	
	//给数组填充值
	public static int[] fillNum(int[] a) {
		for (int i = 0; i < a.length; i++) {
			a[i] = (int)(Math.random()*100);
			System.out.println("第"+i+"位数是： "+a[i]);
		}
		return a;
	}
}
``````

##### for循环遍历数组

###### 练习

用增强型for循环找出最大的那个数

``````java
public class ArrayPrac {
	static int[] a;
	
	public static void main(String[] args) {
		int[] b = fillNum(a);
		findMax(b);
	}
	//foreach找最大值
	public static void findMax(int[] a) {
		int markNum = a[0];
		for (int i : a) {
			if(i>markNum) {
				markNum = i;
			}
		}
		System.out.println(markNum);
	}
	//给数组填充值
	public static int[] fillNum(int[] a) {
		Random r =new Random();
		a = new int[r.nextInt(4,9)+1];
		for (int i = 0; i < a.length; i++) {
			a[i] = (int)(Math.random()*100);
			System.out.println("第"+i+"位数是： "+a[i]);
		}
		return a;
	}
}
``````

##### 复制数组

###### 官方方法

把一个数组的值，复制到另一个数组中

`System.arraycopy(src, srcPos, dest, destPos, length)`

`src`: 源数组
`srcPos`: 从源数组复制数据的起始位置
`dest`: 目标数组
`destPos`: 复制到目标数组的起始位置
`length`: 复制的长度

``````java
public class ArrayPrac {
	static int[] a;
	public static void main(String[] args) {
		int[] c = fillNum(a);
		int[] d = copyArr(c);
		readArr(d);
	}
	//复制数组
	//注意！这里要完全创建数组的原因是 -- 不初始化的话
	//赋值的时候b[i]调值就会NullPointerException
	public static int[] copyArr(int[] a) {
		int b[] = new int[a.length];
		Random r = new Random();
		int startPos = r.nextInt(0,a.length);
		int countLength = a.length-startPos;
		System.arraycopy(a, startPos, b, 0, countLength);
		return b;
	}
	
	//给数组填充值
	public static int[] fillNum(int[] a) {
		Random r =new Random();
		a = new int[r.nextInt(4,9)+1];
		for (int i = 0; i < a.length; i++) {
			a[i] = (int)(Math.random()*100);
			System.out.println("第"+i+"位数是： "+a[i]);
		}
		return a;
	}
	//遍历数组
	public static void readArr(int[] a) {
		for (int i = 0; i < a.length; i++) {
			System.out.println(a[i]);
		}
	}
}
``````

###### prac

首先准备两个数组，他俩的长度是5-10之间的随机数，并使用随机数初始化这两个数组

然后准备第三个数组，第三个数组的长度是前两个的和
通过System.arraycopy 把前两个数组合并到第三个数组中

``````java
public class ArrayPrac {
	static int[] a;
	static int[] b;
	public static void main(String[] args) {
		int[] c = fillNum(a);
		int[] d = fillNum(b);
		int[] e = mergeArr(c,d);
		readArr(e);
	}
	//组合数组
	public static int[] mergeArr(int[] x1,int[]x2) {
		int[] x = new int[x1.length+x2.length];
		System.arraycopy(x1, 0, x, 0, x1.length);
		System.arraycopy(x2,0,x,x1.length-1,x2.length);
		return x;
	}
	
	
	//给数组填充值--长度是5-10之间的随机数
	public static int[] fillNum(int[] a) {
		Random r =new Random();
		a = new int[r.nextInt(4,10)+1];
		for (int i = 0; i < a.length; i++) {
			a[i] = (int)(Math.random()*100);
			System.out.println("第"+i+"位数是： "+a[i]);
		}
		return a;
	}
	//遍历数组
	public static void readArr(int[] a) {
		for (int i = 0; i < a.length; i++) {
			System.out.print(a[i]+"   ");
		}
	}
}
``````



##### 二维数组

###### prac

定义一个5X5的二维数组。 然后使用随机数填充该二维数组。
找出这个二维数组里，最大的那个值，并打印出其二维坐标

``````java
public class ArrayPrac {
	static int[][] a = new int[5][5];
	public static void main(String[] args) {
		fillXNum(a);
		findXMax(a);
	}
	//填充多维数组
	public static void fillXNum(int[][] a) {
//		Random r = new Random();
		for (int[] is : a) {
			for (int i = 0; i < is.length; i++) {
				is[i] = (int)(Math.random()*100);
				System.out.print(is[i]+"  ");
			}
			System.out.println(" ");
		}
	}
	//寻找多维数组中的最大值
	public static void findXMax(int[][] a) {
		int count = 0;
		for (int i = 0; i < a.length; i++) {
			if(count<findMax(a[i])) {
				count = findMax(a[i]);
			}
		}
		System.out.println(count);
	}
	//foreach找最大值
	public static int findMax(int[] a) {
		int markNum = a[0];
		for (int i : a) {
			if(i>markNum) {
				markNum = i;
			}
		}
		return markNum;
	}
}
``````

#### 类和对象

##### 引用和指向

* `Hero hero = new Hero();` 这样的代码
  * 左边是声明 有一个Hero类型的变量； 变量名为hero
  * 右边是创建对象 （instance实例化） --- 这个new在内存里开辟空间，创建了Hero格式的对象
  * 等号表示了 将左边的变量指向**右边内存中的对象**
  * 直接syso hero的话可以得到该对象在内存中的地址值



##### 关于this

this的适用范围

1. 解决变量名冲突

   * 例如`this.name = name;`可以区分局部变量和成员变量

2. 在构造函数中调用其他构造函数

   * ```java
     public class MyClass {
         private int x;
         private String name;
         public MyClass() {
             this(0, "Default"); // 调用另一个构造函数
         }
         public MyClass(int x, String name) {
             this.x = x;
             this.name = name;
         }
     }
     ```

3. **在方法中返回当前对象：** 可以在方法中使用 `this` 来返回当前对象，从而支持方法链式调用。这在构建流畅的API或构建器模式时非常有用。例如：

​	

```java
public class MyClass {
    private int x;

    public MyClass setX(int x) {
        this.x = x;
        return this; // 返回当前对象以支持链式调用
    }
}
```

4. **作为方法参数传递给其他方法：** 您可以将 `this` 作为方法参数传递给其他方法，以便在方法中访问当前对象的成员。这在事件处理和回调等情况下可能会用到。



##### 传参

###### 基本类型传参

基本类型传参
在方法内，无法修改方法外的基本类型参数

###### 类类型传参

传的是地址值 --- 修改该地址值内的内容会改变外面的引用内容

在方法中，如果您将方法参数引用指向一个新的对象，**外部的引用将仍然指向原来的对象**。**方法参数是方法的局部变量**，在方法内部创建新的对象并将参数引用指向新的对象时，这只会在方法的作用域内生效，不会影响到外部的引用。

###### 浅拷贝//深拷贝//传参

**浅拷贝（Shallow Copy）**： 浅拷贝是指创建一个新对象，该对象的成员变量是原始对象的引用的副本。换句话说，浅拷贝只复制了对象的引用，而不是对象本身。这意味着原始对象和浅拷贝对象之间共享相同的成员变量，如果成员变量是可变对象，那么对其中一个对象的修改会影响到另一个对象。

**深拷贝（Deep Copy）**： 深拷贝是指创建一个新对象，该对象的成员变量是原始对象成员变量的完全副本。深拷贝会递归复制对象及其所有嵌套对象，以确保原始对象和深拷贝对象之间没有共享的引用关系。这意味着对其中一个对象的修改不会影响到另一个对象。



##### 属性初始化

分为成员变量属性初始化&& 静态变量属性初始化

* 成员变量

1. 声明该属性的时候初始化
2. 构造方法中初始化
3. 初始化块

**注意**：执行顺序是 声明 -- 初始化块 -- 构造方法

* 静态变量

1. 声明该属性的时候初始化
2. 静态初始化块



##### 单例模式singleton

单例模式又叫做 Singleton模式，指的是一个类，在一个JVM里，只有一个实例存在。

分两种：饿汉式&&懒汉式

**饿汉式**是立即加载的方式，无论是否会用到这个对象，都会加载。
如果在构造方法里写了性能消耗较大，占时较久的代码，比如建立与数据库的连接，那么就会在启动的时候感觉稍微有些卡顿。

**懒汉式**，是延迟加载的方式，只有使用的时候才会加载。 并且有[线程安全](https://how2j.cn/k/thread/thread-synchronized/355.html#step793)的考量(鉴于同学们学习的进度，暂时不对线程的章节做展开)。
使用懒汉式，在启动的时候，会感觉到比饿汉式略快，因为并没有做对象的实例化。 但是在第一次调用的时候，会进行实例化操作，感觉上就略慢。

看业务需求，如果业务上允许有比较充分的启动和初始化时间，就使用饿汉式，否则就使用懒汉式

```java
//饿汉式
public class GiantDragon {
 
    //私有化构造方法使得该类无法在外部通过new 进行实例化
    private GiantDragon(){
         
    }
 
    //准备一个类属性，指向一个实例化对象。 因为是类属性，所以只有一个
 
    private static GiantDragon instance = new GiantDragon();
     
    //public static 方法，提供给调用者获取12行定义的对象
    public static GiantDragon getInstance(){
        return instance;
    }
     
}
//懒汉式
public class GiantDragon {
  
    //私有化构造方法使得该类无法在外部通过new 进行实例化
    private GiantDragon(){       
    }
  
    //准备一个类属性，用于指向一个实例化对象，但是暂时指向null
    private static GiantDragon instance;
      
    //public static 方法，返回实例对象
    public static GiantDragon getInstance(){
        //第一次访问的时候，发现instance没有指向任何对象，这时实例化一个对象
        if(null==instance){
            instance = new GiantDragon();
        }
        //返回 instance指向的对象
        return instance;
    }
      
}
```

###### 单例模式三要素

1. 构造方法私有化
2. 静态属性指向实例
3. public static的 getInstance方法，返回第二步的静态属性

例子：

```java
public class HelloWorld {
    public static void main(String[] args) {
        
        Season season = Season.SPRING;
        switch (season) {
        case SPRING:
            System.out.println("春天");
            break;
        case SUMMER:
            System.out.println("夏天");
            break;
        case AUTUMN:
            System.out.println("秋天");
            break;
        case WINTER:
            System.out.println("冬天");
            break;
        }
    }
}
```



##### 枚举类型

枚举enum是一种特殊的类(还是类)，使用枚举可以很方便的定义常量



#### 接口与继承（多态）

##### 在多态中，方法调用遵循以下原则：

1. **方法签名必须一致：** 多态中，不同类的对象可以对相同的方法进行调用，但这些方法必须有相同的方法签名（==方法名称、参数列表和返回类型相同==）。 --- override的要求
2. **实际对象决定方法的具体实现：** 虽然多个不同类的对象可以对相同的方法进行调用，但最终执行的方法取决于实际对象的类型。这被称为动态绑定（Dynamic Binding）或运行时多态。 ---==编译看左边，运行看右边==
3. **方法必须在超类或接口中声明：** 在多态中，方法必须在超类或接口中声明。子类可以选择是否覆盖（重写）这些方法，从而提供自己的实现。 --- 也可以有自己单独的方法，但那就不是多态的体现了

###### 动态绑定 && 运行时多态

动态绑定（Dynamic Binding）或运行时多态（Runtime Polymorphism）是Java中面向对象编程的一个重要特性。它允许在运行时决定要调用哪个方法的实现，而不是在编译时确定。这使得代码更加灵活，能够适应不同类型的对象。

在Java中，动态绑定的实现是通过方法重写（Method Overriding）和虚方法表（Virtual Method Table）来实现的。以下是关于动态绑定的重要概念：

1. **方法重写（Method Overriding）：** 在子类中可以重写（覆盖）父类的方法，前提是方法具有相同的名称、参数列表和返回类型。子类的方法覆盖了父类的方法，但父类引用指向子类对象时，调用该方法时会执行子类的实现。
2. **虚方法表（Virtual Method Table，VTable）：** Java编译器会为每个类创建一个虚方法表，其中包含了该类及其父类的虚方法（即可重写的方法）的引用。在运行时，Java虚拟机根据对象的实际类型查找虚方法表，以确定要调用哪个方法的实现。



##### 静态方法&&override

在Java中，静态方法（static methods）不能被重写（override）。静态方法是与类相关联的方法，而不是与对象相关联的方法。因此，它们不属于对象的行为，而是属于类的行为。因为静态方法是通过类名而不是实例调用的，所以它们不会根据对象的类型而变化，也就没有必要重写。



##### 对象转型

所谓的转型，是指当**引用类型**和**对象类型**不一致的时候，才需要进行类型转换
类型转换有时候会成功一个很简单的判别办法
**把右边的当做左边来用**，看说得通不



##### 子类构造器&& 父类构造器

###### 默认调用父类无参constructor

子类构造器会默认调用父类的无参构造器

也可以用super关键字去调用父类的其他构造器

###### super和this关键字在构造器中的使用

1. **`super` 和 `this` 的调用必须在构造器的第一行：** 无论是调用父类构造器还是本类其他构造器，都必须在构造器的第一行使用这些关键字。

所以使用时注意不能让两者在同一个constructor中都调用构造方法。



##### 超类 Object

1. Object类是所有类的父类
2. 它的子类继承了他的一些方法
   1. toString()
   2. equals() --- 与`==`相比，`==`是比较引用是否相同（地址值）
   3. hashCode()
   4. getClass() --- 返回一个对象的类对象
   5. finalize（） --- 没有指向时，被垃圾回收，由虚拟机调用



##### final

1. 修饰类 ---- 不能被继承
2. 修饰方法 ---- 不能被重写
3. 修饰引用 ---- 只能指向一次



##### 抽象类和接口的区别

区别1：
子类只能继承一个抽象类，不能继承多个
子类可以实现**多个**接口
区别2：
抽象类可以定义
public,protected,package,private
静态和非静态属性
final和非final属性
但是接口中声明的属性，只能是
public
静态
final的
即便没有显式的声明

注: 抽象类和接口都可以有实体方法。 接口中的实体方法，叫做[默认方法](https://how2j.cn/k/interface-inheritance/interface-inheritance-default-method/676.html)

###### 接口中可包含

1. **抽象方法**
   * 只有方法签名（方法名、参数列表和返回类型）。实现该接口的类必须提供这些方法的具体实现。
   * **接口中必须包含抽象方法**
2. **默认方法（Default Methods）**
   * 默认方法允许在不破坏现有实现的情况下向接口添加新方法。
3. **静态方法（Static Methods）**
   * 可以直接通过接口名称调用
4. **常量**
   * 接口可以包含常量，这些常量==默认是 `public`、`static` 和 `final` 的==。它们通常用于定义常量值，因此在实现类中可以直接使用这些常量。

###### 为什么接口要用public

在Java中，接口中的成员（包括抽象方法、默认方法、静态方法和常量）默认都是 `public` 访问修饰符的，这是因为接口的主要目的是定义一组公共的行为规范，供多个类来实现。这种设计有以下原因：

1. **接口是一种契约：** 接口定义了一组公共方法，表示了实现该接口的类必须提供的一组行为。这些方法是类与类之间的契约，用于确保类之间的一致性。因此，接口中的方法应该是公共的，以便所有实现类都能遵守这个契约。
2. **实现多态性：** 接口在实现多态性方面非常有用。通过将对象引用声明为接口类型，可以使代码更加通用，以适应不同的实现类。因为接口中的方法是公共的，所以可以在任何实现类上调用这些方法，而不需要访问权限。 --- 例如people和cat都有eat行为  --- 将eat定义为接口
3. **可访问性和可见性：** 默认情况下，接口中的成员都是 `public`，这意味着它们对所有类都可见和可访问。这符合了接口的设计目标，即为外部世界提供一组公共行为规范。

虽然接口中的成员默认是 `public`，但可以通过在成员前面添加 `private`、`protected` 或包级别的访问修饰符来限制其访问性。但需要注意的是，这些限制访问性的修饰符只能用于默认方法和静态方法，不能用于接口中的抽象方法和常量，因为它们默认就是 `public` 的。

所以静态方法和默认方法就可以限制可见性 --- 因为不是需要实现接口的人去修改该内容的，所以不一定需要public

###### 抽象类可以包含

1. 抽象方法
   * 抽象类的存在有时候是为了提供一些通用的行为或属性，而不一定需要强制子类来实现抽象方法。
   * 抽象类不一定非要包含抽象方法
2. 具体方法
3. 构造方法
   * 抽象类可以有构造方法，用于初始化抽象类的对象。子类在实例化时会调用父类的构造方法。
4. 成员变量

###### 抽象类不能instance化，但仍然有构造器的原因

1. **初始化共享的状态：** 抽象类可以包含实例变量（成员变量），这些变量用于存储对象的状态。构造器允许在创建抽象类的子类对象时初始化这些共享的状态，确保对象的一致性和正确性。子类在实例化时会调用父类的构造方法来执行初始化工作。
2. **定义构造流程：** 抽象类的构造方法可以定义对象的创建和初始化流程。这对于确保对象的正确初始化非常重要。构造方法可以执行一些通用的初始化步骤，然后由子类来扩展或调整这个过程。
3. **传递参数：** 构造方法可以接受参数，这些参数可以用于初始化对象的状态。通过构造方法，可以将参数传递给抽象类，并在其中进行处理。子类在实例化时也可以传递参数给父类的构造方法。

虽然抽象类不能直接实例化，但它的构造方法可以在子类实例化时被调用，以确保对象的正确初始化。抽象类的构造方法通常会被子类的构造方法显式或隐式地调用，以便完成对象的初始化过程。

需要注意的是，抽象类的构造方法可以是 `public`、`protected` 或包级别的，但不能是 `private`。这是因为子类需要能够访问父类的构造方法来进行初始化。



##### 内部类

###### 内部类的作用

1. **封装和隐藏：** 内部类可以访问其外部类的成员，包括私有成员。这允许你将相关的类组织在一起，并将实现细节隐藏在内部类中，从而提高了封装性和安全性。
2. **代码组织：** 内部类可以用于将相关的类放在一起，使代码更具有组织性和可读性。这对于大型项目中的复杂类结构非常有用。
3. **实现多重继承：** Java不支持多重继承，但你可以使用内部类实现类似多重继承的效果。你可以在一个类中包含多个内部类，每个内部类可以继承不同的类或实现不同的接口。
4. **回调和事件处理：** 内部类可以用于实现回调函数和事件处理机制。例如，Swing GUI应用程序经常使用内部类来处理用户事件。
5. **实现迭代器和集合：** 内部类可以用于实现迭代器和集合类。它们可以访问外部类的私有成员，并提供更灵活的迭代器实现。
6. **实现工厂模式：** 内部类可以用于实现工厂模式，其中内部类用于创建外部类的实例，同时隐藏实现细节。

```java
public class ShapeFactory {
    // 内部工厂类，用于创建图形对象
    private class CircleFactory implements Shape {
        @Override
        public void draw() {
            new Circle().draw();
        }
    }

    private class RectangleFactory implements Shape {
        @Override
        public void draw() {
            new Rectangle().draw();
        }
    }

    // 公共方法，根据参数创建图形对象
    public Shape createShape(String shapeType) {
        if ("circle".equalsIgnoreCase(shapeType)) {
            return new CircleFactory();
        } else if ("rectangle".equalsIgnoreCase(shapeType)) {
            return new RectangleFactory();
        } else {
            throw new IllegalArgumentException("不支持的图形类型");
        }
    }
}

```

这种使用内部类的工厂模式可以有效地隐藏对象创建的细节，提高了代码的封装性和可维护性。同时，它还允许你在工厂内部轻松地扩展支持更多的图形类型，而不必修改客户端代码。

7. **实现单例模式：** 内部类可以用于实现线程安全的单例模式。通过在内部类中创建单例对象，可以延迟加载并确保只有一个实例。

   * 内部类实现单例模式是一种常见的用法，因为它可以实现延迟加载（懒汉模式）和线程安全，同时也隐藏了单例类的实现细节。

   * ```java
     public class Singleton {
         // 私有构造方法，防止外部实例化
         private Singleton() {
         }
     
         // 使用静态内部类来实现单例
         private static class SingletonHolder {
             // 在内部类中创建单例实例
             private static final Singleton INSTANCE = new Singleton();
         }
     
         // 公共方法，返回单例实例
         public static Singleton getInstance() {
             return SingletonHolder.INSTANCE;
         }
     }
     
     ```

     

8. **访问外部类的私有成员：** 内部类可以访问外部类的私有成员，这对于某些特定的设计需求很有用，但需要小心使用以确保数据安全性。

###### 内部类分类

非静态内部类
静态内部类
匿名类
本地类

###### 在匿名类中使用外部的局部变量

在匿名类中使用外部的局部变量，外部的局部变量必须修饰为final

在jdk8中，已经不需要强制修饰成final了，如果没有写final，不会报错，因为编译器**偷偷的**帮你加上了看不见的final

```java
public abstract class Hero {
 
    public abstract void attack();
      
    public static void main(String[] args) {
 
        //在匿名类中使用外部的局部变量damage 必须修饰为final
        int damage = 5;
         
        //这里使用本地类AnonymousHero来模拟匿名类的隐藏属性机制
         
        //事实上的匿名类，会在匿名类里声明一个damage属性，并且使用构造方法初始化该属性的值
        //在attack中使用的damage，真正使用的是这个内部damage，而非外部damage
         
        //假设外部属性不需要声明为final
        //那么在attack中修改damage的值，就会被暗示为修改了外部变量damage的值
         
        //但是他们俩是不同的变量，是不可能修改外部变量damage的
        //所以为了避免产生误导，外部的damage必须声明为final,"看上去"就不能修改了
        class AnonymousHero extends Hero{
            int damage;
            public AnonymousHero(int damage){
                this.damage = damage;
            }
            public void attack() {
                damage = 10;
                System.out.printf("新的进攻手段，造成%d点伤害",this.damage );
            }
        }
         
        Hero h = new AnonymousHero(damage);
         
    }
      
}
```



#### 数字与字符串

##### 装箱&& 拆箱

* 注意byte和Integer这种不能互相拆装箱 --- 必须要对应

```java
public class StringPrac {
	public static void main(String[] args) {
		int x1 = 50;
		byte x2 = 12;
		//注意如果使用第13行代码也不会报错 --- 因为int格式的参数传入byte可以自动转变为int；反之则不行
		testAutoIn(x1);
		testAutoIn(x2);
		
		Byte x3 = 4;
		Integer x4 = 5;
		//不能存在自动转换功能，必须overload
		testAutoOut(x3);
		testAutoOut(x4);
		//找寻Byte的最大值
		System.out.println(Byte.MAX_VALUE+"-----------");
		
	}

	// 测试byte和Integer是否能自动装箱
//	public static void testAutoIn1(byte x1) {
	public static void testAutoIn(byte x1) {
		Byte x2 = x1;
		System.out.println(x2.toString());
	}
	public static void testAutoIn(int x1) {
		Integer x2 = x1;
		System.out.println(x2.toString());
	}
	//测试Byte和Integer能否自动拆箱
	public static void testAutoOut(Integer x1) {
		int x2 = x1;
		System.out.println(x1);
	}
	public static void testAutoOut(Byte x1) {
		byte x2 = x1;
		System.out.println(x1);
	}
	
}
```

##### 数字字符串转换

1. 数字转换为字符串

   1. 方法1：

      ```java
      	int x1 = 12;
      	Integer x2 = x1;
      	String str = x2.toString();
      ```

      方法2：

      ```java
      	int x1 = 12;
      	String str = String.valueOf(x1);
      ```

2. 字符串转数字

```java
	int x1 = 12;
	String str = String.valueOf(x1);
	int x3 = Integer.parseInt(str);

	double x1 = 12;
	String str = String.valueOf(x1);
	double x3 = Double.parseDouble(str);
```

如果字符串是 3.1a4，转换为浮点数会得到什么？ ---- 会报错



##### Math方法

java.lang.Math提供了一些常用的数学运算方法，并且都是以静态方法的形式存在

```java
public class TestNumber {
  
    public static void main(String[] args) {
        float f1 = 5.4f;
        float f2 = 5.5f;
        //5.4四舍五入即5
        System.out.println(Math.round(f1));
        //5.5四舍五入即6
        System.out.println(Math.round(f2));
         
        //得到一个0-1之间的随机浮点数（取不到1）
        System.out.println(Math.random());
         
        //得到一个0-10之间的随机整数 （取不到10）
        System.out.println((int)( Math.random()*10));
        //开方
        System.out.println(Math.sqrt(9));
        //次方（2的4次方）
        System.out.println(Math.pow(2,4));
         
        //π
        System.out.println(Math.PI);
         
        //自然常数
        System.out.println(Math.E);
    }
}
```



##### PRINTF或FORMAT 进行格式化输出

%s 表示字符串
%d 表示数字
%n 表示换行

```java
public class TestNumber {
  
    public static void main(String[] args) {
 
        String name ="盖伦";
        int kill = 8;
        String title="超神";
         
        //直接使用+进行字符串连接，编码感觉会比较繁琐，并且维护性差,易读性差
        String sentence = name+ " 在进行了连续 " + kill + " 次击杀后，获得了 " + title +" 的称号";
         
        System.out.println(sentence);
         
        //使用格式化输出
        //%s表示字符串，%d表示数字,%n表示换行
        String sentenceFormat ="%s 在进行了连续 %d 次击杀后，获得了 %s 的称号%n";
        System.out.printf(sentenceFormat,name,kill,title);
         
    }
}
```

printf和format能够达到一模一样的效果，通过eclipse查看java源代码可以看到，在printf中直接调用了format

```java
public class TestNumber {
  
    public static void main(String[] args) {
 
        String name ="盖伦";
        int kill = 8;
        String title="超神";
         
        String sentenceFormat ="%s 在进行了连续 %d 次击杀后，获得了 %s 的称号%n";
        //使用printf格式化输出
        System.out.printf(sentenceFormat,name,kill,title);
        //使用format格式化输出
        System.out.format(sentenceFormat,name,kill,title);
         
    }
}
```

###### 换行符

**换行符**就是另起一行 --- '\n' 换行（newline）
**回车符**就是回到一行的开头 --- '\r' 回车（return）
在eclipse里敲一个回车，实际上是**回车换行符**
Java是跨平台的编程语言，同样的代码，可以在不同的平台使用，比如Windows,Linux,Mac
然而在不同的操作系统，换行符是不一样的
（1）在DOS和Windows中，每行结尾是 “\r\n”；
（2）Linux系统里，每行结尾只有 “\n”；
（3）Mac系统里，每行结尾是只有 "\r"。
为了使得同一个java程序的换行符在所有的操作系统中都有一样的表现，使用%n，就可以做到平台无关的换行

###### 总长度，左对齐，补0，千位分隔符，小数点位数，本地化表达

```java
import java.util.Locale;
   
public class TestNumber {
   
    public static void main(String[] args) {
        int year = 2020;
        //总长度，左对齐，补0，千位分隔符，小数点位数，本地化表达
          
        //直接打印数字
        System.out.format("%d%n",year);
        //总长度是8,默认右对齐
        System.out.format("%8d%n",year);
        //总长度是8,左对齐
        System.out.format("%-8d%n",year);
        //总长度是8,不够补0
        System.out.format("%08d%n",year);
        //千位分隔符
        System.out.format("%,8d%n",year*10000);
  
        //小数点位数
        System.out.format("%.2f%n",Math.PI);
          
        //不同国家的千位分隔符
        System.out.format(Locale.FRANCE,"%,.2f%n",Math.PI*10000);
        System.out.format(Locale.US,"%,.2f%n",Math.PI*10000);
        System.out.format(Locale.UK,"%,.2f%n",Math.PI*10000);
          
    }
}
```



##### char和character

* char的包装类是character

###### Character常见方法

```java
public class TestChar {
 
    public static void main(String[] args) {
         
        System.out.println(Character.isLetter('a'));//判断是否为字母
        System.out.println(Character.isDigit('a')); //判断是否为数字
        System.out.println(Character.isWhitespace(' ')); //是否是空白
        System.out.println(Character.isUpperCase('a')); //是否是大写
        System.out.println(Character.isLowerCase('a')); //是否是小写
         
        System.out.println(Character.toUpperCase('a')); //转换为大写
        System.out.println(Character.toLowerCase('A')); //转换为小写
 
        String a = 'a'; //不能够直接把一个字符转换成字符串
        String a2 = Character.toString('a'); //转换为字符串
         
    }
}
```

###### 常见转义

```java
public class TestChar {
  
    public static void main(String[] args) {
        System.out.println("使用空格无法达到对齐的效果");
        System.out.println("abc def");
        System.out.println("ab def");
        System.out.println("a def");
          
        System.out.println("使用\\t制表符可以达到对齐的效果");
        System.out.println("abc\tdef");
        System.out.println("ab\tdef");
        System.out.println("a\tdef");
         
        System.out.println("一个\\t制表符长度是8");
        System.out.println("12345678def");
          
        System.out.println("换行符 \\n");
        System.out.println("abc\ndef");
 
        System.out.println("单引号 \\'");
        System.out.println("abc\'def");
        System.out.println("双引号 \\\"");
        System.out.println("abc\"def");
        System.out.println("反斜杠本身 \\");
        System.out.println("abc\\def");
    }
}
```

###### prac

通过[Scanner](https://how2j.cn/k/operator/operator-scanner/658.html#step2330)从控制台读取字符串，然后把字符串转换为字符数组

```java
public class StringPrac {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("please input:");
		String str = new String(sc.next());
//		在Java中，Scanner 类没有 nextString() 方法，
//		而是提供了 next() 方法来读取下一个以空白字符（空格、制表符、换行符等）分隔的字符串。
//		这是因为在Java中，字符串通常是以空格或其他空白字符分隔的，
//		因此 next() 方法可以满足大多数情况下的字符串读取需求。
//		如果你需要读取整行文本而不考虑分隔符，可以使用 nextLine() 方法，它会读取整行文本，包括空格。
		char[] cs = str.toCharArray();
		System.out.println("-----------------");
		System.out.println(cs.toString()); //object类的toString默认返回地址，输出的是地址值
//      它会返回数组的内容而不是地址值：
		System.out.println("-----------------");
		for (int i = 0; i < cs.length; i++) {
			System.out.print(cs[i]+" ");
		}
	}
}

结果：
please input:
delicious dog
-----------------
[C@7f63425a
-----------------
d e l i c i o u s 
```



##### 字符串

###### 字符串创建方法

```java
public class TestString {
 
    public static void main(String[] args) {
        String garen ="盖伦"; //字面值,虚拟机碰到字面值就会创建一个字符串对象
         
        String teemo = new String("提莫"); //创建了两个字符串对象
         
        char[] cs = new char[]{'崔','斯','特'};
         
        String hero = new String(cs);//  通过字符数组创建一个字符串对象
         
        String hero3 = garen + teemo;//  通过+加号进行字符串拼接
    }
}
```

###### 字符串长度

```java
        String unknowHero = "";
         
        //可以有长度为0的字符串,即空字符串
        System.out.println(unknowHero.length());
```

###### prac

创建一个长度是5的随机字符串，随机字符有可能是数字，大写字母或者小写字母

```java

import java.util.Arrays;
import java.util.Random;
import java.util.Scanner;

//创建一个长度是5的随机字符串，随机字符有可能是数字，大写字母或者小写字母
//需要知道ascii码表中a~zA~Z以及数字的编号
public class StringPrac {
	public static void main(String[] args) {
		char[] c = {'A','Z','a','z','0','9'};
		Scanner sc = new Scanner(System.in);
		System.out.println("please input word:");
		System.out.println(changeStr(sc.next(),c));
	}
	//查询ascii码表中的编号问题
	public static void lookup() {
		char x1 = 'a';
		int x2 = (int)x1 - 0;
		System.out.println(x2);
	}
	
	//实现传入字符自动替换为随机功能
	public static String changeStr(String word,char[] c) {
		char[] x = word.toCharArray();
		//由于查询范围是两两一组，所以只需要一维数组长度等于查询用的char【】的长度的一半
		short[][] x1 = new short[c.length/2][2];
		int[] t_mark = lookup2(c);
		//为了防止传入的char[] c不是按照大小顺序写的，要给数组排序
		Arrays.sort(t_mark);
		for (int i = 0; i < t_mark.length/2; i++) {
			x1[i][0] = (short)t_mark[i*2]; 
			x1[i][1] = (short)t_mark[i*2+1];
		}
		//每个字符循环替换
		Random r = new Random();
		for (int i = 0; i < x.length; i++) {
			int a =r.nextInt(0,x1.length);
			x[i] = (char)r.nextInt(x1[a][0],x1[a][1]);
		}
		String result = new String(x);
		System.out.println("--------------------");
		System.out.println("最终答案如下");
		return result;
	}
	
	//查询方法2 -- 传入想要查询的内容数组即可
	public static int[] lookup2(char[] c) {
		int[] x = new int[6];
		char[] x2 = c; 
		for (int i = 0; i < x.length; i++) {
			x[i] = changeTo(x2[i]);
		}
		for(int i=0;i<x.length/2;i++) {
			String str  = "范围%s~%s为%d~%d";
			StringBuffer sb = new StringBuffer();
			sb.append(new String(x2));
//			String result = sb.subSequence(i*2, i*2+2).toString();
//			在这里，sb.subSequence(i*2, i*2+2)
//			返回一个 CharSequence，然后调用了 toString() 
//			方法将其转换为 String。
//			但是，虽然 toString() 方法会返回一个新的 String 对象，
//			但它并没有复制整个字符序列，而是返回了原始字符序列的一个子序列的视图，
//			因此 result 和 sb 共享相同的字符数据。
//			因此，当你后续在 result 中进行子字符串的提取时，
//			实际上是在原始字符序列上进行操作，这可能会导致问题。
			String result = sb.substring(i*2, i*2+2).toString();
			String r1 = result.toString().substring(0, 1);
			String r2 = result.toString().substring(1);
			//使用subsequence后StringBuffer就会变成CharSequence ---》不可变了
			int startPos = x[i*2];
			int endPos = x[i*2+1];
//			System.out.println(str,r1,r2,startPos,endPos);
//			System.out.println() 方法接受一个参数，它是要打印的字符串。
//			但是，你在 System.out.println() 中传递了多个参数，其中包括多个字符串和整数。
			//所以要使用formatted方法
			String outPut = String.format(str, r1,r2,startPos,endPos);
			System.out.println(outPut);
			System.out.println("--------------------------------");
		}
		System.out.println(Arrays.toString(x));
		return x;
	}
	//数据转换用meth
	public static short changeTo(char x) {
		short x1 = (short)x;
		return x1;
	}
}
```

```
please input word:
nihaowoshimnide
范围A~Z为65~90
--------------------------------
范围a~z为97~122
--------------------------------
范围0~9为48~57
--------------------------------
[65, 90, 97, 122, 48, 57]
--------------------
最终答案如下
K5iq1ti34T430UF
```

###### prac2

创建一个长度是8的字符串数组
使用8个长度是5的随机字符串初始化这个数组
对这个数组进行排序，按照每个字符串的首字母排序(无视大小写)

```java
import java.util.Arrays;
import java.util.Iterator;
import java.util.Random;
import java.util.Scanner;

//创建一个长度是8的字符串数组
//使用8个长度是5的随机字符串初始化这个数组
//对这个数组进行排序，按照每个字符串的首字母排序(无视大小写)
//注1： 不能使用Arrays.sort() 要自己写
//注2： 无视大小写，即 Axxxx 和 axxxxx 没有先后顺序
public class StringPrac {
	public static void main(String[] args) {
		String[] strArr = new String[8];
		turnJudge(fillIn(strArr));
	}
	//填充字符串数组
	public static String[] fillIn(String[] x) {
		char[] a = {'A','Z','a','z','0','9'};
		for (int i = 0; i < x.length; i++) {
			char[] c = new char[x.length-3];
			for (int j = 0; j < c.length; j++) {
				c[j] = '1';
			}
			String str = new String(c);
			x[i] = changeStr(str,a);
		}
		return x;
	}
	//排序功能
	public static void turnJudge(String[] x) {
		System.out.println("-----------最初的字符串数组------------");
		System.out.println(Arrays.toString(x));
		short[] turnMark = new short[x.length];
		for (int i = 0; i < x.length; i++) {
			char[] charSet = x[i].toUpperCase().toCharArray();
			System.out.println("-----------查看是否都转换为2大写------------");
			System.out.println(Arrays.toString(charSet));
			turnMark[i] = (short)charSet[0];
		}
		//标记顺序
		int[] num = new int[turnMark.length];
		for (int i = 0; i < num.length; i++) {
			num[i]=i;
		}
		System.out.println("-----------排序前------------");
		System.out.println(Arrays.toString(turnMark));
		System.out.println(Arrays.toString(num));
		//开始排序
		for (int i = 0; i < num.length; i++) {
			for (int j = 0; j < num.length; j++) {
				if(turnMark[i]<turnMark[j]) {
					short temp = turnMark[i];
					turnMark[i] = turnMark[j];
					turnMark[j] = temp;
					int temp1 = num[i];
					num[i] = num[j];
					num[j] = temp1;
				}
			}
		}

		System.out.println("-----------排序后------------");
		System.out.println(Arrays.toString(turnMark));
		System.out.println(Arrays.toString(num));
		//根据顺序替换原有String[]
		String[] result = new String[x.length];
		for (int i = 0; i < result.length; i++) {
			result[i] = x[num[i]];
		}
		System.out.println("-----------字符串arr排序前------------");
		System.out.println(Arrays.toString(x));
		System.out.println("-----------字符串arr排序后------------");
		System.out.println(Arrays.toString(result));
	}
	
	
	
	//实现传入字符自动替换为随机功能
	public static String changeStr(String word,char[] c) {
		char[] x = word.toCharArray();
		//由于查询范围是两两一组，所以只需要一维数组长度等于查询用的char【】的长度的一半
		short[][] x1 = new short[c.length/2][2];
		int[] t_mark = lookup2(c);
		//为了防止传入的char[] c不是按照大小顺序写的，要给数组排序
		Arrays.sort(t_mark);
		for (int i = 0; i < t_mark.length/2; i++) {
			x1[i][0] = (short)t_mark[i*2]; 
			x1[i][1] = (short)t_mark[i*2+1];
		}
		//每个字符循环替换
		Random r = new Random();
		for (int i = 0; i < x.length; i++) {
			int a =r.nextInt(0,x1.length);
			x[i] = (char)r.nextInt(x1[a][0],x1[a][1]);
		}
		String result = new String(x);
		System.out.println("--------------------");
		System.out.println("最终答案如下");
		return result;
	}
	
	//查询方法2 -- 传入想要查询的内容数组即可
	public static int[] lookup2(char[] c) {
		int[] x = new int[6];
		char[] x2 = c; 
		for (int i = 0; i < x.length; i++) {
			x[i] = changeTo(x2[i]);
		}
		for(int i=0;i<x.length/2;i++) {
			String str  = "范围%s~%s为%d~%d";
			StringBuffer sb = new StringBuffer();
			sb.append(new String(x2));
//			String result = sb.subSequence(i*2, i*2+2).toString();
//			在这里，sb.subSequence(i*2, i*2+2)
//			返回一个 CharSequence，然后调用了 toString() 
//			方法将其转换为 String。
//			但是，虽然 toString() 方法会返回一个新的 String 对象，
//			但它并没有复制整个字符序列，而是返回了原始字符序列的一个子序列的视图，
//			因此 result 和 sb 共享相同的字符数据。
//			因此，当你后续在 result 中进行子字符串的提取时，
//			实际上是在原始字符序列上进行操作，这可能会导致问题。
			String result = sb.substring(i*2, i*2+2).toString();
			String r1 = result.toString().substring(0, 1);
			String r2 = result.toString().substring(1);
			//使用subsequence后StringBuffer就会变成CharSequence ---》不可变了
			int startPos = x[i*2];
			int endPos = x[i*2+1];
//			System.out.println(str,r1,r2,startPos,endPos);
//			System.out.println() 方法接受一个参数，它是要打印的字符串。
//			但是，你在 System.out.println() 中传递了多个参数，其中包括多个字符串和整数。
			//所以要使用formatted方法
			String outPut = String.format(str, r1,r2,startPos,endPos);
			System.out.println(outPut);
			System.out.println("--------------------------------");
		}
		System.out.println(Arrays.toString(x));
		return x;
	}
	//数据转换用meth
	public static short changeTo(char x) {
		short x1 = (short)x;
		return x1;
	}
}
```

###### prac3

1. 生成一个长度是3的[随机字符串](https://how2j.cn/k/number-string/number-string-string/324.html#step2361)，把这个字符串作为当做密码

2. 使用穷举法生成长度是3个字符串，匹配上述生成的密码
   要求： 分别使用多层for循环 和 递归解决上述问题

```java

```

###### 关于递归

递归是一种在计算机编程中经常使用的概念，它指的是一个函数或方法在其定义中调用自己的过程。递归函数通常用于解决可以分解成较小相似子问题的问题，每次调用时问题规模都会减小，直到达到基本情况或终止条件，然后逐层返回结果，最终得到问题的解。

递归包括两个关键部分：

1. **递归调用（Recursive Call）：** 在函数或方法的定义中，它调用自身以处理较小规模的问题。这是递归的核心。
2. **基本情况（Base Case）：** 递归函数必须定义一个或多个基本情况，这些情况是问题规模已经足够小，不再需要递归调用的情况。基本情况确保递归不会无限循环，而是在某个时候结束。

递归的经典示例包括计算阶乘、计算斐波那契数列、树的遍历（如二叉树）、解决迷宫问题、图的深度优先搜索等。

下面是一个简单的示例，计算一个正整数的阶乘，使用递归实现

```java
public class Main {
    public static void main(String[] args) {
        int n = 5;
        int factorial = calculateFactorial(n);
        System.out.println("Factorial of " + n + " is " + factorial);
    }

    // 递归函数计算阶乘
    public static int calculateFactorial(int n) {
        // 基本情况：当 n 为 0 或 1 时，阶乘为 1
        if (n == 0 || n == 1) {
            return 1;
        }
        // 递归调用：n 的阶乘等于 n 乘以 (n-1) 的阶乘
        return n * calculateFactorial(n - 1);
    }
}
```

##### 操作字符串

###### charAt(int index) 获取指定位置的字符

```java
public class TestArr {
    public static void main(String[] args) {
        String sentence = "盖伦,在进行了连续8次击杀后,获得了 超神 的称号";    
        char c = sentence.charAt(0);        
        System.out.println(c);         
    }
}
```

###### toCharArray( ) 获取对应的字符数组

```java
public class TestArr {
    public static void main(String[] args) {  
        String sentence = "盖伦,在进行了连续8次击杀后,获得了 超神 的称号";
        char[] c = sentence.toCharArray();
        System.out.println(c.length);    
    }
}
```

###### subString 截取子字符串

![image-20231002101326056](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20231002101326056.png)

```java
public class TestArr {
    public static void main(String[] args) {  
        String sentence = "盖伦,在进行了连续8次击杀后,获得了 超神 的称号";
        String str1 = sentence.substring(3);
        String str2 = sentence.substring(4,7);
        System.out.println(str1);    
        System.out.println(str2);
    }
}
```

###### split 根据分隔符进行分隔

```java
public class TestArr {
    public static void main(String[] args) {  
        String sentence = "盖伦,在进行了连续8次击杀后,获得了 超神 的称号";
        //根据,进行分割，得到3个子字符串
        String subSentences[] = sentence.split("了");
        for (String sub : subSentences) {
            System.out.println(sub);
        }
    }
}
```

**输出结果**

```
盖伦,在进行
连续8次击杀后,获得
 超神 的称号
```

分隔符不会被显示出来

###### trim 去掉首尾空格

```java
public class TestArr {
    public static void main(String[] args) {  
        String sentence = "        盖伦,在进行了连续8次击杀后,获得了 超神 的称号      ";
        System.out.println(sentence);
        //去掉首尾空格
        System.out.println(sentence.trim());
    }
}
```

###### 大小写

toLowerCase 全部变成小写
toUpperCase 全部变成大写

```Java
        String sentence = "Garen";
         
        //全部变成小写
        System.out.println(sentence.toLowerCase());
        //全部变成大写
        System.out.println(sentence.toUpperCase());
```

###### 定位

indexOf 判断字符或者子字符串出现的位置
contains 是否包含子字符串

```java
        String sentence = "盖伦,在进行了连续8次击杀后,获得了超神 的称号";
  
        System.out.println(sentence.indexOf('8')); //字符第一次出现的位置
          
        System.out.println(sentence.indexOf("超神")); //字符串第一次出现的位置
          
        System.out.println(sentence.lastIndexOf("了")); //字符串最后出现的位置
          
        System.out.println(sentence.indexOf(',',5)); //从位置5开始，出现的第一次,的位置
          
        System.out.println(sentence.contains("击杀")); //是否包含字符串"击杀"
```

###### 替换

replaceAll 替换所有的
replaceFirst 只替换第一个

```java
        String sentence = "盖伦,在进行了连续8次击杀后,获得了超神 的称号";
        String temp = sentence.replaceAll("击杀", "被击杀"); //替换所有的
//注意这都是不改变原来的sentence内容，返回值是新的内容
        temp = temp.replaceAll("超神", "超鬼");
        System.out.println(temp);
        temp = sentence.replaceFirst(",","");//只替换第一个
        System.out.println(temp);
```

###### prac1

给出一句英文句子： "let there be light"
得到一个新的字符串，每个单词的首字母都转换为大写

```java
    public static void main(String[] args) {
//      给出一句英文句子： "let there be light"
//      得到一个新的字符串，每个单词的首字母都转换为大写
        String s = "let there be light";
        System.out.println(s);
        String[] words = s.split(" ");
        for (int i = 0; i < words.length; i++) {
            String word = words[i];
            char upperCaseFirstWord =Character.toUpperCase(word.charAt(0));
            String rest = word.substring(1);
            String capitalizedWord = upperCaseFirstWord + rest;
            words[i]  = capitalizedWord;
        }
        String result = "";
        for (String word : words) {
            result+= word + " ";
        }
        result= result.trim();
        System.out.println(result);
    }
}
```

###### prac2

英文绕口令
peter piper picked a peck of pickled peppers
统计这段绕口令有多少个以p开头的单词

```Java
public class TestArr2 {
	public static void main(String[] args) {
		String hon = "peter piper picked a peck of pickled peppers";
		String[] honSplit = hon.split(" ");
		int count = 0;
		for (int i = 0; i < honSplit.length; i++) {
			System.out.print(honSplit[i]+"  ");
			if(honSplit[i].charAt(0) == 'p') {
				count++;
			}
		}
		System.out.println("");
		System.out.println("数量："+count);
	}
}
```

###### prac3

```java
public class TestArr2 {
	public static void main(String[] args) {
//		把 lengendary 改成间隔大写小写模式，即 LeNgEnDaRy
		String word = "legendary";
		char[] wordChar = word.toCharArray();
		for (int i = 0; i < wordChar.length; i++) {
			if(i%2 == 0) {
				wordChar[i] = Character.toUpperCase(wordChar[i]);
			}
		}
		String newWord = new String(wordChar);
		System.out.println(newWord);
	}
}
```

###### prac4

把 lengendary 最后一个字母变大写

```java
public class TestArr2 {
	public static void main(String[] args) {
//		把 lengendary 最后一个字母改成大写
		String word = "legendary";
		char[] wordChar = word.toCharArray();
		wordChar[wordChar.length-1] = Character.toUpperCase(wordChar[wordChar.length-1]);
		String newW = new String(wordChar);
		System.out.println(newW);
	}
}
```

###### prac5

Nature has given us that two ears, two eyes, and but one tongue, to the end that we should hear and see more than we speak
把最后一个two单词首字母大写

```java
public class TestArr2 {
	public static void main(String[] args) {
//		Nature has given us that two ears, two eyes, and but one tongue, to the end that we should hear and see more than we speak
//		把最后一个two单词首字母大写
		String word = "Nature has given us that two ears, two eyes, and but one tongue, to the end that we should hear and see more than we speak";
		char[] c1 = word.toCharArray();
		int x = word.lastIndexOf("two");
		c1[x] = Character.toUpperCase(c1[x]);
		String newW = new String(c1);
		System.out.println(newW);
	}
}
```

##### 字符串比较

* 使用new创建的字符串 --- 是在内存中存储
* 直接使用 `String xx = "   ";`这样子的创建的内容是在串池里

直接用`==`比较的话是比较地址值是不是一样，所以这里会false

所以比较字符串内容的时候用`.equals()`；还有`equalsIgnoreCase`

###### 使用串池中的内容创建字符串

`String`类的`intern()`方法用于将字符串对象添加到字符串池，或者返回字符串池中已存在的字符串对象的引用。

```java
String s1 = new String("Hello"); // 创建一个新的字符串对象
String s2 = s1.intern(); // 将s1添加到字符串池，或者返回字符串池中已存在的"Hello"的引用
```

1. **将字符串添加到字符串池中：**当调用`intern()`方法时，它会首先检查字符串池中是否已经存在与当前字符串内容相同的字符串。如果不存在，则将当前字符串对象添加到字符串池中，然后返回字符串池中的引用。这意味着如果多个字符串对象具有相同内容，它们会在字符串池中共享同一个实际字符串对象。
2. **返回字符串池中的引用：**如果字符串池中已存在与当前字符串内容相同的字符串，`intern()`方法将返回字符串池中的引用，而不是创建一个新的字符串对象。这意味着多个字符串对象可以共享相同的字符串内容，从而节省内存。
3. **使用场景：** `intern()`方法通常在以下情况下使用：
   - 当你需要确保字符串对象在内存中只有一个实例时，可以使用`intern()`。
   - 在处理大量字符串对象时，可以使用`intern()`来减少内存使用，尤其是当字符串相同且内容相同时。

###### `startsWith && endsWith`以...开始//以...结束

```java
        String str1 = "the light";
         
        String start = "the";
        String end = "Ight";
         
        System.out.println(str1.startsWith(start));//以...开始
        System.out.println(str1.endsWith(end));
```

###### prac

创建一个长度是100的字符串数组
使用长度是2的随机字符填充该字符串数组
统计这个字符串数组里**重复的字符串有多少种**

```java

```



#### java API

Java的API（ApplicationProgrammingInterface）是指一组用于编程的类、方法、接口和组件，这些允许开发人员在其Java应用程序中进行各种操作和交互。Java的API提供了一种访问和使用Java编程语言核心功能和库的标准方式，包括输入输出、数据结构、网络通信、图形界面用户（GUI）、数据库访问、多线程处理等。

Java的API可以分为以下几个主要部分：

1. **标准Java API**：是Java平台的核心API，提供了用于基本数据类型、集合框架、文件I/O、网络通信、线程处理等的类和接口。包括、 、`java.lang`、`java.util`等`java.io`包`java.net`。
2. **Java标准库**：这是一组标准类库，用于执行各种通用任务，如日期和时间处理、数学计算、字符串处理等。这些类库通常包含在Java标准API中。
3. **Java扩展API**：Java平台还提供了一些可选的扩展API，用于特定领域的开发，如Java EE（企业版）用于企业级应用程序开发、JavaFX用于构建图形用户界面等。
4. **第三方库和框架**：除了标准Java API之外，Java社区还有大量的第三方库和框架，用于各种用途，例如数据库访问（如Hibernate、JPA）、Web图像开发（如Spring框架）、处理（如Java图形库）、文本处理（如Apache Commons Text）等。
5. **自定义API**：开发人员可以根据需要创建自定义API，这些API可以包含在他们自己的Java应用程序中，用于解决特定问题或提供特定功能。

总之，Java的API已经定义了好的接口和类，它们提供了一种与Java编程语言交互的标准方式。通过使用这些API，开发人员可以更容易地构建、扩展和维护Java应用程序，而不必从头开始编写所有的功能和组件。这使得Java成为一种非常强大和灵活的编程语言，适用于各种应用领域。



## 前端部分

### JSON

#### jso是什么

JSON JavaScript 对象表示法（**J**ava**S**cript **O**bject **N**otation） 是一种存储数据的方式。

#### 创建json对象

`var gay = {"name":"chen","age":"18"}`

上述方式就创建了一个json对象 --- 必须由名称和值组合起来（：隔开）

值可以是任意javascript数据类型 字符串 布尔 数字 数组 甚至是对象

### 快捷方式

##### eclipse

1. 输入`syso`后使用`alt+?`可以直接生成 --- `System.out.println();`
2. 快速写main方法 --- 输入main再使用`alt+?`
3. for循环体的快捷输入 --- 输入for+`alt+?`
4. ==快捷修复代码== --- 在出错那行使用`ctrl+1`
5. 知乎整理内容 https://zhuanlan.zhihu.com/p/62665653
6. how2j整理内容  https://how2j.cn/k/helloworld/helloworld-eclipse-tips/300.html

### 使用IDE时的问题

##### eclipse

1. ###### 写了完全没问题的代码确告知没有写main方法

```java
	public static void main(String[] args) {
		System.out.println("Hello World");
	}
}
```

解决方式 Windows -- preferences -- run/debug -- launching

将`save reqiured dirty editors before launching`勾选为always

原因：

- **Dirty Editor** : 指当前在编辑器中打开的文件，但由于您已经对文件进行了更改，因此该文件处于“只读”状态。这意味着文件与磁盘上的原始文件不同。
- **Save**：表示将正在编辑的文件保存到磁盘上的文件中，以便最新的更改生效。
- **Launching**：通常是指启动应用程序、运行代码或调试代码的操作。

该警告的目的是确保您在运行或调试代码之前保存了所有更改，表格因为未保存的更改而导致潜在的问题。如果您选择不保存文件并继续运行代码，您的代码可能会未保存的状态运行，导致不一致或意外的行为。

通常情况下，如果您看到这个警告，最好的做法是点击“保存”或“全部保存”按钮，将正在编辑的文件保存到磁盘上，以确保代码在运行或调试时是最新的版本。有助于减少潜在的错误和问题。

2. ###### eclipse中出现找不到类的情况

* 可能原因1
  * Eclipse是保存后自动编译，但是建立在一个设置的前提上：
    菜单-Project->勾选Build Automatically，如果这里没有勾选，那么是不会自动把Hello.java编译成Hello.class的
  * 查询problems
    * 菜单->Window->Show View->Problems 显示Problems页面
      这里会显示当前项目的错误，倘若有错误，那么项目也不会对.java文件进行自动编译。




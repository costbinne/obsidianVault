# Java金牌

## chp1

### final && static 修饰符

#### final

##### final的三个场景

1. 修饰类的时候 --- 该类不能被继承（没有子类）
2. 修饰方法 --- 该方法不能被重写 override 
3. 修饰变量（成员变量；局部变量）  --- 常量

##### final写法

* 记在access修饰符之后

##### final prac 1

``````java
class foo{
    final int num1=10;
    final int num2		// ---> final修饰的变量可以不在第一时间被赋值，也说明final修饰的意义是[限制只能被赋值一次]
    foo(int i){
        num2 = i;
    }
}
public class main{
    public static void main(String[] args){
        final Foo obj1 = new Foo(100);
        // obj1 = new Foo(200) ---> 会compile error；因为被final修饰只能被赋值一次，改变非基本数据类型的指向也不行，但也说明引用数据类型，不改变指向的前提下可以修改该地址的内容
        Foo obj2 = new Foo(300);
        syso(num1);  // ---> 输出10
        syso(num2);  // ---> 输出300
    }
}
``````

 **关于上述代码中`num2`一些问题**

1. 为什么final修饰的成员变量（未被赋值），可以通过创建多个该对象进行多次赋值

   1. 要理解这个问题需要理解成员变量和实例之间的关系

      在Java中，创建一个类的实例时，类的成员变量（也称为实例变量或字段）会在内存中的状态如下：

      1. 内存分配：使用`new`关键字创建一个类的实例时，Java虚拟机（JVM）会在==堆内存==中为该实例分配一块内存空间。这块==内存空间用于存储该实例的成员变量==。
      2. 默认初始化：==在Java中，成员变量会根据其数据类型进行默认初始化。==例如，数值类型的成员变量会被初始化为0，布尔类型的成员变量会被初始化为，引用类型的成员变量会被`false`初始化为`null`。
      3. 构造函数：如果类有构造函数，==构造函数将在分配内存后执行。==构造函数可以用于对成员变量进行初始化，也可以执行其他必要的操作。您可以通过构造函数的参数来传入初始值。

说明本质上，num2在每一次被实例化生成的时候产生的num2，应该是["实例名".num2],所以obj1和obj2对各自的num2赋值一次并不违背final

#### static修饰符

##### 使用场景

1. 修饰变量 ---> 静态变量
2. 修饰方法 ----> 也被称为类方法

##### 关于静态和内存

* 当类加载进栈的时候，该类的静态就进入内存

* 静态存在于类的运行时数据区域，而不是对象的实例数据区域。

* 加载之后，类及其静态变量成员和静态方法都会一直存在于内存中，直到程序退出。

* 使用instance调用static时，即使instance为null也可以调用该static不触发`NullPointerException`

  * 原因如下：

    * 声明一个对象引用时，即使没有实例化对象，这个声明仍然表示了该引用和类之间的关系。这是因为这个声明告诉编译器打算使用该引用来访问该引用类的成员（包括静态成员）。这种声明允许在后续的代码中使用该引用来访问类的成员，包括静态变量和静态方法。

      虽然对象引用在没有实例化对象的情况下不会引用任何具体的实例，但它告诉编译器与特定的类进行交互，而不是与任何具体的对象实例进行交互。因此，可以使用这个引用来访问该类的静态成员，因为静态成员属于类本身，而不是特定的对象实例。

  * 补充内容

    * 单纯的声明行为并不会在内存中开辟空间 --- 实际的内存分配发生在`new`关键字实例化之后。只是声明的话他就是个未初始化的引用，它的值是`null`

    * 如果直接给声明对象赋值null，实际上并没有在内存中分配空间来存储对象。在这种情况下，该声明就是一个对象引用，但它的值`null`，表示它当前不引用任何对象。

      `null`是一个特殊的值，表示引用变量不引用任何对象。Java的垃圾收集器会负责回收不再被引用的对象，但对象引用本身只是一个指向对象的指针，不会占用额外的内存空间。因此，声明将其分配为`null`不会在内存中分配额外的空间。

### ENUM

#### enum写法

* 修饰子    enum   名称{ 值1，值2，值3，..... }

#### enum相关内容

##### enum定义位置

* 单独写一个类似于class的enum

``````java
package com.example;
public enum MyEnum {
    VALUE1,
    VALUE2,
    VALUE3
}
``````

* 将enum定义为内部类
* 不能将enum定义在方法中

##### enum例子

``````java
//文件名Card.java
public enum Card{
    spades,clubs,diamonds,hearts
}
``````

上述的Card.java在被编译之后 --- 生成Card.class --- 具体如下

``````java
final class Card extends java.lang.Enum<Card>{
    public static final Card spades;
    public static final Card clubs;
    public static final Card diamonds;
    public static final Card hearts;
    //part2
    public static Card[] values(){ .... }
    public static Card valueOf(java.lang.String){ .... }
    static{ .... }
}
``````

可以知道enum被编译之后是final修饰的 --- > 说明Card,java是不能被继承的

* enum本质是为了表示一组固定的常量
* 在创建enum时，其值并没有看作字符串加双引号，因为class文件可以看出这个值实际是当作变量名来看的
* part2部分的内容属于是继承了Enum后追加的
  * value（） --- 用数组形式返回内容
  * valueOf（） --- 指定index
* 由上可以知道列举型就是常量和方法构成的class，但是不能实例化 --- 指的是new的形式去实例化
  * 内部赋值的内容都被实例化了
* 调用例子：[Card.spades]

##### enum中主要的方法




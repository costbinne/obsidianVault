# Linux操作系统学习

## linux为什么重要

* 操作系统分三类：

  1. 个人桌面操作系统：windows ； macOS

  2. 服务器操作系统： Linux

  3. 手机操作系统：安卓；IOS

     **LINUX的应用场景（大分类）：**后端开发；大数据开发；运维开发；测试开发；前端开发

     **原因：**因为后端软件；大数据系统；运维监控；测试程序；网页服务。等都需要最终运行在linux操作系统之上

## 操作系统相关知识

### 操作系统的作用

* 主要是协助用户调度硬件工作，充当用户和计算机之间的桥梁

## Linux系统的组成：

1. Linux系统内核
2. 系统级应用程序

**内核的作用：**提供系统最核心的功能，eg：调度cpu；调度内存；调度文件系统；调度网络通讯；调度IO等。

**系统级应用程序：**可以理解为出厂自带程序，如：文件管理器；任务管理器；图片查看；音乐播放。（无论用户使用自带音乐播放器或是第三方---均是由播放器程序，调用内核提供的相关功能）

![image-20230603162032469](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603162032469.png)

![image-20230603162145277](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603162145277.png)

![image-20230603162237428](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603162237428.png)

* 由于发行版很多----国内CentOS用的多；国外ubuntu用的多---基础指令是都相同的---所以学习的话不必太纠结发行版的选择

## 虚拟机相关

### 虚拟机是什么

通过虚拟化技术，在电脑内虚拟出计算机硬件，并给虚拟的硬件安装操作系统，得到一台虚拟的电脑---虚拟机

### 虚拟化软件

* VMware---有免费版，也有试用版
* 注意事项：
  * 安装后需要查看网络设置是否存在VMware Network ~1&8；
    * 打开方式win+r；---输入ncpa.cpl

### 虚拟机快照

![image-20230603224215797](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603224215797.png)

免费的player版本的话没有快照功能

## Linux学习

### 图形化//命令行

* 对于操作系统的使用，有两种形式：
  1. 图形化页面
  2. 命令行形式

* **为什么要学习Linux的命令行**原因是Linux诞生至今并未在优化图形化页面上发力---导致图形化页面不好用不稳定；；第二点在开发中使用命令行，效率更高，更加直观，且占用资源更低，程序运行更稳定

### 为什么要使用FinalShell

![image-20230603213623225](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603213623225.png)

* 当发现==连接好的FinalShell链接不上==的时候---可能是ip地址发生了变化（linux的）---在Linux系统中用ifconfig命令确定ip----再在FinalShell中设置修改就可以了

### WSL

![image-20230603215321410](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603215321410.png)

* WSL全称==**Windows Subsystem for Linux**==，是用于windows系统之上的Linux子系统---作用是可以在windows系统中获得Linux系统环境，并直接直连计算机硬件，无需虚拟机虚拟硬件。

### Linux目录结构

![image-20230603224615862](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603224615862.png)

* windows中的顶级目录可以有多个//Linux只有一个

![image-20230603224834732](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603224834732.png)

* 例如Linux的路径例子： /usr/local/hello.txt
  * 注意最开始的“/”表示根目录

### Linux命令

#### Linux命令是什么

![image-20230603225313486](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603225313486.png)

#### Linux命令的基础格式

![image-20230603225646072](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603225646072.png)

示例2：

```java
cp -r test1 test2
```

cp是命令本身，-r是选项----意思是复制test1文件夹成为test2文件夹

#### ls命令

![image-20230603230034820](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603230034820.png)

##### home目录和当前工作目录

![image-20230603230349452](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603230349452.png)

* 注意：==HOME目录是指`/home/costbinne`这个路径并不是Root下的home文件夹==

##### **ls命令的参数和选项**

* ==**-a选项**==---all的意思，列出包括隐藏文件夹在内的全部文件

![image-20230603231103968](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603231103968.png)

前面带有点的文件就是隐藏文件---需要使用ls -a才能看到

* ==**-l 选项**==，表示以列表的形式（竖向排列）展示内容，并展示更多信息

![image-20230603231258066](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603231258066.png)

从左到右展示的是：

权限 || 用户和用户组 || 大小 || 创建时间

* ==语法中的选项可以混合使用==
  * 例如 -al或者-la或者`ls -a -l`

* 除了选项本身可以组合外，选项和参数也可以一起使用。例如： `ls -al /`

上述表示对根目录执行这个ls命令

* ==**-h选项**==这个选项需要和`-l`一起使用，单独使用没有意义
* 因为单独使用`-l`的时候虽然会列出文件大小---但没有单位---加上`-h`的话可以带上单位

![image-20230603232323788](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230603232323788.png)

* ==**参数的作用**==，就是指定除了默认工作目录以外的路径

#### -cd   -pwd 命令

##### -cd切换工作目录

* linux默认以home（用户各自的）作为当前工作目录---可以通过`-cd`来改变当前工作目录
* cd命令来自英文: Change Diretory
* 语法： cd [Linux 路径]
  * cd命令无需选项；只有参数；表示切换到哪里
  * cd直接执行不写参数，表示回到用户的home目录下

![image-20230604102018753](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604102018753.png)

##### `-pwd`查看当前工作目录

* 刚才通过`ls`来验证当前工作目录，其实是不恰当的；合理的方法是通过`pwd`命令，来查看当前所在的工作目录。
* `pwd`命令来自于: Print Work Directory
* 语法 `pwd`
* `pwd`命令，无选项，无参数，直接输入就可

![image-20230604102516566](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604102516566.png)

#### 上述命令的练习

* 使用cd 结合 ls ，尝试找出games文件夹在哪里

`/var/lib/games`

#### 相对路径 绝对路径 特殊路径表示符

![image-20230604103240617](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604103240617.png)

![image-20230604103348600](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604103348600.png)

##### 特殊路径符

![image-20230604103603197](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604103603197.png)

#### mkdir 命令

* 作用：mkdir可以创建新目录（文件夹）
* mkdir来自英文：Make directory
* 语法： `mkdir [-p] Linux路径`
  * 参数必须写，表示Linux路径（就是要创建的文件夹的路径），可以相对或者绝对路径
  * `-p`选项可选，表示自动创建不存在的父目录，适用于创建连续多层级的目录

![image-20230604105500544](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604105500544.png)

![image-20230604105705510](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604105705510.png)

##### 关于`-p`选项

![image-20230604105819060](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604105819060.png)

![image-20230604105936113](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604105936113.png)

* ==**注意：**==创建文件夹需要修改权限，请确保操作均在HOME目录内，不要在HOME外操作---后续会讲解权限管控

![image-20230604110404334](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604110404334.png)



#### 清空console/terminal快捷键

* `ctrl+l`

#### 文件操作命令相关

##### touch cat more

###### touch命令

* 可以通过touch命令创建文件
* 语法：`touch Linux路径`
  * `touch`命令无选项，参数必填，表示要创建的文件路径，相对绝对/特殊路径符均可

![image-20230604110936695](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604110936695.png)

###### `cat`命令

* 有了文件后，可以用cat命令查看文件的内容
* 由于未学习vi编辑器---无法向文件内编辑内容---所以要先用图形化页面添加内容----再用cat去确认。
* 语法： `cat Linux路径`
  * 没有选项 ； 只有必填参数---表示被查看文件的路径 （相对绝对特殊均可）

![image-20230604111711036](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604111711036.png)

###### 组合练习

![image-20230606085645111](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606085645111.png)

由上可知---cat命令可以打开多个文件

###### `more`命令

* `more`同样用于查看文件内容
  * 与`cat`存在不同：
    1. cat是将内容全部显示出来
    2. more支持翻页，如果文件内容过多，可以一页一页展示
* 语法：`more Linux路径`
  * 没有选项 ； 只有必填参数

![image-20230604112101273](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604112101273.png)

* 查看页数较多的文件---进一步理解more的作用
  * 路径`/etc/services`
    * 查看过程中，通过`space`翻页
    * 通过`q`退出

##### `cp`命令

* cp命令可用于复制文件/文件夹
* 语法： `cp [-r] 参数1 参数2`
  * `-r`选项，可选，用于复制文件夹使用，表示递归
  * 参数1，Linux路径，表示被复制对象
  * 参数2，Linux路径，表示要复制去的地址

![image-20230604112804960](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604112804960.png)

![image-20230604112949152](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604112949152.png)

* 关于复制文件夹

![image-20230604113106179](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604113106179.png)

所以复制文件夹的时候需要加上	`-r`



##### `mv`命令

* mv命令可以用于移动文件/文件夹
* 语法`mv 参数1 参数2`
  * 参数1，Linux路径，被移动者
  * 参数2，Linux路径，移动目的地---如果目标不存在啊，则进行改名，确保目标存在

![image-20230604113421872](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604113421872.png)

* 关于文件夹移动

![image-20230604113752213](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604113752213.png)

注意点：路径最后可以跟斜杠`/`也可以不用



##### `rm`命令

* `rm`命令可用于删除文件/文件夹
* 语法：`rm [-r -f] 参数1 参数2 ... 参数N`
  * `-r`选项用于删除文件夹
  * `-f`表示force，强制删除（不会弹出提示确认信息）
    * 普通用户删除内容不会弹出提示，只有root管理员删除内容会有提示
    * 所以一般用户用不到`-f`选项
  * 参数n---表示被删除对象

![image-20230604114540516](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604114540516.png)

###### `rm`命令与通配符

rm命令支持通配符`*`，用来做模糊匹配

例子：

	1. test*---表示匹配任何用test开头的内容
	1. *test --- 匹配~结尾
	1. `*test*`---匹配包含~

![image-20230604115040301](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604115040301.png)

###### rm命令的[-f]选项

* 可以通过 `su - root`,并输入密码，临时切换到root用户体验
* 通过exit命令，退回普通用户（用完一定要退出）

![image-20230604115653142](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604115653142.png)

* 提示的时候输入对应的y或者n

![image-20230604115900409](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604115900409.png)

##### which命令

* Linux命令本体就是一个个的二进制可执行程序---和windows中的`.exe`是一个意思
* 可以通过which命令，查看所使用的一系列命令的程序文件放在哪里
* 语法：which 要查找的命令

![image-20230604211157990](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604211157990.png)



##### find命令

* 在Linux系统中，可以通过find命令去搜索指定的文件

* 语法：`find 起始路径 -name "被查找文件名"`

* 为了确保搜索中有最大权限，可以在整个系统总完成搜索

  需要切换到Root用户（`su - root`）

![image-20230604211835668](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604211835668.png)

提示了一系列的权限不够

获得临时权限后

![image-20230604211953512](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604211953512.png)

搜索文件名

![image-20230604215942855](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604215942855.png)

通配符搜索

![image-20230604220033166](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604220033166.png)

###### find命令按文件大小搜索

* 语法：`find 起始路径 -size +|-n[KMG]`

  * +,-  表示大于或者小于
  * n --- 表示大小数字
  * kMG --- 表示大小单位，k（小写字母）表示kb，M表示MB，G表示GB

* eg：

  * 查找小于10kb的文件：

    `find / -size -10k`

  * 查找大于100MB的文件

    `find / -size +100M`

  * 查找大于1GB的文件

    `find / -size +1G`

* ==注意想要中断输出的话快捷键是`ctrl+c`==

* 可以用`ls -lh`去查看文件的大小来验证

![image-20230604221237304](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230604221237304.png)

##### grep命令

* 通过这个命令，从文件中通过关键字过滤文件行
* 语法： `grep [-n] 关键字 文件路径`
  * 选项 -n ，可选，表示在结果中显示匹配的行的行号
  * 参数 关键字 ==必须填写==表示过滤的关键字，带有空格或其它特殊符号，建议使用“”将关键字包围
  * 参数 文件路径 ==必须填写==表示要过滤内容的文件路径，可作为内容输入端口

![image-20230606090044084](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606090044084.png)



##### wc命令

* 可以通过wc命令统计文件的行数，单词数量等

* 语法：`wc [-c -m -l -w] 文件路径`
  * 选项 -c --- 统计bytes数量
  * 选项 -m --- 统计字符数量
  * 选项 -l --- 统计行数
  * 选项 -w --- 统计单词数量
  * 参数 文件路径 被统计文件---可作为内容输入端口

![image-20230606092742844](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606092742844.png)

可以组合使用，但是注意顺序是由差别的---`lwmc`

如果wc命令什么都不加的话---就显示行数 单词数 字节数

![image-20230606093200235](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606093200235.png)

顺序验证如上图---一个汉字两个字节||==注意汉字被算作一个单词==



##### 管道符

* 管道符是一个符号： `|`
* 含义是：将管道左边的命令结果，作为右边命令的输入

![image-20230606093602005](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606093602005.png)

在grep命令中就不需要加入被查验文件的路径参数了

![image-20230606093953179](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606093953179.png)

也可以和`ls`命令组合---查找文件夹之类的

![image-20230606094122583](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606094122583.png)

这样子可以统计出文件夹中有多少文件

![image-20230606094234860](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606094234860.png)

管道符嵌套使用

![image-20230606094419422](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606094419422.png)

问题1：

统计hello.txt中的c关键字有几行

![image-20230606094602051](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606094602051.png)

问题2：

统计带有coffee的关键字结果中有多少个单词

![image-20230606094755649](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606094755649.png)



##### echo命令

* 可以使用echo命令在命令行内输出指定内容
* 语法 `echo 输出内容`
  * 无需选项 只有一个参数 表示要输出的内容---复杂的话可用“ ”包围
    * 不包围的话很可能被识别为第二个参数（不影响结果）

![image-20230606095231849](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606095231849.png)



##### 反引号

* 如果想`echo pwd`---输出当前工作路径 而不是将pwd作为普通字符输出的话---可以用反引号包裹pwd

![image-20230606095552598](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606095552598.png)

里面就会被当作命令执行



##### 重定向符号

* `> 和 >>`
* `>`  表示将左侧命令的结果，覆盖写入到符号右侧指定的文件中
* `>>`  表示将左侧命令的结果，追加写入到符号右侧的指定文件中

![image-20230606100034679](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606100034679.png)



##### tail命令

* 可以查看文件尾部内容，跟踪文件最新更改 
* 语法： `tail [-f -num] Linux路径 `
  * 参数，Linux路径 表示被跟踪的文件路径
  * 选项，-f，表示持续跟踪
  * 选项，-num，表示查看尾部多少行，不填默认10行

##### 练习

![image-20230606102344056](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606102344056.png)

![image-20230606102658951](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606102658951.png)

![image-20230606103111124](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606103111124.png)

* 注意之前的内容中pwd被输出为字符是因为未使用反引号

![image-20230606102712511](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606102712511.png)



##### vi/vim编辑器介绍

vi/vim是visual interface的简称，是Linux中最经典的文本编辑器

vim 是vi的加强版本---兼容其指令 ； 不仅能编辑文本还可以shell程序编程（且可以进行颜色区分来辨别语法的正确性）



##### vi/vim编辑器的三种工作模式

1. 命令模式（command mode）

   ​	此模式下，所敲的按键编辑器都理解为命令，以命令驱动执行不同的功能，此模式下，不能自由进行文本编辑。

2. 输入模式（insert mode）

​			也就是编辑模式，可自由编辑文本内容

3. 底线命令模式（last line mode）

   ​	以`:`开始，通常用于文件的保存，退出

![image-20230606103950150](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606103950150.png)

![image-20230606104123630](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606104123630.png)

进入的时候都是进入命令模式

中间模式切换都是靠命令模式作为bridge

##### 命令模式下的操作

1. 按`i`进入编辑模式
2. 按esc退回命令~
3. 按`yy 然后 p`复制一行
4. 按`dd`删除一行
5. 按`u`撤销
6. 按`:`进入底线命令模式
7. 可以通过键盘的方向键控制光标位置
8. ![image-20230606105126357](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606105126357.png)
9. ![image-20230606105242104](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606105242104.png)

10. $用shift+4
11. shift+n搜索模式下向上搜索上一个
12. ctrl+r 反向撤销
13. d0当前光标位置删除到行头；d$删到行尾

##### 底线命令模式中的操作

1. wq---w是保存；q是退出

![image-20230606105754510](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606105754510.png)



##### 切换账户//su命令

![image-20230606110250293](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606110250293.png)

* root用户切换普通用户使用su命令的话，不需要使用密码

##### sudo命令

![image-20230606110541040](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606110541040.png)

认证配置方法

![image-20230606110704365](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606110704365.png)



##### 用户和用户组

![image-20230606155639139](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606155639139.png)

##### 用户组管理命令

* 需要Root用户执行---权限

* 创建用户组

  语法：`groupadd 用户组名`

* 删除用户组

  语法：`groupdel 用户组名`

![image-20230606160125446](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606160125446.png)

##### 用户管理相关命令

* 创建用户

  语法： `useradd [-g -d] 用户名`

  		1. 选项 -g ---指定用户的组，不指定 -g ，会创建同名组并自动加入，指定 -g 需要组已经存在 ，如已经存在同名组则必须指定 -g 。
  		1. 选项 -d ---指定用户HOME路径，不指定---HOME目录默认在：/home/用户名

* 删除用户

  语法：`userdel [-r] 用户名`

  	1. 选项 -r ---删除用户的HOME目录，不使用 -r --- 删除用户时，其HOME目录保留

* 查看用户所属组

  语法：`id [用户名]`

  	1. 参数：用户名 ---被查看的用户，如果不提供则查看自身

* 修改用户所属组

  语法：`usermod -aG 用户组 用户名`

  ​	将指定用户加入指定组

![image-20230606161142077](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606161142077.png)

* useradd中 -g 选项后面直接写组名
* 存在同名组不用 -g 对象的话---该用户不会创建
* 查看用户所属组---不需要root权限

![image-20230606161458148](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606161458148.png)

* 一个用户可以有多个组
* 权限最大时---也不能直接删除别人的主组

**![image-20230606161737056](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606161737056.png)**

* 没办法随意 cd 进入别人的HOME文件夹

![image-20230606162038894](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606162038894.png)

* 但是可以修改和查看文件夹

![image-20230606162156642](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606162156642.png)

* 删除用户及其HOME

![image-20230606162622649](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606162622649.png)

* 指定选项不需要顺序

![image-20230606163027843](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606163027843.png)

* 可以切换到别人的账户上---通过root用户不需要密码

![image-20230606163411228](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606163411228.png)

* 切换后一定记得 exit 



##### getent 命令

* 这个命令可以帮忙查看当前系统中有哪些用户

  语法： `getent passwd`

  除了自己创建的以外---还有很多系统自身构建的用户

![image-20230606163818029](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606163818029.png)

![image-20230606163845770](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606163845770.png)

* 使用`getent group `可以查看当前系统中有哪些组

  包含三分信息：

  	1. 组名称；2. 组认证（显示为x）；3. 组id

  ![image-20230606164121473](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606164121473.png)



##### 权限相关

![image-20230606164408650](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606164408650.png)

![image-20230606164658615](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606164658615.png)

* 首位中： d 表示文件夹 - 表示文件 l 表示软链接

![image-20230606164824159](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606164824159.png)

##### chmod命令

![image-20230606165415953](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606165415953.png)

**权限的快捷表示**

![image-20230606165850705](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606165850705.png)

**练习**

![image-20230606170038867](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606170038867.png)

515-----`chmod 515 hello.txt`

![image-20230606170135309](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606170135309.png)

`chmod 326 hello.txt`

![image-20230606170213488](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606170213488.png)

user 只有 x （cd进入权限）；group 有 w （write权限--即修改）；other有 wx 进入和修改

`--x-w--wx`



##### chown命令

![image-20230606170558475](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230606170558475.png)



#### 快捷键

##### ctrl+c 强制停止

![image-20230608094830290](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608094830290.png)

命令输入错误了，不想一个一个删除，就可以ctrl+c直接取消输入



##### ctrl+d 退出或登出

* 可以通过快捷键`ctrl+d`退出当前的账户----例如`su - root`之后可以用exit或者ctrl+d
* 或者用于推出某些特定程序的专属页面
  * 例如 linux中的python---就可以用ctrl+d（在系统中直接输入python---就会进入python这门语言的解释器环境中---==python是linux自带的==）



##### 历史命令搜索

1. 可以通过输入history命令----查看到历史使用过的命令
2. 通过grep 搜索关键字可以查找特定命令
3. 作用是---可以找一些很长的命令复制粘贴

* 另一种模式
  * 输入感叹号作为命令前缀---（以python为例，我曾经执行过python---我就可以用`!p`命令使得系统按着history去从下往上匹配---找到合适的---再次执行该命令

![image-20230608095849257](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608095849257.png)

![image-20230608095909232](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608095909232.png)

同理：想要执行history---！h

但是不能匹配很久之前的

* 另一种模式
  * 可以通过快捷键`ctrl+r`输入命令去匹配历史命令
  * 如果搜索到的内容是需要的可以回车执行//键盘左右键可以得到此命令不执行

![image-20230608100208323](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608100208323.png)

![image-20230608100330297](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608100330297.png)



##### 快捷移动光标

* ctrl+a ---- 跳到命令开头
* ctrl+e ---- 跳到命令结尾
* ctrl+键盘左键 ---- 向左跳一个单词
* ctrl+键盘右键 ---- ~



##### 清屏

* 可以用ctrl+l
* 也可以用clear命令



##### 一些tips

1. 按ctrl + c 可以停止一些持续执行的命令---例如 tail -f ； 
2. 按方向键上建---可以执行相同上次的命令内容跟



#### 安装软件

##### Linux的系统应用商店

![image-20230608101008472](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608101008472.png)

##### yum命令

![image-20230608101105685](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608101105685.png)

* RPM就是Linux系统的安装包格式

**Ubuntu中的软件安装**

![image-20230608101722180](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608101722180.png)

* ubuntu中软件安装包是deb格式的后缀---对应的软件安装程序是apt
* wsl系统中都默认配置了sudo权限
* 要输入自己配置的密码



##### systemctl命令

![image-20230608102308685](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608102308685.png)

* 查看防火墙运行状态

![image-20230608102510904](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608102510904.png)

![image-20230608102714812](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608102714812.png)

* 停止防火墙需要root权限---所以建议切换root用户再操作

![image-20230608103010198](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608103010198.png)

* 关闭开启防火墙
* 除了内置的这些功能----还可以控制外置的一些程序的状态

![image-20230608103212796](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608103212796.png)

* ntp --- 时间同步软件---安装后会把自己注册为系统的服务
  * 注：systemctl能控制得第三方软件需要和服务相关（指的是软件安装的时候会自动集成到Systemctl中）---也可以手动添加



#### 软连接

![image-20230608103925986](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608103925986.png)

![image-20230608104547174](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608104547174.png)

可以制定不同名的文件软连接----会帮你创建该名字

且在ls -lh的展示下---第一位不是d（文件夹）-（文件）；而是l----这个l表示的是软连接

![image-20230608111543106](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608111543106.png)

![image-20230608112057412](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608112057412.png)

在root模式下可以制作正常的软连接



#### 时间和时区

##### date命令

![image-20230608112403765](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608112403765.png)

* 使用data命令本体，无选项，直接查看时间

![image-20230608194014601](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608194014601.png)

* 可以用格式化字符串自定义显示格式

![image-20230608194145351](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608194145351.png)

![image-20230608194601383](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608194601383.png)

* 一定要加上双引号---不然系统会报错（额外的操作数）---因为中间出现了空格

* ==自定义格式的时候一定要加号==
* 选项如何计算时间

![image-20230608195131886](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608195131886.png)

* 其中-d选项支持的时间标记如下：
  * year；month；day；hour；minute；second

![image-20230608195831129](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608195831129.png)

* 如何修改时区

  * 要使用root权限---执行下列命令

  `rm -f /etc/localtime`

  `sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`

![image-20230608200625802](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608200625802.png)

* 时间如何校准

![image-20230608200711226](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230608200711226.png)



#### IP地址

![image-20230609105448609](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609105448609.png)

* 一般centos系统的网卡都会叫做`ens33`其中的inet就是ip地址
* lo表示本地回环的网卡///virbr0是虚拟机虚拟的网卡（都可以在ifconfig中查询到）

![image-20230609105908684](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609105908684.png)

* `lo`中的`inet:127.0.0.1`这个ip地址用于指代本机
* `0.0.0.0`，特殊的ip地址
  * 可以用于指代本机
  * 可以在端口绑定中用来确定绑定关系
  * 在一些ip地址限制中，表示所有IP的意思，如放行规则设置为`0.0.0.0`，表示允许任意ip访问

#### 主机名

![image-20230609113614114](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609113614114.png)

![image-20230609113632894](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609113632894.png)

##### 在Linux中修改主机名

* 使用hostname可以查看主机名
* 可以在root权限下---使用`hostnamectl set-hostname 主机名`，来对主机名进行修改---修改后重新登陆FinalShell就可以查看到自己的新主机名

![image-20230609114026702](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609114026702.png)



#### 域名解析

* 由于ip地址难以记忆 --- 所以实际上一般都是通过字符化的地址去访问服务器，很少指定ip地址
  * 例如用`www.baidu.com`去打开百度网址 --- 这样的被称为域名
* 将ip地址映射到网址上就可以

实现流程

![image-20230609154800451](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609154800451.png)

1. 先看私人地址（Linux的话查看`/etc/hosts`）
   1. windows的话`c:\Windows\System32\drivers\etc\hosts`文件
2. 在看公开DNS服务器去查询

##### 配置主机名映射

* Windows的finalshell是通过ip地址连接到Linux服务器的，要实现用过域名（主机名）连接的话就需要配置主机名映射

* 由于是在windows系统中所以需要配置到前述文件位置中

配置流程

1. 以管理员身份运行记事本程序
2. 在记事本打开文件查找到对应的hosts文件
3. 在其中写入 （ip地址---linux的）+“ ”+（主机名）



#### 虚拟机配置固定ip

![image-20230609160021223](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609160021223.png)

在VMware Workstation中配置固定ip：

![image-20230609160125417](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609160125417.png)

![image-20230609161517034](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609161517034.png)

由于我是VMplayer版本所以不能设置 --- 暂时跳过

参考资料：VM plyaer虚拟机固定ip（https://blog.csdn.net/yanzhaoxun/article/details/114367745）

日文资料（https://www.nslabs.jp/linux-nat-on-vmware.rhtml）

（https://www.bigbang.mydns.jp/vmwareplayer-kotei-x.htm）



#### 网络传输

##### ping命令

![image-20230609162036607](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609162036607.png)

![image-20230609163602939](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609163602939.png)

连接不到的话会显示unreachable



##### wget命令

![image-20230609163654229](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609163654229.png)

注意下载一旦开始---就算被中断了---该文件还是会产生



##### curl命令

![image-20230609163958447](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609163958447.png)

![image-20230609164133837](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609164133837.png)

向网站发起请求的话 --- 可以在命令行得到网站的源码



#### 端口（网络传输）

![image-20230609164404458](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609164404458.png)

![image-20230609164450320](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609164450320.png)

![image-20230609164513421](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609164513421.png)

![image-20230609164706071](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609164706071.png)

##### nmap命令

![image-20230609164732020](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609164732020.png)

![image-20230609164938435](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609164938435.png)

`127.0.0.1`可以代表本机

本机上有五个端口被占用了

ssh占用22端口 --- finalshell就通过这个链接到Linux中



##### nestat命令

![image-20230609165132949](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609165132949.png)

![image-20230609165401230](C:\Users\chin itsufu\AppData\Roaming\Typora\typora-user-images\image-20230609165401230.png)

* 4个0有时候也可以表示本机

除了可以直接查端口的情况 --- 也可以grep跟上进程数字 --- 查看进程的状态

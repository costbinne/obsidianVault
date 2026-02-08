## 前端代码与浏览器
前端代码 由 浏览器解析渲染之后 呈现给用户
浏览器进行解析渲染的部分 就是浏览器的内核
由于浏览器内核的不同,对于相同前端代码解析的效果可能会存在差异

为了使网页在不同浏览器的内核下 呈现相同的效果,有开发的标准如下
![[Pasted image 20260208171915.png]]

## 前端代码 基础知识
https://developer.mozilla.org/zh-CN/
推荐查询网站如上

## 练习代码HTML
注意点 
	1. 标签不区分大小写
	2. 属性值可以单引号 和 双引号
	3. 语法结构松散 一部分结束标签不写也不会出错
```
<html>

    <head>

        <title>

            HTML快速练习

        </title>

    </head>

    <body>

        <h1>

            Hello HTML

        </h1>

        <img src="C:\Users\chin itsufu\Pictures\pic1.jpg">

    </body>

</html>
```
实际代码
```
<!DOCTYPE html>

<!-- 声明文档的类型为HTML -->

<html lang="en">

<head>

    <meta charset="UTF-8">

    <!-- 字符集的设置 -->

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- 设置在移动端的显示宽度以及缩放比例 -->

    <title>Document</title>

</head>

<body>

    <h1>HTML练习</h1>

    <!-- 给我一个H1，标题内容为HTML青年大学习 -->

    <h1>HTML青年大学习</h1>

        <!-- 给我一个超链接能够链接到google首页，内容为google 且实在新窗口中打开 -->

     <a href="https://www.google.com" target="_blank">google</a>
</body>

</html>
```
![[Pasted image 20260208200730.png]]

## CSS代码
![[Pasted image 20260208191543.png]]
```
<!DOCTYPE html>

<!-- 声明文档的类型为HTML -->

<html lang="en">

<head>

    <meta charset="UTF-8">

    <!-- 字符集的设置 -->

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- 设置在移动端的显示宽度以及缩放比例 -->

    <title>Document</title>

    <!-- 引入CSS样式的方式2 -->

     <style>

        p{

            color: blue;

        }

     </style>

  

     <!-- 引入CSS样式的方式3 -->

     <link rel="stylesheet" href="CSS/practice02.css">

</head>

<body>

    <h1>HTML练习</h1>

    <!-- 给我一个H1，标题内容为HTML青年大学习 -->

    <h1>HTML青年大学习</h1>

        <!-- 给我一个超链接能够链接到google首页，内容为google 且实在新窗口中打开 -->

     <a href="https://www.google.com" target="_blank">google</a>

    <!-- 引入CSS样式的方式1 -->

     <span style="color: red;">引入CSS样式的方式1 行内指定</span>

  

    <!-- 引入CSS样式的方式2 -->

     <p>引入CSS样式的方式2 内部指定</p>

    <h2>引入CSS样式的方式3 外部指定</h2>

</body>

</html>
```
CSS代码
```
        h2{

            color: green;

        }
```
![[Pasted image 20260208192739.png]]
### CSS中的颜色表示方式
![[Pasted image 20260208193017.png]]
![[Pasted image 20260208193503.png]]
### CSS中的选择器
![[Pasted image 20260208195244.png]]
```
<!DOCTYPE html>

<!-- 声明文档的类型为HTML -->

<html lang="en">

<head>

    <meta charset="UTF-8">

    <!-- 字符集的设置 -->

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- 设置在移动端的显示宽度以及缩放比例 -->

    <title>Document</title>

    <!-- 引入CSS样式的方式2 -->

     <style>

        p{

            color: blue;

        }

        .cls{

            color: #b2b2b2;

        }

        /* id选择器不能以数字作为开头 */

        #a001{

            color: rgb(253, 12, 180);

        }

        a{

            /* 去除超链接的下划线 */

            text-decoration: none;

            color: rgb(180,45, 255);

        }

     </style>

  

     <!-- 引入CSS样式的方式3 -->

     <link rel="stylesheet" href="CSS/practice02.css">

</head>

<body>

    <h1>HTML练习</h1>

    <!-- 给我一个H1，标题内容为HTML青年大学习 -->

    <h1>HTML青年大学习</h1>

        <!-- 给我一个超链接能够链接到google首页，内容为google 且实在新窗口中打开 -->

     <a href="https://www.google.com" target="_blank">google</a>

    <!-- 引入CSS样式的方式1 -->

     <span style="color: red;">引入CSS样式的方式1 行内指定</span>

    <!-- 引入CSS样式的方式2 -->

     <p>引入CSS样式的方式2 内部指定</p>

    <h2>引入CSS样式的方式3 外部指定</h2>

    <!-- 这个内部指定CSS的话 是优先于外部指定生效的 -->

    <h2 class="cls">CSS类选择器 测试</h2>

    <h2 class="cls" id="a001">CSS ID选择器 测试</h2>

</body>

</html>
```
![[Pasted image 20260208195327.png]]


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

### CSS中的盒子模型
可以将下面代码用浏览器读取查看
```
<!DOCTYPE html>

<html lang="zh-CN">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>盒子模型演示</title>

    <style>

        body {

            font-family: Arial, sans-serif;

            margin: 20px;

            background-color: #f5f5f5;

        }

        .container {

            display: flex;

            gap: 20px;

            justify-content: center;

            flex-wrap: wrap;

        }

        .box {

            width: 200px;

            height: 150px;

            background-color: lightblue;

            border: 5px solid #333;

            margin: 20px;

            padding: 15px;

        }

        .box1 {

            background-color: #ffcccc;

            border: 8px solid #e74c3c;

            padding: 10px;

            margin: 15px;

        }

        .box2 {

            background-color: #ccffcc;

            border: 6px solid #27ae60;

            padding: 20px;

            margin: 10px;

        }

        .box3 {

            background-color: #ccccff;

            border: 10px solid #3498db;

            padding: 5px;

            margin: 25px;

        }

        .detailed-box {

            width: 150px;

            height: 100px;

            background-color: #fff3cd;

            border: 4px solid #856404;

            padding: 12px;

            margin: 30px;

            position: relative;

        }

        .explanation {

            max-width: 800px;

            margin: 30px auto;

            padding: 20px;

            background-color: white;

            border-radius: 8px;

            box-shadow: 0 2px 10px rgba(0,0,0,0.1);

        }

    </style>

</head>

<body>

    <h1 style="text-align: center;">CSS 盒子模型演示</h1>

    <div class="explanation">

        <h2>什么是盒子模型？</h2>

        <p>CSS盒子模型是网页布局的基础概念，它将每个HTML元素都看作一个矩形的"盒子"。</p>

        <h3>盒子模型的四个组成部分：</h3>

        <ol>

            <li><strong>Content（内容）</strong> - 盒子的中心部分，显示文本、图像等内容</li>

            <li><strong>Padding（内边距）</strong> - 内容与边框之间的空间，背景色/背景图会延伸到内边距</li>

            <li><strong>Border（边框）</strong> - 围绕内容和内边距的边界</li>

            <li><strong>Margin（外边距）</strong> - 盒子与其他元素之间的外部空间</li>

        </ol>

        <h3>盒子总宽度和高度计算公式：</h3>

        <ul>

            <li>总宽度 = width + 左右padding + 左右边框 + 左右margin</li>

            <li>总高度 = height + 上下padding + 上下边框 + 上下margin</li>

        </ul>

    </div>

  

    <div class="container">

        <div class="box box1">

            <h3>盒子 1</h3>

            <p>宽: 200px<br>

               高: 150px<br>

               边框: 8px<br>

               内边距: 10px<br>

               外边距: 15px</p>

        </div>

        <div class="box box2">

            <h3>盒子 2</h3>

            <p>宽: 200px<br>

               高: 150px<br>

               边框: 6px<br>

               内边距: 20px<br>

               外边距: 10px</p>

        </div>

        <div class="box box3">

            <h3>盒子 3</h3>

            <p>宽: 200px<br>

               高: 150px<br>

               边框: 10px<br>

               内边距: 5px<br>

               外边距: 25px</p>

        </div>

    </div>

  

    <div class="explanation">

        <h2>实际例子分析</h2>

        <p>以第一个盒子为例，其实际占用的空间为：</p>

        <ul>

            <li>内容宽度: 200px</li>

            <li>左右内边距: 10px × 2 = 20px</li>

            <li>左右边框: 8px × 2 = 16px</li>

            <li>左右外边距: 15px × 2 = 30px</li>

            <li><strong>总宽度: 200 + 20 + 16 + 30 = 266px</strong></li>

        </ul>

    </div>

    <div class="explanation">

        <h2>Box-sizing 属性</h2>

        <p>默认情况下，width 和 height 设置的是 content 的尺寸。使用 <code>box-sizing: border-box</code> 可以让 width 和 height 包含 padding 和 border：</p>

        <pre>

/* 默认值 */

element {

  box-sizing: content-box;  /* width/height 只包含 content */

}

  

/* 更直观的方式 */

element {

  box-sizing: border-box;   /* width/height 包含 content + padding + border */

}

        </pre>

    </div>

</body>

</html>
```
#### 详细说明
参考链接
https://www.runoob.com/css/css-boxmodel.html
![[Pasted image 20260208224127.png]]
![[Pasted image 20260208224324.png]]

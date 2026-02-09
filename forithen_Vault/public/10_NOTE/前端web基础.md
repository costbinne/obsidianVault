
## 工程级AI在前端页面生成中的主流做法整理

### 一、背景

随着生成式AI在开发领域的应用增加，前端页面的生成不再只是“AI自动写HTML”，而逐渐演变为一种**工程级受控生成模式**。

核心变化是：

`从：AI自由生成HTML 到：AI在规则体系内生成页面`

即：

> AI不是自由设计页面，而是在企业定义好的组件体系和开发规范内自动生成代码。

---

### 二、当前主流的三种工程级AI页面生成模式

### 模式1：设计系统驱动（当前最主流）

#### 核心思路

先定义统一UI组件和样式规则  
AI只能在这些组件内生成页面

#### 基本流程

`设计系统（组件库）    ↓ AI根据mock生成组件结构    ↓ 输出符合规范的页面代码`

#### 示例

公司组件：

`AppForm AppInput AppDatePicker AppButton`

AI生成页面：

`<AppForm action="/searchUser">   <AppInput name="userId" label="用户ID" />   <AppDatePicker name="date" label="日期" />   <AppButton type="submit">搜索</AppButton> </AppForm>`

而不是：

`<form>   <input> </form>`

#### 优点

- 页面风格统一
    
- 可批量生成页面
    
- 后期维护成本低
    
- AI生成更稳定
    

#### 缺点

- 需要先建设组件库
    
- 自由度降低
    

---

### 模式2：模板驱动生成（传统企业常用）

#### 核心思路

先准备标准页面模板  
AI只负责填字段内容

#### 流程

`页面模板    ↓ AI填充字段    ↓ 生成页面`

#### 示例

模板：

`<form method="post" action="{action}">   <label>{label1}</label>   <input name="{name1}"> </form>`

AI生成数据：

`action = "/searchUser" label1 = "用户ID" name1 = "userId"`

系统生成页面。

#### 优点

- 稳定
    
- 易管控
    
- 符合传统开发模式
    

#### 缺点

- 灵活性差
    
- UI创新困难
    

---

### 模式3：Schema / DSL驱动生成（新趋势）

#### 核心思路

AI不生成HTML  
而是生成页面描述数据

即：

`AI → DSL（页面描述） DSL → 渲染引擎 渲染引擎 → HTML页面`

#### 示例

AI生成DSL：

`{   "type": "form",   "action": "/search",   "fields": [     { "type": "text", "name": "userId" },     { "type": "date", "name": "date" }   ] }`

系统自动生成页面。

#### 优点

- AI更容易生成正确结构
    
- 页面完全统一
    
- 支持批量生成
    
- 易维护
    

#### 缺点

- UI自由度较低
    
- 需要额外渲染引擎
    

---

### 三、统一UI组件的概念解释

统一UI组件本质上是：

> 把HTML标签封装成公司内部的标准标签  
> 所有页面只能用这些标签拼装

---

### 无组件体系的情况

不同开发者写法不同：

`<input class="input"> <button class="btn-blue">`

`<input class="form-control"> <button class="primary-button">`

结果：

- 样式混乱
    
- 难维护
    
- AI生成不稳定
    

---

### 有组件体系的情况

公司规定只能使用：

`<AppInput> <AppButton>`

页面代码：

`<AppInput name="userId" /> <AppButton>搜索</AppButton>`

所有页面统一。

---

### 四、为什么要限制原生HTML

这是一种工程管理策略，而不是技术限制。

核心目的有三个：

### 原因1：统一风格

只改组件  
全站样式自动统一

---

### 原因2：降低维护成本

UI改动只改组件  
不用逐页修改

---

### 原因3：让AI生成可控

AI只能在组件规则内生成代码  
不会生成不可维护结构

---

### 实际工程结构

`页面层   └── 只能使用组件  组件层   └── 内部可以使用原生HTML`

即：

`页面： <AppInput />  组件内部： <input>`

---

### 五、UI DSL（页面描述语言）的概念

DSL是：

> 一种用于描述页面结构的语言  
> 由系统引擎解析后生成真实页面

---

### 传统HTML生成

AI直接生成：

`<form>   <input> </form>`

---

### DSL生成方式

AI生成：

`Page:   Form:     action: /search     fields:       - text: userId       - date: date`

系统流程：

`DSL  ↓ 渲染引擎  ↓ 组件结构  ↓ HTML页面`

---

### DSL三层结构

`DSL层   ↓ 组件层   ↓ HTML层`

---

### 六、DSL的工程优势

### 优势1：AI更容易生成正确页面

DSL结构简单  
字段固定

---

### 优势2：系统更易维护

改组件  
所有页面自动更新

---

### 优势3：适合企业系统

银行系统常见页面：

- 查询表单
    
- 列表表格
    
- 操作按钮
    

非常适合DSL描述。

---

### 七、你原始思路的分析

你的原始流程：

`mock → 提示词 → 原型代码 → 指定规则 → 大量应用`

### 正确的地方

你抓住了两个关键点：

#### 正确点1：需要规则

AI必须在规则内生成。

#### 正确点2：CSS必须统一

否则AI生成的class会混乱。

---

### 八、你方案目前的三个主要问题

### 问题1：规则在生成之后才加入

你的流程：

`先生成页面 再指定规则`

主流流程是：

`先定义规则 再生成页面`

---

### 问题2：缺少组件层

你现在是：

`mock → HTML`

主流是：

`mock → 组件结构 → 页面`

---

### 问题3：缺少验证环节

工程级流程必须有：

`AI生成  ↓ 静态检查  ↓ 测试  ↓ 合并`

---

### 九、当前主流的工程级AI页面生成流程

`① 定义设计系统（组件、样式、命名规则） ② 定义页面Schema或DSL结构 ③ AI根据mock生成组件或DSL ④ 自动检查（lint、命名、结构） ⑤ 自动测试 ⑥ 合并到主分支`

---

### 十、未来发展趋势

### 趋势1：AI生成DSL而不是HTML

页面通过DSL描述  
由引擎统一生成。

---

### 趋势2：AI只生成差异代码

例如：

`在UserForm中新增DatePicker`

而不是重写整个页面。

---

### 趋势3：AI参与CI/CD流程

例如：

- 自动修复样式
    
- 自动生成测试
    
- 自动重构组件
    

---

### 十一、整理后的推荐表达方式

可以把你的思路升级为：

`设计系统与开发规则定义    ↓ mock画面生成    ↓ AI根据规则生成组件级代码或DSL    ↓ 自动检查（命名、样式、结构）    ↓ 生成可维护的页面代码    ↓ 批量应用到新页面开发`
## 前端代码与浏览器
前端代码 由 浏览器解析渲染之后 呈现给用户
浏览器进行解析渲染的部分 就是浏览器的内核
由于浏览器内核的不同,对于相同前端代码解析的效果可能会存在差异

为了使网页在不同浏览器的内核下 呈现相同的效果,有开发的标准如下
![[Pasted image 20260208171915.png]]

## 前端代码 基础知识
https://developer.mozilla.org/zh-CN/
推荐查询网站如上
### 重要内容 表单form
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Form练习</title>

</head>

<body>

    <!-- 表单属性：action 提交地址  method 提交方式  enctype 提交编码 -->

     <!-- 关于method：

     get：提交数据时，数据将显示在url后面

     post：提交数据时，数据将不会显示在url后面 -->

     <!-- 表单中的name是表单中元素的标识符，用于在提交表单时识别和获取用户输入的值。

     具体的name例子及说明 -->

     <!-- 注意表单项要想能够采集数据，必须添加name属性，表示当前表单项的名字 -->

     <form action="/save" method="get">

        name:<input type="text" name="name"><br>

        age:<input type="text" name="age"><br>

        <input type="submit" value="提交">

     </form>

  

</body>

</html>
```
![[Pasted image 20260209105738.png]]
![[Pasted image 20260209105753.png]]
换用method为post的时候
![[Pasted image 20260209105837.png]]
但是能在开发者模式中确认到对应的内容
![[Pasted image 20260209110126.png]]
![[Pasted image 20260209110606.png]]

#### 常见表单项
![[Pasted image 20260209110440.png]]
##### Input的type取值
![[Pasted image 20260209110705.png]]
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Form练习</title>

</head>

<body>

    <!-- 表单属性：action 提交地址  method 提交方式  enctype 提交编码 -->

     <!-- 关于method：

     get：提交数据时，数据将显示在url后面

     post：提交数据时，数据将不会显示在url后面 -->

     <!-- 表单中的name是表单中元素的标识符，用于在提交表单时识别和获取用户输入的值。

     具体的name例子及说明 -->

     <!-- 注意表单项要想能够采集数据，必须添加name属性，表示当前表单项的名字 -->

     <form action="/save" method="get">

        name:<input type="text" name="name"><br>

        age:<input type="text" name="age"><br>

  

        <!-- radio的同一组的话 name属性需要一直 -->

        <input type="radio" name="sex" value="1">man

        <!-- Label标签是为了提升用户体验的，可以点击女字就能选中radio -->

        <label ><input type="radio" name="sex" value="2">woman</label><br>

  

        <!-- checkbox 复选框 -->

        爱好：<input type="checkbox" name="hobby" value="1">足球</input>

                <input type="checkbox" name="hobby" value="2">篮球</input>

                <input type="checkbox" name="hobby" value="3">羽毛球</input><br>

  

        <input type="file"><br>

        <input type="date"><br>

        <input type="time"><br>

  

        <input type="submit" value="提交"><br>

        <input type="reset">

     </form>

  

</body>

</html>
```
![[Pasted image 20260209122227.png]]



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
## 全体代码示例
```
<!DOCTYPE html>

<html lang="zh-CN">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Tlias智能学习辅助系统</title>

    <style>

      body {

        margin: 0;

      }

  

      /* 顶栏样式 */

      .header {

          display: flex;

          justify-content: space-between;

          align-items: center;

          background-color:  #c2c0c0;

          padding: 10px 20px;

          box-shadow: 0 2px 5px rgba(0,0,0,0.1);

      }

      /* 加大加粗标题 */

      .header h1 {

          margin: 0;

          font-size: 24px;

          font-weight: bold;

      }

  

      /* 文本链接样式 */

      .header a {

          text-decoration: none;

          color: #333;

          font-size: 16px;

      }

  

      /* 搜索表单区域 */

      .search-form {

          display: flex;

          align-items: center;

          padding: 20px;

          background-color: #f9f9f9;

      }

  

      /* 表单控件样式 */

      .search-form input[type="text"], .search-form select {

          margin-right: 10px;

          padding: 5px 10px;

          border: 1px solid #ccc;

          border-radius: 4px;

          width: 200px;

      }

  

      /* 按钮样式 */

      .search-form button {

          padding: 5px 15px;

          margin-left: 10px;

          background-color: #007bff;

          color: white;

          border: none;

          border-radius: 4px;

          cursor: pointer;

      }

  

      /* 清空按钮样式 */

      .search-form button.clear {

        background-color: #6c757d;

      }

  

      .table {

         min-width: 100%;

         border-collapse: collapse;

      }

  

      /* 设置表格单元格边框 */

      .table td, .table th {

        border: 1px solid #ddd;

        padding: 8px;

        text-align: center;

      }

      .avatar {

        width: 30px;

        height: 30px;

        object-fit: cover;

        border-radius: 50%;

      }

  

      /* 页脚版权区域 */

    .footer {

        background-color: #c2c0c0;

        color: white;

        text-align: center;

        padding: 10px 0;

        margin-top: 30px;

    }

  

    .footer .company-name {

        font-size: 1.1em;

        font-weight: bold;

    }

  

    .footer .copyright {

        font-size: 0.9em;

    }

  

    #container {

      width: 80%;

      margin: 0 auto;

    }

    </style>

</head>

<body>

  <div id="container">

    <!-- 顶栏 -->

    <div class="header">

      <h1>Tlias智能学习辅助系统</h1>

      <a href="#">退出登录</a>

    </div>

  

    <!-- 搜索表单区域 -->

    <form class="search-form" action="#" method="post">

      <input type="text" name="name" placeholder="姓名" />

      <select name="gender">

          <option value="">性别</option>

          <option value="male">男</option>

          <option value="female">女</option>

      </select>

      <select name="position">

          <option value="">职位</option>

          <option value="班主任">班主任</option>

          <option value="讲师">讲师</option>

          <option value="学工主管">学工主管</option>

          <option value="教研主管">教研主管</option>

          <option value="咨询师">咨询师</option>

      </select>

      <button type="submit">查询</button>

      <button type="reset" class="clear">清空</button>

    </form>

  

    <table class="table table-striped table-bordered">

      <thead>

          <tr>

              <th>姓名</th>

              <th>性别</th>

              <th>头像</th>

              <th>职位</th>

              <th>入职日期</th>

              <th>最后操作时间</th>

              <th>操作</th>

          </tr>

      </thead>

      <tbody>

          <tr>

              <td>令狐冲</td>

              <td>男</td>

              <td><img src="https://web-framework.oss-cn-hangzhou.aliyuncs.com/2023/1.jpg" alt="令狐冲" class="avatar"></td>

              <td>讲师</td>

              <td>2021-03-15</td>

              <td>2023-07-30T12:00:00Z</td>

              <td class="btn-group">

                  <button>编辑</button>

                  <button>删除</button>

              </td>

          </tr>

          <tr>

              <td>任盈盈</td>

              <td>女</td>

              <td><img src="https://web-framework.oss-cn-hangzhou.aliyuncs.com/2023/1.jpg" alt="任盈盈" class="avatar"></td>

              <td>学工主管</td>

              <td>2020-04-10</td>

              <td>2023-07-29T15:00:00Z</td>

              <td class="btn-group">

                  <button>编辑</button>

                  <button>删除</button>

              </td>

          </tr>

          <tr>

              <td>岳不群</td>

              <td>男</td>

              <td><img src="https://web-framework.oss-cn-hangzhou.aliyuncs.com/2023/1.jpg" alt="岳不群" class="avatar"></td>

              <td>教研主管</td>

              <td>2019-01-01</td>

              <td>2023-07-30T10:00:00Z</td>

              <td class="btn-group">

                  <button>编辑</button>

                  <button>删除</button>

              </td>

          </tr>

          <tr>

              <td>宁中则</td>

              <td>女</td>

              <td><img src="https://web-framework.oss-cn-hangzhou.aliyuncs.com/2023/1.jpg" alt="宁中则" class="avatar"></td>

              <td>班主任</td>

              <td>2018-06-01</td>

              <td>2023-07-29T09:00:00Z</td>

              <td class="btn-group">

                  <button>编辑</button>

                  <button>删除</button>

              </td>

          </tr>

      </tbody>

    </table>

  

    <!-- 页脚版权区域 -->

    <footer class="footer">

      <p class="company-name">学生信息管理系统</p>

      <p class="copyright">&copy; 2023</p>

    </footer>

  

  </div>

  

</body>

</html>
```
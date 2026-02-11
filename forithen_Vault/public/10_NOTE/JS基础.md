![[Pasted image 20260209125306.png]]
## 如何引入
### 内部脚本
![[Pasted image 20260209173547.png]]
为什么放在body底部
	因为解析完成后才会展示JS之后的Html页面，会影响速度，所以一般放底部
### 外部脚本
类似于CSS文件的引入
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <!-- 1.行内脚本示例 -->

<script src="js/test.js"></script>

<input type="button" value="点击我1" onclick="alert('clicked');"><br>

<button type="button" onclick="alert('clicked');">点击我2</button>

    <script>

        //1.内部脚本

        alert   ("hello world");

    </script>

</body>

</html>

<!-- js可以定义在任意位置 -->

 <script>

    alert("hello world out");

</script>

  

<!-- 外部脚本的引入 使用script标签以及其中的src属性来进行引入 -->
```
## 常量变量
![[Pasted image 20260209174653.png]]
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

  

    <script>

        //1.变量

        let a = 1;

        a = "hello";

        alert   (a);

        const b = "我被输出了";

        console.log(b);//输出常量到控制台
        document.write(b);//写入值到浏览器得body区域

    </script>

</body>

</html>
```
![[Pasted image 20260209175641.png]]
document输出内容如下
![[Pasted image 20260209180236.png]]

## 数据类型
![[Pasted image 20260209180727.png]]
使用typeof可以获取数据类型
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

  

    <script>

        document.write(typeof 1);

    </script><br>

<script>

document.write(typeof null);

</script><br>

<script>

document.write(typeof "hello world");

</script><br>

<script>

document.write(typeof true);

</script><br>

<script>

        let a ;

        document.write(typeof a);

</script><br>

</body>

</html>
```
![[Pasted image 20260209181214.png]]
### 模板字符
![[Pasted image 20260209181423.png]]
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <script>

        let name = "张三";

        let age = 18;

        document.write(`我是${name},今年${age}岁`);

    </script>

</body>

</html>
```
![[Pasted image 20260209183458.png]]

## JS函数
![[Pasted image 20260209183529.png]]
函数的调用
![[Pasted image 20260209183928.png]]
#### 匿名函数
![[Pasted image 20260209184138.png]]
匿名函数的调用
![[Pasted image 20260209184235.png]]
## 自定义对象
![[Pasted image 20260209184501.png]]
![[Pasted image 20260209184838.png]]
![[Pasted image 20260209184852.png]]
![[Pasted image 20260209185023.png]]
这里this指定的全局对象window

## JSON
![[Pasted image 20260209185143.png]]
![[Pasted image 20260209185216.png]]
json本质就是基于js对象的文本，并不是数据和代码
![[Pasted image 20260209185445.png]]
stringfy方法可以将js对象 转换为json
parse就是反向转换
#### 代码例子
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <script>

        //定义一个对象

        let user = {

            name : "张三",

            age : 20,

            sex : "男",

            hobby : ["football","basketball","badminton"],

            /**

             *  I can sing

             *  Output: I can sing in the console

             */

            sing: function(){

                console.log("I can sing")

            }

        }

  

        alert(user);//直接显示JS对象 并不会表示内容

        alert(JSON.stringify(user));//可以尝试将其转换为Json

    </script>

</body>

</html>
```
![[Pasted image 20260209185910.png]]
![[Pasted image 20260209185921.png]]
反向联系
![[Pasted image 20260209190309.png]]

## DOM
![[Pasted image 20260209190513.png]]
![[Pasted image 20260209190538.png]]
每一个标签都会封装成一个对象
标签中的文本对象会被封装成 TEXT
![[Pasted image 20260209190706.png]]
### DOM操作的方法

![[Pasted image 20260209190751.png]]
获取方法
![[Pasted image 20260209190812.png]]
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <h1 id="title1">1111</h1>

    <h1>2222</h1>

    <h1>3333</h1>

    <script>

        //获取dom对象

        let h1 = document.getElementById("title1");

        let h2 = document.querySelectorAll('h1');

        h1.innerHTML = "我是修改后的文本";

        h2[1].innerHTML = "修改后的2号文本";

    </script>

</body>

</html>
```
![[Pasted image 20260209192605.png]]
现在主流是使用queryselector去获取Dom对象

## 事件监听
![[Pasted image 20260211205818.png]]![[Pasted image 20260211205841.png]]
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <button id="btn1">点击我1</button><br>

    <input type="button" id="btn2" value="点击我2"></input><br>

    <input type="button" id="btn3" value="点击我3"></input><br>

    <input type="button" id="btn4" value="点击我4"></input>

    <script>

        document.querySelector('#btn1').onclick = function(){

            alert('点击了1')

        }

        document.querySelector('#btn2').addEventListener('click', function() {alert('点击了2')});

  

        document.querySelector('#btn3').addEventListener('click', () => {alert('点击了3')});

  

        //早期写法 事件源.on

        document.querySelector('#btn4').onclick = () => {

            alert('点击了4')

        }

        /*

            addeventListener()这种方式的好处是可以多次绑定同一事件 拥有更多特性

            而onclick只能绑定一次，多次绑定同一事件按钮只会执行最后一次绑定的函数

            注意btn1先是onlick绑定一次 再用addEventListener绑定一次的话不会覆盖

        */

       document.querySelector('#btn1').addEventListener('click', () => {alert('点击了1 第二次')});

       document.querySelector('#btn2').addEventListener('click', () => {alert('点击了2 第二次')});

       document.querySelector('#btn4').onclick = () => {alert('点击了4 第二次')};

    </script>

</body>

</html>
```
### 事件监听案例
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

  <script>

    //为上述表格添加事件监听，当我的鼠标移到表格的某一行 该行变色背景色#f2e2e2，移除之后变为#fff使用JS先版本语法实现

    //获取表格所有行

    const rows = document.querySelectorAll('.table tbody tr');

    //为每一行添加事件监听

    rows.forEach(row => {

        row.addEventListener('mouseover', () => { //使用mouseenter事件也可以

            row.style.backgroundColor = '#f2e2e2';

        });

        row.addEventListener('mouseout', () => { //使用mouseleave事件也可以

            row.style.backgroundColor = '#fff';

        });

    });

  

  </script>

</body>

</html>
```
### 常见事件
![[Pasted image 20260211212418.png]]
### JS的引入
![[Pasted image 20260211213410.png]]
使用模块JS的时候需要追加type属性
模块化JS指的是使用import和Export关键字的JS文件
![[Pasted image 20260211213554.png]]

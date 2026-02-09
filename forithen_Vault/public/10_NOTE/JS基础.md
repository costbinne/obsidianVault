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

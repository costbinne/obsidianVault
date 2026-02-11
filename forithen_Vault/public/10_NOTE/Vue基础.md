## 构建用户界面
前后端交互的时候 传递的是Json格式的数据
![[Pasted image 20260211213904.png]]
Vue可以将原始的Json数据渲染展示在页面上
这个行为被称为构建用户界面，即基于数据渲染出用户看到的界面
## 渐进式
Vue核心包
	声明式渲染
	组件系统
![[Pasted image 20260211214130.png]]
渐进式就是指可以只使用其中的核心包，不一定全部引入Vue生态
可以根据自己的需要来进行开发
![[Pasted image 20260211214252.png]]
以上为目前Vue开发的常见两种方式

## 框架
![[Pasted image 20260211214345.png]]

## 基础入门
![[Pasted image 20260211214559.png]]
```
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Document</title>

</head>

<body>

    <div id="app">

        <!-- 接受数据渲染 -->

        <h1>{{message}}</h1>

    </div>

    <script type="module">

        //引入Vue

        import { createApp } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'

        //创建Vue实例 用来控制Html中的元素

        createApp({

            /*

               由于要数据驱动视图

               1 所以需要准备数据

               2 通过插值表达式渲染页面

            */

  

            //定义数据

            data() {

                return {

                    message: "Hello Vue"

                }

            }

        }).mount("#app");

    </script>

</body>

</html>
```
实际工程中是由服务器返回数据模型，Vue将数据根据插值表达式渲染到页面。

## 常用指令

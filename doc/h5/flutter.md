## flutter

* [简介](#简介)
* [Dart](#Dart)
* [简介](#简介)


#### 简介
* 极速构建漂亮的原生应用、Dart语言编写逻辑、Widget框架构建UI
* 与RN对比
    * RN采用JS语言开发，基于React，对前端工程师更友好。Dart语言受众小
    * Flutter自己实现了一套UI框架，丢弃了原生的UI框架。而RN还是可以自己利用原生框架，两个各有好处。Flutter的兼容性高，RN可以利用原生已有的优秀UI

#### Dart
* JavaScript和Dart对比
    * 入口点：每个app都必须有一个顶级的main（）函数作为应用程序的入口点
    * 打印到控制台：print('Hello world!')
    * 变量：
        * 变量必须是明确的类型
        * 未初始化的变量的初始值为 null
        * if 判断只有布尔值 true 被视为true 
        * function
        ```js
        // JavaScript
        function fn() {
        return true;
        }
        // Dart
        fn() {
        return true;
        }
        // can also be written as
        bool fn() {
        return true;
        }
        ```
    * 异步编程
        * async 函数返回 Future 对象，await 运算符用于等待 Future


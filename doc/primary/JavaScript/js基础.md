## js基础

* [语法](#语法)
* [变量](#变量)
* [数据类型](#数据类型)
* [运算符](#运算符)
* [条件判断](#条件判断)
* [循环](#循环)
* [函数](#函数)
* [错误](#错误)

#### 语法
* JavaScript 对大小写敏感
* JavaScript 会忽略多余的空格
```js
var carname="Volvo";
等价
var carname = "Volvo";
```
* 可以在`文本字符串`中使用反斜杠\对代码行进行换行（避免一行一行执行）
```js
document.write("你好 \
世界!");
```
* 注释
```js
//单行注释
/*
多行注释
多行注释
*/
```
* 严格模式
```
"use strict"
不能使用未声明的变量
不允许删除变量、对象、函数（delete x;// 报错）
不允许变量重名（function x(p1, p1) {};// 报错）
不允许使用八进制（var x = 010;// 报错）
不允许使用转义字符（var x = \010;// 报错）
不允许对只读属性赋值
不允许对一个使用getter方法读取的属性进行赋值
不允许删除一个不允许删除的属性（delete Object.prototype; // 报错）
变量名不能使用 "eval"| "arguments" 字符串
由于一些安全原因，在作用域 eval() 创建的变量不能被调用
禁止this关键字指向全局对象
```
* void：该操作符指定要计算一个表达式但是不返回值
```js
var a,b,c;
a = void ( b = 5, c = 7 );//a = undefined, b = 5, c = 7
onclick = "javascript:void(0)";//单击此处什么也不会发生
onclick = "javascript:void(alert('Warning!!!'))";//点击后显示警告信息
```
* with：用于设置代码在特定对象中的作用域
```js
//语法：with (expression) statement
var sMessage = "hello";
with(sMessage) {
    console.log(toUpperCase());	//输出 "HELLO"
}
```
* 代码规范
    * 命名规则：
        * 变量：小驼峰法标识, 即除第一个单词之外，其他单词首字母大写（ lowerCamelCase）
        * 常量|全局变量：大写加下划线
        * 函数：前缀为动词 小驼峰
        ```
        can：判断是否可执行某个动作(权限)，返回布尔值
        |has：判断是否含有某个值，返回布尔值
        is：判断是否为某个值，返回布尔值
        ge：获取某个值，返回非布尔值
        set：设置某个值
        load：加载某些数据，返回无或是否加载完成
        ```
        * 类|构造函数：前缀为名称 首字母大写 大驼峰
        ```
        公共属性和方法：跟变量和函数的命名一样
        私有属性和方法：前缀为_(下划线)
        ```
        * TML5 属性可以以 data- (如：data-quantity, data-price) 作为前缀
        * CSS 使用 - 来连接属性名 (font-size)
        * 使用小写文件名
    * 运算符 ( = + - * / ) 前后需要添加空格
    * 代码缩进：4 个空格符号（不推荐使用 TAB 键来缩进，因为不同编辑器 TAB 键的解析不一样）
    * 语句规则：
        * 一条语句通常以分号作为结束符
        * 将左花括号放在第一行的结尾
        * 左花括号前添加一空格
        * 将右花括号独立放在一行
        * 不要以分号结束一个复杂的声明
    * 对象规则：
        * 将左花括号与类名放在同一行
        * 冒号与属性值间有个空格
        * 字符串使用双引号，数字不需要
        * 最后一个属性-值对后面不要添加逗号
        * 将右花括号独立放在一行
        * 以分号作为结束符号
        * 短的对象代码可以直接写成一行
    * 为了便于阅读每行字符建议小于数 80 个，如果超过 80 个字符，建议在运算符或者逗号后换行

#### 变量
* 变量必须以字母开头，也能以 $ 和 _ 符号开头（不推荐）
* 变量名称对大小写敏感
* 变量声明之后不赋值，默认为undefined
* 如果重新声明 JavaScript 变量，该变量的值不会丢失
```js
var carname="Volvo";
var carname; //值依然是 "Volvo"
function myFunction()
{
    carname1="Volvo";// carname1自动作为全局变量
}
```
* JavaScript 变量均为对象。当您声明一个变量时，就创建了一个新的对象
* 局部变量
```
在 JavaScript 函数内部声明的变量（使用 var）是局部变量，所以只能在函数内部访问它。（局部作用域）。
您可以在不同的函数中使用名称相同的局部变量，因为只有声明过该变量的函数才能识别出该变量。
只要函数运行完毕，本地变量就会被删除。
```
* 全局变量
```
在函数外声明的变量是全局变量，网页上的所有脚本和函数都能访问它（全局作用域）
```
* 生存期：
```
生命期从它们被声明的时间开始
局部变量会在函数运行以后被删除
全局变量会在页面关闭后被删除
```

#### 数据类型
* 数据类型
    * 值类型(基本类型)：string、number、boolean、object、null（正常的意料之中的值的空缺）、undefined（类似错误的出乎意料的值的空缺）、symbol（ES6：表示独一无二的值）
    * 引用数据类型：Object、Array、Function
    * 对象类型：Array、Function、Date、RegExp、Error
* 判断类型
    * typeof 数据：返回一个表示数据类型的字符串
        ```js
        Object、Array、null -> object
        function -> function
        undefined -> undefined
        string -> string
        number -> number
        boolean -> boolean
        symbol -> symbol
        ```
    * 实例对象 instanceof 构造函数：判断左操作数对象的原型链上是否有右边这个构造函数的prototype属性
        ```js
        String = String、Object
        ```
    * 实例对象.constructor：返回实例对象的构造函数
        ```js
        "John".constructor                 // 返回函数 String()  { [native code] }
        (3.14).constructor                 // 返回函数 Number()  { [native code] }
        false.constructor                  // 返回函数 Boolean() { [native code] }
        [1,2, 3,4].constructor              // 返回函数 Array()   { [native code] }
        {name:'John', age:34}.constructor  // 返回函数 Object()  { [native code] }
        new Date().constructor             // 返回函数 Date()    { [native code] }
        function() {}.constructor         // 返回函数 Function(){ [native code] }

        myArray.constructor.toString().indexOf("Array") > -1; //判断数组
        ```
    * Object.prototype.toString.call(数据)：返回[object 调用者的具体类型]
        ```js
        String,Number,Boolean,Undefined,Null,Function,Date,Array,RegExp,Error,HTMLDocument,Window
        ```
* 类型转换
    * 函数转换
    ```js
    Number() 转换为数字， String() 转换为字符串， Boolean() 转化为布尔值，一元运算符Operator +将变量转换为数字
    ```
    * 自动转换
    ```js
    5 + null; // 返回 5
    "5" + null; // 返回"5null"
    "5" + 1; // 返回 "51"
    "5" - 1; // 返回 4
    "b" - "a"; // 返回 NaN

    document.getElementById("demo").innerHTML = myVar;
    myVar = 123             // toString 转换为 "123"
    myVar = true            // toString 转换为 "true"
    myVar = false           // toString 转换为 "false"
    myVar = {name:"Fjohn"}  // toString 转换为 "[object Object]"
    myVar = [1,2,3,4]       // toString 转换为 "1,2,3,4"
    myVar = new Date()      // toString 转换为 "Fri Jul 18 2014 09:08:55 GMT+0200"
    ```
    * 隐式转换：==
    ```js

    ```

#### 运算符
* 算术运算符：+、-、*、/、%、++、--

    ```js
    var y = 5;
    var x = ++y;
    x; //6
    y; //6

    var y = 5;
    var x = y++;
    x; //5
    y; //6
    ```

* 赋值运算符：=、+=、-+、*=、/=、%=

    ```js
    var x = 10, y = 5;
    x += y; //x = x + y
    ```

* 字符串连接运算符：+

    ```js
    //数字与字符串相加，结果将成为字符串
    "1" + 1; // "11"
    null + 1; // 1
    undefined + 1; // NaN
    ```

* 比较运算符：==、===、!=、!==、>、<、>=、<=

    ```js
    //会自动进行类型转换
    "5" > 4; // true
    ```

* 逻辑运算符：!、&&、||

    ```js
    逻辑运算符的优先级是：！、&& 、||

    let a = 1;
    0 && (a=2); //0
    a; //1
    ```

* 条件运算符：三元运算符

    ```js
    a = 1 > 2 ? true : false; //false
    ```

* 一元运算符：+

    ```js
    //Operator + 可用于将变量转换为数字
    var y = "5";      // y 是一个字符串
    var x = + y;      // x 是一个数字
    var y = "John";   // y 是一个字符串
    var x = + y;      // x 是一个数字 (NaN)
    var time = +new Date(); //time是当前时间的毫秒数
    ```

#### 条件判断
```
if...else if....else

switch(n)
{
    case 1:
        执行代码块 1
        break;
    case 2:
        执行代码块 2
        break;
    case 3|4:
        执行代码块
        break;
    default:
        与 case 1、2、3、4 不同时执行的代码
}
```

#### 循环
* for循环：循环代码块一定的次数
    ```js
    语句 1：（代码块）开始前执行
    语句 2：定义运行循环（代码块）的条件,布尔值,省略时默认为true会无限循环
    语句 3：在循环（代码块）已被执行之后执行

    for (语句 1; 语句 2; 语句 3)
      {
      被执行的代码块
      }
    ```
* for/in循环：循环遍历对象的属性
    ```js
    var person={fname:"John",lname:"Doe",age:25};
    for (x in person){
      txt=txt + person[x];
    }
    ```
* while 循环：当指定的条件为 true 时循环指定的代码块
* do/while 循环：至少执行一次 (条件);
```
break跳出循环，continue跳过循环中的一个迭代
```
* 标签
    ```js
    /*
    continue 语句（带有或不带标签引用）只能用在循环中。
    break 语句（不带标签引用），只能用在循环或 switch 中。
    通过标签引用，break 语句可用于跳出任何 JavaScript 代码块
    */
    cars=["BMW","Volvo","Saab","Ford"];
    list:
    {
    document.write(cars[0] + "<br>");
    document.write(cars[1] + "<br>");
    document.write(cars[2] + "<br>");
    break list;
    document.write(cars[3] + "<br>");
    document.write(cars[4] + "<br>");
    document.write(cars[5] + "<br>");
    }
    ```

#### 函数

* 匿名函数
```js
var x = function (a, b) {return a * b};
var z = x(4, 3);
```
* 函数提升
```js
myFunction(5);
function myFunction(y) {
    return y * y;
}
```
* 自调用函数
```js
(function () {
    var x = "Hello!!";      // 我将调用自己
})();
```
* return
```js
//在使用 return 语句时，函数会停止执行，并返回指定的值，返回值是可选的
function myFunction()
{
    return;// 跳出函数
}
```
* 构造器函数
```js
function Person(firstname,lastname,age,eyecolor){
   this.firstname=firstname;
   this.lastname=lastname;
   this.age=age;
   this.eyecolor=eyecolor;

   this.changeName=changeName;
   function changeName(name){
       this.lastname=name;
   }
}
var myFather=new Person("Bill","Gates",56,"blue"); //创建对象
myFather.changeName("Ballmer"); //调用对象内方法
```
* Arguments 对象：包含了函数调用的参数数组
```js
x = sumAll(1, 123, 500, 115, 44, 88);
function sumAll() {
    var i, sum = 0;
    for (i = 0; i < arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
}
```
* 预定义的函数方法：call()、 apply()
```js
//两个方法的第一个参数必须是对象本身
//在 JavaScript 严格模式(strict mode)下, 在调用函数时第一个参数会成为 this 的值， 即使该参数不是一个对象。
//在 JavaScript 非严格模式(non-strict mode)下, 如果第一个参数的值是 null 或 undefined, 它将使用全局对象替代
function myFunction(a, b) {
    return a * b;
}
myObject = myFunction.call(myObject, 10, 2);     // 返回 20
myObject = myFunction.apply(myObject, [10, 2]);  // 返回 20
```
* 闭包：可访问上一层函数作用域里变量的函数，即便上一层函数已经关闭
```js
const add = (function () {
    let counter = 0;
    return function () { //内嵌函数可以访问上一层的函数变量
        counter += 1;
        console.log(counter);
    }
})(); //自执行函数只在初始化时执行一次
add();//1
add();//2
add();//3
```

#### 错误

```js
/*try 语句测试代码块的错误。
catch 语句处理错误。
throw 语句创建自定义错误。*/

let x = "123";
try {
    if(!x)  throw "值为空";
    if(isNaN(x)) throw "不是数字";
    x = Number(x);
    if(x < 5)    throw "太小";
    if(x > 10)   throw "太大";
}
catch(err) {
    console.log("错误: " + err);
}
```
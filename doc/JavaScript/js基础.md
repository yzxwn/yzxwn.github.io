## js基础

####1、JavaScript 对大小写敏感

####2、JavaScript 会忽略多余的空格
```js
var carname="Volvo";
等价
var carname = "Volvo";
```

####3、可以在文本字符串中使用反斜杠\对代码行进行换行（避免一行一行执行）

####4、注释
```js
//单行注释
/*
多行注释
多行注释
*/
```

####5、变量
* 变量必须以字母开头，也能以 $ 和 _ 符号开头（不推荐）
* 变量名称对大小写敏感
* 变量声明之后不赋值，默认为undefined
* 如果重新声明 JavaScript 变量，该变量的值不会丢失
```js
var carname="Volvo";
var carname; //值依然是 "Volvo"
```
* 生存期：

    生命期从它们被声明的时间开始

    局部变量会在函数运行以后被删除

    全局变量会在页面关闭后被删除

####6、数据类型：
* 数据类型
    * 字符串、数字、布尔、数组、对象、Null（值为空）、Undefined（不含有值）
    * JavaScript 中的所有事物都是对象
    * 数据类型：string、number、boolean、object、function
    * 对象类型：Object、Date、Array
    * 不包含任何值的数据类型：null、undefined
* 判断类型
    * typeof 操作符
        ```js
        typeof "John"                 // 返回 string
        typeof 3.14                   // 返回 number
        typeof NaN                    // 返回 number
        typeof false                  // 返回 boolean
        typeof [ 1,2,3,4]              // 返回 object
        typeof {name: 'John', age:34}  // 返回 object
        typeof new Date()             // 返回 object
        typeof function () {}         // 返回 function
        typeof myCar                  // 返回 undefined
        typeof null                   // 返回 object
        ```
    * constructor 属性：返回所有 JavaScript 变量的构造函数
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
* 类型转换
    * 函数转换
    ```js
    Number() 转换为数字， String() 转换为字符串， Boolean() 转化为布尔值。

    String(false); // "false"

    Number("3.14"); //3.14
    Number("3a14"); //NaN
    Number(false); // 0
    Number(true); // 1
    Number(new Date()); // 毫秒数

    var y = "5"; // y 是一个字符串("5")
    var x = + y; // x 是一个数字(5)
    var y = "John"; // y 是一个字符串("John")
    var x = + y; // x 是一个数字 (NaN)
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

####7、函数：

在使用 return 语句时，函数会停止执行，并返回指定的值，返回值是可选的
```js
function myFunction()
{
    carname="Volvo";// carname自动作为全局变量
    return;// 跳出函数
}
```

####8、运算符：
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

* 逻辑运算符：&&、||、!

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

####9、循环：
```
break跳出循环，continue跳过循环中的一个迭代
```
* 标签
    ```js
    /*
    break 和 continue 语句仅仅是能够跳出代码块的语句
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
* for循环
    ```js
    语句可选
    语句2:循环是否继续条件,布尔值,省略时默认为true会无限循环

    for (语句 1; 语句 2; 语句 3)
      {
      被执行的代码块
      }
    ```
* for/in循环
    ```js
    遍历对象的属性

    var person={fname:"John",lname:"Doe",age:25};
    for (x in person){
      txt=txt + person[x];
    }
    ```
* while 循环
* do/while 循环：至少执行一次 (条件);

####10、构造器函数
```js
function person(firstname,lastname,age,eyecolor){
   this.firstname=firstname;
   this.lastname=lastname;
   this.age=age;
   this.eyecolor=eyecolor;

   this.changeName=changeName;
   function changeName(name){
       this.lastname=name;
   }
}

var myFather=new person("Bill","Gates",56,"blue"); //创建对象
myFather.changeName("Ballmer"); //调用对象内方法
```
## Json

* **语法**
```
JSON: JavaScript Object Notation(JavaScript 对象表示法)
JSON 是存储和交换文本信息的语法。类似 XML。
JSON 比 XML 更小、更快，更易解析。
JSON 文件的文件类型是 ".json"
JSON 文本的 MIME 类型是 "application/json"
JSON 值：数字、字符串、布尔值、数组、对象、null
（名称: 值）：名称必须在双引号中，字符串值必须在双引号中
JSON 不能存储 Date 对象，JSON.stringify会自动将其转换为字符串
JSON 不允许包含函数，但你可以将函数作为字符串存储，之后再将字符串转换为函数（fun = eval("(" + funstr + ")")），JSON.stringify会删除函数属性
eval() 函数使用的是 JavaScript 编译器，可解析 JSON 文本，然后生成 JavaScript 对象。必须把文本包围在括号中，这样才能避免语法错误
```
* **使用**
```js
//循环对象属性
var myObj = { "name":"runoob", "alexa":10000, "sites":[1, 2, 3] };
for (x in myObj) {
    document.getElementById("demo").innerHTML += x + "<br>";
}
//删除对象属性
delete myObj.sites;
//删除数组元素
delete myObj.sites[1];
```
* **JSON.parse(text, reviver?)**：将一个 JSON 字符串转换为 JavaScript 对象
```js
//text:一个有效的 JSON 字符串；reviver: 一个转换结果的函数， 将为对象的每个成员调用此函数
var text = '{ "name":"Runoob", "initDate":"2013-12-14", "site":"www.runoob.com"}';
var obj = JSON.parse(text, function (key, value) {
    if (key == "initDate") {
        return new Date(value);
    } else {
        return value;
}});
document.getElementById("demo").innerHTML = obj.name + "创建日期：" + obj.initDate;
```
* **JSON.stringify(value, replacer?, space?)**：将 JavaScript 值转换为 JSON 字符串
```js
//value:一个有效的 JSON 对象
/*replacer:用于转换结果的函数或数组。
如果 replacer 为函数，则 JSON.stringify 将调用该函数，并传入每个成员的键和值。
使用返回值而不是原始值。如果此函数返回 undefined，则排除成员。根对象的键是一个空字符串：""。
如果 replacer 是一个数组，则仅转换该数组中具有键值的成员。
成员的转换顺序与键在数组中的顺序一样。当 value 参数也为数组时，将忽略 replacer 数组。*/
/*space:文本添加缩进、空格和换行符。
如果 space 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 space 大于 10，则文本缩进 10 个空格。
space 也可以使用非数字，如：\t。*/
const str = {"name":"菜鸟教程", "site":"http://www.runoob.com"};
str_pretty2 = JSON.stringify(str, null, 4) //使用四个空格缩进
```
* **JSONP**
```js
/*
Jsonp(JSON with Padding) 是 json 的一种"使用模式"，可以让网页从别的域名（网站）那获取资料，即跨域读取数据
因为同源策略，所以从不同的域（网站）访问数据需要一个特殊的技术(JSONP )
*/
/*
如客户想访问 : http://www.runoob.com/try/ajax/jsonp.php?jsonp=callbackFunction。
假设客户期望返回JSON数据：["customername1","customername2"]。
真正返回到客户端的数据显示为: callbackFunction(["customername1","customername2"])。
*/
function callbackFunction(result, methodName)
{
    var html = '<ul>';
    for(var i = 0; i < result.length; i++)
    {
        html += '<li>' + result[i] + '</li>';
    }
    html += '</ul>';
    document.getElementById('divCustomers').innerHTML = html;
}
```


## Ajax

* **原理**
```js
//1、创建 XMLHttpRequest 对象
let xmlhttp;
if (window.XMLHttpRequest) {
    xmlhttp=new XMLHttpRequest();//  IE7+, Firefox, Chrome, Opera, Safari 浏览器
} else {

    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");// IE6, IE5 浏览器
}
//2、向服务器发送请求
/*
xmlhttp.open(method,url,async);
    method：请求的类型；GET 或 POST
    url：文件在服务器上的位置
    async：true（异步）或 false（同步）
xmlhttp.setRequestHeader(header,value);
    header: 规定头的名称
    value: 规定头的值
xmlhttp.send(string);
    string：仅用于 POST 请求
*/
xmlhttp.open("POST","/try/ajax/demo_post2.php",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Henry&lname=Ford");
//3、onreadystatechange 事件
/*
XMLHttpRequest 对象的属性：
    onreadystatechange：存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。
    readyState：存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
        0: 请求未初始化
        1: 服务器连接已建立
        2: 请求已接收
        3: 请求处理中
        4: 请求已完成，且响应已就绪
    status：
        200: "OK"
        404: 未找到页面
*/
xmlhttp.onreadystatechange=function()
{
    if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;//保存返回结果
    }
}
```
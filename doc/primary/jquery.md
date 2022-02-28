## jQuery

* [源码分析](https://www.cnblogs.com/aaronjs/p/3278578.html#_h1_0)
4.0.0-pre

#### 项目分析
```
使用git进行项目版本管理，使用nodejs进行项目开发，使用grunt进行项目工程化管理
```
* 整体模块划分
```
核心模块：创建和初始化jQuery对象、涉及的文件
功能模块：属性操作、样式操作、元素操作、动画操作、事件操作、Ajax操作、遍历
底层模块：数据缓存、队列、回调、工具方法
```
* jQuery函数（core.js）
```js
return new jQuery.fn.init( selector, context ); //方便使用时可以省略new
init.prototype = jQuery.fn; //同步原型对象
jQuery.fn = jQuery.prototype; //简化编程
```
* jQuery.prototype对象（core.js）
```js
toArray() //jQuery对象转换成数组，提高编程效率
get(num) //获取jQuery对象的某个元素或全部元素
pushStack(elems) //添加元素数组为jQuery对象的prevObject，返回新对象
```
 * init(selector, context, root)
 ```
选择器：
    string
    domElement
    function
 ```

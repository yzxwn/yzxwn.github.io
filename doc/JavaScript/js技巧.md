## js技巧

#### 数据类型

1、判断数据类型
```
1. 判断数组：Array.isArray(arr)
2. typeof:未定义-undefined，对象|null|数组-object
3. 判断对象和函数，一个变量是否是某个对象的实例：new Array() instanceof Array === true
    Object.prototype.toString.call(undefined) === "[object Undefined]" //准确返回首字母大写数据类型
```

#### 代理

[原文](https://segmentfault.com/a/1190000016468988)

#### 数组去重

[原文](https://segmentfault.com/a/1190000016418021)

1、es6 set去重

代码最少，无法去掉空对象
```js
function unique (arr) {
  return Array.from(new Set(arr))
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
 //[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]
```

2、for循环，splice去重
```js
function unique(arr){
        for(var i=0; i<arr.length-1; i++){
            for(var j=i+1; j<arr.length; j++){
                if(arr[i]==arr[j]){         //第一个等同于第二个，splice方法删除第二个
                    arr.splice(j,1);
                    j--;
                }
            }
        }
return arr;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
    console.log(unique(arr))
    //[1, "true", 15, false, undefined, NaN, NaN, "NaN", "a", {…}, {…}]     //NaN和{}没有去重，两个null直接消失了
```

## es6

* [es6文档](http://es6.ruanyifeng.com/)
* [babel文档](http://www.ruanyifeng.com/blog/2016/01/babel.html)
* [babel官网](https://babeljs.io/)

#### babel
* bug
```js
[...new Set([1,2,3])]   //转换成new Set([1,2,3]).slice()
```
* babel-polyfill
```
Babel 默认只转换新的 JavaScript 句法，而不转换新的 API ，
如 Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise 等全局对象，
以及一些定义在全局对象上的方法（如 Object.assign、Array.from ）都不会转码。
```

#### es6快捷环境搭建
```
1).npm init
2).npm i babel-cli babel-preset-es2015 -D
3).新建.babelrc
{
  "presets": [
    "es2015"
    ],
  "plugins": []
}
4).package.json快捷命令
    "run": "babel-node index.js",
    "build": "babel index.js -o dist/index.js"
5)新建dist文件夹
```

#### let和const
```
1）块级作用域
2）不存在变量提升
3）暂时性死区：块级作用域内，声明的变量会绑定这个区域，声明变量之前不能使用该变量
4）不允许重复声明（相同作用域内）
5）const 声明的变量必须提供一个初始值，而且会被认为是常量（变量指向的内存地址不能改变）
6）let、const、class 声明的全局变量不属于顶层对象（window/global）的属性
```

#### 解构赋值
```
1）模式匹配：只要等号两边的模式相同，左边的变量就会被赋予对应的值
2）允许指定默认值：严格等于undefined时默认值生效
3）不能将{}写在行首：已声明变量应放在圆括号里赋值，写成({x}={x:1})
4）可以重命名变量：let {x:y} = {x:1}
5）可以解构数组、对象、字符串、数值、布尔值，除数组和对象都先转为对象，所以不能解构undefined和null
6）可以解构函数参数
7）圆括号：不能使用圆括号（变量声明模式、函数参数、赋值语句的模式），可以使用圆括号（赋值语句：非模式部分）
```

#### 字符串
* **字符支持Unicode表示法**
```
字符以 UTF-16 的格式储存，每个字符固定为2个字节。
对于那些需要4个字节储存的字符（ Unicode 码点大于 OxFFFF 的字符）,JavaScript也会认为它们是2个字符
str.codePointAt(index)：能够正确处理4个字节储存的字符
str.at(index)：返回指定索引位置的字符（可以识别Unicode编号大于0xFFFF的字符）
String.fromCharCode(str)：从码点返回对应字符，但是这个方法不能识别 32 位的 UTF-16 字符（ Unicode 编号大于 OxFFFF)
```
* **字符串遍历**：for...of（可以识别Unicode 码点大于 OxFFFF 的字符）
* **includes(str, n?)**：返回布尔值，表示是否找到了参数字符串从n索引位置开始搜索
* **startsWith(str, n?)**：返回布尔值，表示参数字符串是否在源字符串的头部从n索引位置开始搜索
* **endsWith(str, n?)**：返回布尔值，表示参数字符串是否在源字符串的尾部在前n个位置
* **repeat(n)**：返回一个新字符串，表示将原字符串重复n次（n>-1，n只保留整数位，NaN等于0，字符串会转换成数字）
* **padStart(n, str?)**：返回用str或空格补全到n长度的字符串
* **padEnd(n, str?)**：返回用str或空格补全到n长度的字符串
* **模板字符串**：`${x} + ${y} = ${x + y}`
* **标签模板**：
```
alert`123`// 等同于alert(123)
var a = 5, b = 10;
tag`Hello ${ a + b } world ${ a * b }`;
// 等同于
tag(['Hello ', ' world ', ''], 15, 50);
```

#### RegExp构造函数
* **new RegExp()**：第一个参数是正则表达式时，允许使用第二个参数添加修饰符（覆盖原有修饰符）
* **字符串的正则方法**：字符串对象能使用正则的4个方法在语言内部全部调用RegExp的实例方法
```
String.prototype.match 调用 RegExp.prototype[Symbol.match]
String.prototype.replace 调用 RegExp.prototype[Symbol.replace)
String.prototype.search 调用 RegExp.prototype[Symbol.search)
String.prototype.split 调用 RegExp.prototype[Symbol.split)
```
* **u 修饰符**：Unicode 模式，用来正确处理大于\uFFFF的 Unicode 字符
* **y 修饰符**：粘连修饰符，y修饰符的设计本意就是让头部匹配标志 ^ 在全局匹配中都有效（g 修饰符只要剩余位置中存在匹配就行，而 y 修饰符会确保匹配必须从剩余的第一个位置开始）
* **s 修饰符**：dotAll 模式，点（ . ）代表一切字符（包括行终止符）
* **flags**：返回正则表达式的修饰符
* **后行断言**：
```
先行断言：只匹配y前面的x，/x(?=y)/
先行否定断言：只匹配不在y前面的x，/x(?!y)/
后行断言：只匹配y后面的x，/(?<=y)x/
后行否定断言：只匹配不在y后面的x，/(?<!y)x/
```
* **具名组匹配**：允许为每一个组匹配指定一个名字?<组名>（正则表达式使用圆括号进行组匹配）
```
//指定组名
const RE_DATE = /(?<year>\d{4})-(?<month>\d{2} )-(?<day>\d{2})/;
const matchObj = RE_DATE.exec ( "1999-12-31");
const year= matchObj.groups.year; // 1999
const month= matchObj.groups.month; // 12
const day= matchObj.groups.day ; // 31
//replace替换
"2015-01-02".replace(RE_DATE, "$<day>/$<month>/$<year>"); // 02/01/2015
//重复引用
/(?<word>\d+)!\k<word>/.test("12!12"); // true
```

#### 数值
* **二进制和八进制表示法**：用前缀 0b （或0B）和 0o（或0O）表示
* **指数运算符**：**（a **= 3 等同 a = a*a*a）
* **Integer数据类型**：整数类型的数据只用来表示整数，没有位数的限制，任何位数的整数都可以精确表示（为了与 Number 类型区别，Integer 类型的数据必须使用后缀n来表示）
```
typeof 123n; // "integer"
Integer(123); // 123n
```
* **Number.isFinite()**：检查一个数值是否为有限的（非number类型都返回false，全局isFinite()会先将非数值转换为数值）
* **Number.isNaN()**：检查一个数值是否为NaN（只有NaN返回true，非NaN都返回false，全局isNaN()将非数值转换为数值后为NaN的都返回true）
* **Number.parseInt()**：Number.parseInt === parseInt
* **Number.parseFloat()**：Number.parseFloat === parseFloat
* **Number.isInteger()**：判断一个值（必须是number类型）是否为整数（在JavaScript内部，整数和浮点数是同样的储存方法，所以3和3.0被视为同一个值）
* **Number.EPSILON()**：引入一个这么小的量，目的在于为浮点数计算设置一个误差范围
* **安全整数**：
```
//JavaScript能够准确表示的整数范围在-2**53和2**53之间（不含两个端点），超过这个范围就无法精确表示
Number.MAX SAFE INTEGER === Math.pow(2, 53) - 1; // true
Number.MIN SAFE INTEGER === -Number.MAX SAFE INTEGER; // true
//Number.isSafeInteger()：用来判断一个整数是否落在这个范围之内
```
* **Math.trunc()**：去除一个数的小数部分，返回整数部分（非数值先转换成数值，不传值和无法取整的值返回NaN）
* **Math.sign()**：判断一个数到底是正数、负数，还是零（非数值先转换成数值，正数：1，负数：-1,0：0，-0：-0，其他值：NaN）
* **Math.signbit()**：判断一个数的符号位是否己经设置（负值和-0返回true）
* **Math.cbrt()**：计算一个数的立方根（非数值先转换成数值，不传值和无法计算的值返回NaN）
* **Math.clz32()**：JavaScript的整数使用32二进制形式表示，返回一个数的32位无符号整数形式有多少个前导0
* **Math.imul()**：返回两个数以32位带符号整数形式相乘的结果，返回的也是32的带符号整数
* **Math.fround()**：返回一个数的单精度浮点数形式
* **Math.hypot()**：返回所有参数的平方和的平方根
* **Math.expm1(x)**：）返回e**x-1，即 Math exp(x) - l
* **Math.log1p(x)**：法返回 ln(l+x），即 Math.log(l + x)如果x小于-1，则返回 NaNo
* **Math.log10(x)**：返回以10为底的x的对数。如果x小于0，则返回 NaN
* **Math.log2(x)**：返回以2为底的x的对数。如果x小于0，则返回 NaN
* **Math.sinh(x)**：返回x的双曲正弦
* **Math.cosh(x)**：返回x的双曲余弦
* **Math.tanh(x)**：返回x的双曲正切
* **Math.asinh(x)**：返回x的反双曲正弦
* **Math.acosh(x)**：返回x的反双曲余弦
* **Math.atanh(x)**：返回x的反双曲正切

#### 函数
* **参数默认值**：参数为undefined时取默认值（指定了默认值以后，函数的length属性将返回没有指定默认值的参数个数，如果设置了默认值的参数不是尾参数，那么length属性也不再计入后面的参数）
* **rest参数**：（...变量名），用数组获取函数的多余参数，这样就不需要使用 arguments 对象了（函数的length属性不包括 rest 参数）
* **严格模式**：只要函数参数使用了默认值、解构赋值或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则就会报错
* **name属性**：返回该函数的函数名（如果将一个匿名函数赋值给一个变量， ES5 name 属性会返回空字符串，而 ES6 name 属性会返回变量名）
* **箭头函数**：
```
1）函数体内的 this 对象就是定义时所在的对象，而不是使用时所在的对象
2）不可以当作构造函数。就是说不可以使用 new 命令，否则会抛出错误
3）不可以使用 arguments 对象，该对象在函数体内不存在。可以用 rest 参数代替
4）不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数
5）super和new.target分别指向层函数的对应变量
6）由于箭头函数没有自己的 this，所以不能用 call()、apply()、bind()这些方法去改变 this 的指向
```
* **（函数式编程）尾调用优化**：
    * 尾调用：指某个函数的最后一步操作是调用另一个函数
    ```
    function f(x){
        return g(x);
    }
    ```
    * 尾调用优化：尾调用由于是函数的最后一步操作，并且不再用到外层函数的内部变量，所以不需要保留外层函数的调用帧，直接用内层函数的调用帧取代外层函数的即可
    ```
    ES6 的尾调用优化只在严格模式下开启，正常模式下是无效的
    自己实现优化：采用“循环”替换“递归”
    ```
    * 尾递归：函数调用自身称为递归。如果尾调用自身就称为尾递归
    ```
    递归非常耗费内存，因为需要同时保存成百上千个调用帧，很容易发生“栈溢出”错误。
    但对于尾递归来说，由于只存在一个调用帧，所以永远不会发生“栈溢出”错误，相对节省内存。
    ```
* **函数参数允许有尾逗号**

#### 数组
* **扩展运算符**：三个点（...），如同 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列
```
1）合并数组
2）与解构赋值结合
3）函数的多个返回值
4）将字符串转为真正的数组
5）任何实现了 Iterator 接口的对象都可以用扩展运算符转为真正的数组
```
* **Array.from(obj, fun?, callThis?)**：将两类对象转为真正的数组：类似数组的对象（NodeList、arguments）和可遍历（Iterator）的对象（字符串、Set）
```
fun：对每个元素进行处理，将处理后的值放入返回的数组
callThis：绑定fun内部this
```
* **Array.of()**：用于将一组值转换为数组（Array.of(3,11,8) //[3,11,8]）
* **copyWithin(target, start?, end?)**：在当前数组内部将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组
```
target：从该位置开始替换数据
start：：从该位置开始读取数据，默认为0。如果为负值，表示倒数
end：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数
参数都应该是数值，如果不是，会自动转为数值
[ 1, 2 , 3 , 4, 5] .copyWithin ( 0 , 3 , 4) // [4 , 2 , 3 , 4, 5]
```
* **find(function(value,index,arr){})**：用于找出第一个符合条件的数组成员
* **findIndex(function(value,index,arr){})**：用于找出第一个符合条件的数组成员的位置
* **fill(str, start?, end?)**：使用给定值填充数组（数组中已有元素会被覆盖），可指定起始和结束位置
* **entries()**：返回一个遍历器对象，可用 for...of 或遍历器对象的 next 方法循环遍历，键值对
* **keys()**：返回一个遍历器对象，可用 for...of 或遍历器对象的 next 方法循环遍历，键名
* **values()**：返回一个遍历器对象，可用 for...of 或遍历器对象的 next 方法循环遍历，键值
* **includes(str, start?)**：判断数组是否包含给定的值
```
start：表示搜索的起始位置，默认为0。如果为负数，则表示倒数的位置，如果负值大于数组长度，则为0
对比indexOf：找到参数值的第一个出现位置，内部使用严格相等符（===）不能识别NaN
```
* **数组的空位**：指数组的某一个位置没有任何值（for...of 没有忽略它，map 方法遍历会跳过空位）

#### 对象
* **属性简写、方法简写**：{a,b(){}}
* **属性名表达式**：obj["h"+"ello"]
* **属性的可枚举性**：enumerable
```
Object.getOwnPropertyDescriptor()：获取对象某个属性的描述对象，用于控制该属性的行为
忽略不可枚举的属性：
1）for...in 循环：只遍历对象自身的和继承的可枚举属性
2）Object.keys()：返回对象自身的所有可枚举属性的键名
3）JSON.stringify()：只串行化对象自身的可枚举属性
4）Object.assign()：只复制对象自身的可枚举属性
5）ES6 规定，所有 Class 的原型的方法都是不可枚举的
```
* **属性的遍历**：
```
1）for...in 循环：只遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）
2）Object.keys(obj)：返回对象自身的所有可枚举属性的键名（不含 Symbol 属性）
3）obj.getOwnPropertyNames(obj)：返回对象自身的所有属性（不含 Symbol 属性）
4）obj.getOwnPropertySymbols(obj)：返回对象自身的所有 Symbol 属性
5）Reflect.ownKeys(obj)：返回对象自身的所有属性
遍历顺序：属性名为数值从小到大排序->属性名为字符串生成时间排序->属性名为Symbol生成时间排序
```
* **Object.is()**：判断两个值是否严格相等（与严格相等不同点：NaN等于自身，+0和-0不相等）
* **Object.assign(target,source1?,source2?...)**：将源对象source的所有可枚举属性复制到目标对象target，返回修改后的目标对象（浅拷贝）
* **Object.keys(obj)**：返回对象自身的所有可枚举属性的键名（不含 Symbol 属性）
* **Object.values(obj)**：返回对象自身的所有可枚举属性的键值（不含 Symbol 属性）
* **Object.entries(obj)**：返回对象自身的所有可枚举属性的键值对（不含 Symbol 属性）（将对象转为真正的Map结构：new Map(Object.entries(obj))）
* **_proto_属性**：读取或设置当前对象的 prototype 对象（建议使用 Object.setPrototypeOf()（写操作）、 Object.getPrototypeOf()（读操作）或 Object.create()（生成操作）代替）
* **Object.setPrototypeOf(obj, prototype)**：设置一个对象的 prototype 对象
* **Object.getPrototypeOf(obj)**：读取一个对象的 prototype 对象
* **扩展运算符**：将所有可遍历的、但尚未被读取的属性分配到指定的对象上面（浅拷贝）
* **Object.getOwnPropertyDescriptor(obj,属性名)：获取对象某个属性的描述符
* **Object.getOwnPropertyDescriptors(obj)：获取对象所有自身属性的描述符

#### Symbol
* **Symbol(str?)**：新的原始数据类型，表示独一无二的值（参数只表示对当前 Symbol 值的描述，相同参数的 Symbol 函数的返回值是不相等的。Symbol可转换为String或Boolean类型）
* **作为属性名的 Symbol**：防止命名冲突
* **Symbol.for(str)**：搜索全局环境中有没有以该参数作为名称的 Symbol 值(以Symbol.for形式生成的)。如果有，就返回这个 Symbol 值，否则就新建井返回一个以该字符串为名称的 Symbol 值
* **Symbol.keyFor(symbol)**：返回一个己登记(以Symbol.for形式生成)的 Symbol 类型值的 key
* **内置的 Symbol 值**
    * **Symbol.hasInstance**：该属性指向一个内部方法，对象使用 instanceof 运算符时会调用这个方法，判断该对象是否为某个构造函数的实例
    ```
    foo instanceof Foo //等同于 Foo[Symbol.hasInstance](foo)
    ```
    * **Symbol.isConcatSpreadable**：表示对象使用Array.prototype.concat()时是否可以展开
    ```
    const obj = [3,4]
    obj[Symbol.isConcatSpreadable] = false;
    [1,2].concat(obj, 5) //[1,2,[3,4],5]
    ```
    * **Symbol.species**：指向当前对象的构造函数
    ```
    class MyArray extends Array {
        static get [Symbol.species]() { return Array ; }
    }
    var a= new MyArray(1, 2, 3) ;
    var mapped= a.map(x => x * x) ;
    mapped instanceof MyArray // false
    mapped instanceof Array // true
    ```
    * **Symbol.match**：该属性指向一个函数，当执行 str.match(myObject)时，如果该属性存在，会调用它返回该方法的返回值
    ```
    String.prototype.match(regexp)  // 等同于 regexp[Symbol.match](this)
    ```
    * **Symbol.replace**：该属性指向一个方法，当对象被 String.prototype.replace 方法调用时会返回该方法的返回值
    * **Symbol.search**：
    * **Symbol.split**：
    * **Symbol.iterator**：指向该对象的默认遍历器方法
    * **Symbol.toPrimitive**：该属性指向一个方法，对象被转为原始类型的值时会调用这个方法，返回该对象对应的原始类型值
    * **Symbol.toStringTag**：该属性指向一个方法，在对象上调用 Object.prototype.toString 方法时，如果这个属性存在，其返回值会出现在 toString 方法返回.的字符串中，表示对象的类型
    * **Symbol.unscopables**：该属性指向一个对象，指定了使用 with 关键字时哪些属性会被 with 环境排除

#### Set
* **new Set()**：类似于数组，但是成员的值都是唯一的（接受一个数组或者具有 iterable 接口的其他数据结构作为参数，类似于严格相等但NaN等于自身）
* **Set.prototype.size**：返回 Set 实例的成员总数
* **操作方法**
    * **add(value)**：添加某个值，返回 Set 结构本身
    * **delete(value)**：删除某个值，返回一个布尔值，表示删除是否成功
    * **has(value)**：返回一个布尔值，表示参数是否为 Set 的成员
    * **clear()**：清除所有成员，没有返回值
* **遍历方法**
    * **keys()**：返回键名的遍历器
    * **values()**：返回键值的遍历器
    * **entries()**：返回键值对的遍历器
    * **forEach()**：使用回调函数遍历每个成员
* **WeakSet**
* **new WeakSet()**：
```
1）成员只能是对象
2）成员对象都是弱引用，即垃坡回收机制不考虑 WeakSet 对该对象的引用，避免内存泄漏
操作方法：add()、delete()、has()
```

#### Map
* **new Map()**：类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键（接受一个数组且该数组的成员是一个个表示键值对的数组或者任何具有 Iterator 接口且每个成员都是一个双元素数组的数据结构作为参数）
* **Map.prototype.size**：返回 Map 实例的成员总数
* **操作方法**
    * **set(key,value)**：设置 key 对应的键值，返回整个 Map 结构
    * **get(key)**：读取 key 对应的键值
    * **has(key)**：判断某个键是否在 Map 数据结构中
    * **delete(key)**：删除某个值，返回一个布尔值，表示删除是否成功
    * **clear()**：清除所有成员，没有返回值
* **遍历方法**
    * **keys()**：返回键名的遍历器
    * **values()**：返回键值的遍历器
    * **entries()**：返回所有成员的遍历器
    * **forEach()**：使用回调函数遍历每个成员
* **WeakMap**
* **new WeakMap()**：
```
1）键名只能是对象
2）键名所指向的对象不计入垃圾回收机制
操作方法：get()、set()、has()、delete()
```

#### Proxy（代理器）
* **new Proxy(target, handler)**：
```
元编程：对编程语言进行编程
Proxy：用于修改某些操作的默认行为，在目标对象前架设一个“拦截”层 ，外界对该对象的访问都必须先通过这层拦截，因此提供了一种机制可以对外界的访问进行过滤和改写
target：表示所要拦截的目标对象
handler：一个对象，用来定制拦截行为
针对Proxy实例进行的操作才会被拦截，对目标对象操作不会拦截
```
* **拦截方法**：
    * **get(target,propKey,receiver)**：拦截对象属性的读取
    * **set(target,propKey,value,receiver)**：拦截对象属性的设置，返回布尔值
    * **has(target,propKey)**：拦截 propKey in proxy 的操作，返回布尔值
    * **deleteProperty(target,propKey)**：拦截 delete proxy[propKey] 的操作，返回布尔值
    * **ownKeys(target)**：拦截 Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy) 的操作，返回数组
    * **getOwnPropertyDescriptor(target,propKey)**：拦截 Object.getOwnPropertyDescriptor(proxy,propKey)，返回属性的描述对象
    * **defineProperty(target,propKey,propDesc)**：拦截 Object.defineProperty(proxy,propKey,propDesc)、Object.defineProperties(proxy,propDescs)，返回布尔值
    * **preventExtensions(target)**：拦截 Object.preventExtensions(proxy)，返回布尔值
    * **getPrototypeOf(target)**：拦截 Object.getPrototypeOf(proxy)，返回一个对象
    * **isExtensible(target)**：拦截 Object.isExtensible(proxy)，返回布尔值
    * **setPrototypeOf(target,proto)**：拦截 Object.setPrototypeOf(proxy,proto)，返回布尔值
    * **apply(target,object,args)**：拦截Proxy实例，并将其作为函数调用的操作，比如 proxy(...args)、proxy.call(object,...args)、proxy.apply(...)
    * **construct(target,args)**：拦截Proxy实例作为构造函数调用的操作，比如 new proxy(...args)
* **Proxy.revocable()**：返回一个可取消的 Proxy 实例
```
使用场景：目标对象不允许直接访问，必须通过代理访问，一旦访问结束，就收回代理权，不允许再次访问
let {proxy, revoke} = Proxy.revocable({a:1}, {});
proxy.a; // 1
revoke();
proxy.too; // TypeError: Revoked
```
* **this问题**：
```
//内部的 this 指向 proxy，有些原生对象的内部属性只有通过正确的 this 才能获取，所以 Proxy 无法代理这些原生对象的属性
let target= new Date("2015-01-01");
let handler= {};
nst proxy= new Proxy(target , handler);
proxy.getDate(); // TypeError: this is not a Date object.
handler = {
    get(target, propKey) {
        if (propKey === "getDate") {
            return target.getDate.bind(target);
        }
        return Reflect.get(target, propKey);
    }
};
proxy.getDate(); // 1
```

#### Reflect
```
1）将 Object 对象的一些明显属于语言内部的方法放到 Reflect 对象上（比如 Object.defineProperty）
2）修改某些 Object 方法的返回结果，让其变得更合理（比如 Object.defineProperty(obj,name,desc) 在无法定义属性时会抛出错误，而 Reflect.defineProperty(obj,name,desc) 会返回 false）
3）让 Object 操作都变成函数行为（某些 Object 操作是命令式，比如 name in obj 和 delete obj[name]，而 Reflect.has(obj,name) 和 Reflect.deleteProperty(obj,name) 变成了函数行为）
4）Reflect 对象的方法与 Proxy 对象的方法一一对应，只要是 Proxy 对象的方法，就能在 Reflect 对象上找到对应的方法。这就使 Proxy 对象可以方便地调用对应的 Reflect方法来完成默认行为，作为修改行为的基础
```
* **静态方法**：与Proxy对应的13个方法

#### Promise（异步编程、代码冗余）
* **new Promise(function(resolve,reject){})**：
```
1）承诺：对象的状态不受外界影响。Promise 对象代表一个异步操作，有三种状态： Pending(进行中)、Resolved(己成功)、Rejected(己失败)
2）－旦状态改变就不会再变，任何时候都可以得到这个结果
3）无法取消 Promise，一旦新建它就会立即执行，无法中途取消
4）如果不设置回调函数，Promise 内部抛出的错误不会反应到外部
resolve函数的作用：将 Promise 对象的状态从Pending变为Resolved，在异步操作成功时调用，并将异步操作的结果作为参数传递出去
reject函数的作用：将 Promise 对象的状态从Pending变为Rejected，在异步操作失败时调用，并将异步操作报出的错误作为参数传递出去
```
* **Promise.prototype.then()**：为 Promise 实例添加状态改变时的回调函数，返回一个新的 Promise 实例
```
promise.then(Resolved 状态回调函数，Rejected 状态回调函数?)
回调函数可以将另一个promise作为参数，此时promise的状态由另一个promise决定
```
* **Promise.prototype.catch()**：then(null, rejection)的别名，用于指定发生错误时的回调函数，如果在运行中抛出错误，也会被 catch 方法捕获
* **Promise.all([p1,p2...])**：将多个 Promise 实例包装成一个新的 Promise 实例（都成功才成功返回数组，有一个失败就失败返回第一个失败的值）
* **Promise.race([p1,p2...])**：有一个实例率先改变状态，就返回该结果
* **Promise.resolve()**：将现有对象转为 Promise 对象，返回 Promise 实例的状态从生成起就是 Resolved
* **Promise.reject()**：将现有对象转为 Promise 对象，返回 Promise 实例的状态从生成起就是 Rejected

#### Iterator（遍历器）
```
遍历器：是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构，只要部署 Iterator 接口，就可以完成遍历操作
作用：
1）为各种数据结构提供一个统一的、简便的访问接口
2）使得数据结构的成员能够按某种次序排列
3）Iterator 接口主要供 for...of 消费（其他场合：解构赋值、扩展运算符、yield*、Array.from、数组遍历）
原生具备 Iterator 接口（部署了 Symbol.iterator 属性）的数据结构：String、Array、Map、Set、arguments、NodeList、generator
```
* **for...of**：
```
forEach：无法中途跳出
for...in：会以任意顺序遍历键名，以字符串作为键名，包括原型链上的键，适用于对象
for...of:提供了遍历所有数据结构的统一操作接口，可以与 break、continue、return 配合使用
```

#### Generator（异步编程、生成器）
```
状态机：封装了多个内部状态
遍历器对象生成函数：执行 Generator 函数会返回一个遍历器对象
特征：
1）function 命令与函数名之间有一个星号
2）函数体内部使用 yield（产出）语句定义不同的内部状态
3）遇到 yield 语句就暂停执行后面的操作，并将紧跟在 yield 后的表达式的值作为返回的对象的 value 属性值
4）如果没有再遇到新的 yield 语句，就运行到函数结束，直到 return 语句为止，并将 return 语句后面的表达式的值作为返回对象的 value 属性值
5）如果该函数没有 return 语句 ，则返回对象的 value 属性值为 undefined
6）yield 语句本身总是返回 undefined，next 方法可以带有一个参数，该参数会被当作上一条 yield 语句的返回值
应用：
1）异步操作的同步化表达（异步函数回调执行next函数）
2）利用 Generator 函数可以在任意对象上部署 Iterator 接口
3）作为数据结构（看作一个数组结构）
```
* **yield* generator()**：在一个 Generator 函数里面执行另一个 Generator 函数（任何数据结构只要有 Iterator 接口，就可以被 yield* 遍历）
* **异步实现**：
```
回调函数地狱：因为多个异步操作形成了强耦合，只要有一个操作需要修改，它的上层回调函数和下层回调函数就都要跟着修改
协程：多个线程互相协作，完成异步任务
```
* **Thunk函数**：自动执行 Generator 函数的一种方法
    * **参数的求值策略**：传值调用（在进入函数体之前就计算参数的值）、传名调用（直接将表达式传入函数体，只在用到它的时候求值）
    * **Thunk 函数的含义**：它是“传名调用”的一种实现策略，用临时函数（Thunk 函数）替换某个表达式
    * **JavaScript 语言的 Thunk 函数**：“传值调用”的实现，用一个只接受回调函数作为参数的单参数函数（Thunk 函数）替换多参函数
    * **Generator 函数的自动流程管理**：Thunk 函数、回调函数、Promise对象
* **co 模块**：自动执行 Generator 函数的一种方法

#### async（异步编程、Generator 函数的语法糖）
```
async function f(){await ...}
1）内置执行器：自动执行
2）更好的语义：async 表示函数里有异步操作，await 表示紧跟在后面的表达式需要等待结果
3）返回值是 Promise 对象：
    函数内部 return 语句返回的值，会成为 then 方法回调函数的参数
    函数内部抛出错误会导致返回的 Promise 对象变为 reject 状态，抛出的错误对象会被 catch 方法回调函数接收到
    函数返回的 promise 对象必须等到内部所有 await 命令后面的 Promise 对象执行完才会发生状态改变，除非遇到 return 语句或者抛出错误
    只要一个 await 语句后面的 Promise 变为 reject ，那么整个 async 函数都会中断执行。在 try...catch 或者（promise.catch）结构里面，不管这个异步操作是否成功，都不会终止执行
4）await 命令后面是 promise 对象。如果不是，会被转换成 Promise.resolve 对象
```

#### Class（让对象原型的写法更加清晰--语法糖）
```
类的方法（除 constructor 以外）都定义在 prototype 对象上
类的内部定义的所有方法都是不可枚举的
类和模块的内部默认使用严格模式
类不存在变量提升
类的内部可以使用 get、set 关键字对某个属性设置存值函数和取值函数，拦截该属性的存取行为
如果某个方法之前加上星号*，就表示该方法是一个 Generator 函数
constructor：类的默认方法，默认返回实例对象（this），可以指定返回另外一个对象
静态方法：在方法前加上 static 关键字，就表示该方法不会被实例继承，而是直接通过类调用，父类的静态方法可以被子类继承，静态方法也可以从 super 对象上调用
静态属性：指的是 Class 本身的属性，即 Class.propname（Class内部只有静态方法，没有静态属性）或者 static propname = value，而不是定义在实例对象（this)上的属性
实例属性：可以写入类的定义之中 propname = value
new.target：返回 new 命令所作用的构造函数、子类继承父类时 new.target 会返回子类（作用：规定只能用new命令生成实例、不能独立使用而必须继承后才能使用的类）
```
* **Class继承**：extends
```
super()：在子类的 constructor 方法中必须调用，表示父类的构造函数，用来新建父类的 this 对象（只有调用 super 之后才可以使用 this 关键字）
super：在普通方法中指向父类的原型对象，在静态方法中指向父类（内部绑定子类的 this）
使用 super 的时候，必须显式指定是作为函数还是作为对象使用，否则会报错
子类的 _proto_ 属性表示构造函数的继承，总是指向父类
子类 prototype 属性的 _proto_ 属性表示方法的继承，总是指向父类的 prototype 属性
允许继承原生构造函数定义子类
Mixin 模式：将多个类的接口“混入”另一个类
```

#### Decorator(修饰器)
* **类的修饰**：是一个函数，用来修改类的行为（编译时执行的函数）
```
function decorator(target){}：target为要修饰的类
@decorator
class A{}
// 等同于
class A{}
A = decorator(A) || A;
```
* **类的方法的修饰**：是一个函数，用来修改方法的行为（编译时执行的函数）
```
function decorator(target,name,descriptor){}：target为要修饰的目标对象，name为要修饰的属性名，descriptor为该属性的描述对象
```
* **core-decorators.js**：一个第三方模块，提供了几个常见的修饰器（@autobind、@readonly、@override、@deprecate、@suppressWarnings）

#### Module(模块)
```
CommonJS：运行时整体加载、输出的是值的缓存、加载时执行、再加载时会返回第一次运行的结果
Module：编译时按需加载
1）模块自动采用严格模式
2）代码是在模块作用域之中运行，而不是在全局作用域中运行，模块内部的顶层变量是外部不可见的
3）同一个模块如果加载多次，将只执行一次
export：规定模块的对外接口
    动态绑定（通过该接口可以取到模块内部实时的值）
    可以出现在模块的任何位置，只要处于模块顶层
import：输入其他模块提供的功能
    静态执行（不能使用表达式和变量）
    整体加载（即 * as obj 来指定一个对象，所有输出值都加载在这个对象上，不允许改变这个对象的值）
export default：为模块指定默认输出，import加载时可以用任意名称指向默认输出的值且不使用大括号
```
* **Module加载**
```
<script type="module" src="foo.js" ></script> 或 <script type="module" >import * from "foo.js";</script>
异步加载：等到整个页面渲染完再执行模块脚本，等同于defer（可以设置async：加载完成，渲染引擎就会中断渲染，立即执行，执行完成后，再恢复渲染）
Node加载：
    CommonJS模块：module.exports 等同于 export default
    require 命令加载 ES6 模块：模块的所有输出接口都会成为输入对象的属性，default 接口变成了输入对象的 default 属性
循环加载：a脚本的执行依赖b脚本，而b脚本的执行又依赖a脚本
    CommonJS 模块：返回的是当前己经执行的部分的值
    ES6 模块：变量不会被缓存，而是成为一个指向被加载模块的引用
```
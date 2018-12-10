## javascript对象

[Number](#number)、
[String](#string)、
[Array](#array)、
[Boolean](#boolean)、
[Date](#date)、
[Math](#math：执行常见的算数任务)、
[RegExp](#regexp：正则表达式)、
[全局对象](#全局对象)


* 对象属性
    * **constructor**：返回对创建此对象的对象函数的引用
    * **prototype**：使您有能力向对象添加属性和方法
* 对象方法
    * **toSource()**：返回该对象的源代码
    * **valueOf()**：返回对象的原始值

#### Number
* 整数（不使用小数点或指数计数法）最多为 15 位
* 小数的最大位数是 17，但是浮点运算并不总是 100% 准确
```js
var x=9999999999999999; //10000000000000000
var x=0.2+0.1; //0.30000000000000004
x=(0.2*10+0.1*10)/10; //解决方法：0.3
```
* 如果前缀为 0，则 JavaScript 会把数值常量解释为八进制数，如果前缀为 0 和 "x"，则解释为十六进制数
```js
var y=017; //15
var z=0x1F; //31
```
* 对象属性
    * **MAX_VALUE**：可表示的最大的数（1.7976931348623157e+308）
    * **MIN_VALUE**：可表示的最小的数（5e-324）
    * **NaN**：非数字值（使用 isNaN() 来判断一个值是否是数字，NaN 与所有值都不相等，包括它自己）
    * **NEGATIVE_INFINITY**：负无穷大，溢出时返回该值（-Infinity）
    * **POSITIVE_INFINITY**：正无穷大，溢出时返回该值（Infinity）

    **es6**=========================================================================
    * **EPSILON**：表示 1 和比最接近 1 且大于 1 的最小 Number 之间的差别
    * **MIN_SAFE_INTEGER**：表示在 JavaScript中最小的安全的 integer 型数字 (-(253 - 1))
    * **MAX_SAFE_INTEGER**：表示在 JavaScript 中最大的安全整数（253 - 1）
* 对象方法
    * **toFixed(num?)**：把数字转换为字符串，结果的小数点后有指定位数的数字(四舍五入)
    ```js
    //num：0~20之间的整数，默认：0
    new Number(13).toFixed(2) //13.00
    ```
    * **toString(radix?)**：把数字转换为字符串，使用指定的基数
    ```js
    //radix基数：2~36之间的整数，默认基数：10
    13.toString(2) //当调用该方法的对象不是 Number 时抛出 TypeError 异常
    new Number(13).toString(2) //1101
    ```
    * **toLocaleString()**：把数字转换为字符串，使用本地数字格式顺序
    * **toExponential(num)**：把对象的值转换为指数计数法
    ```js
    //num：规定指数计数法中的小数位数，0~20之间的整数，默认：使用尽可能多的数字
    new Number(1000).toExponential(1) //1.0e+4
    ```
    * **toPrecision(num)**：把数字格式化为指定的长度
    ```js
    //num：规定必须被转换为指数计数法的最小位数，1~21之间的整数，默认：调用方法 toString()
    new Nu

    **es6**=========================================================================
    * **isInteger()**：用来判断给定的参数是否为整数
    ```js
    Number.isInteger(10);        // 返回 true
    Number.isInteger(10.5);      // 返回 false
    ```
    * **isSafeInteger()**：判断传入的参数值是否是一个"安全整数"
    ```js
    Number.isSafeInteger(10);    // 返回 true
    Number.isSafeInteger(12345678901234567890);  // 返回 false
    ```mber(1000).toPrecision(4) //1.000e+4
    ```

    **技巧**=========================================================================
    * **数字补0**
    ```js
    const addZero1 = (num, len = 2) => (`0${num}`).slice(-len)
    const addZero2 = (num, len = 2) => (`${num}`).padStart( len   , '0') //es2017:str.padStart(targetLength, padString?)
    addZero1(3) // 03
    addZero2(32,4)  // 0032
    ```

#### String
* String 类定义的方法都不能改变字符串的内容
```js
"Volvo XC60"[2]; //l
new String("abc") // String {0: "a", 1: "b", 2: "c", length: 3}
"John" === new String("John"); //false
typeof "John" // "string"
typeof new String("John") // "object"
String(true) // "true"
String(5) // "5"
```
* 对象属性
    * **length**：返回字符串的长度
* 对象方法
    * **charAt(index)**：返回指定索引位置的字符或空字符串
    ```js
    'abc'.charAt(1); // "b"
    'abc'[1]; // "b"

    'abc'.charAt(-1|3); // ""，参数为负数或大于等于字符串的长度，返回空字符串
    ```
    * **concat(stringX,...,stringX)**：连接两个或多个字符串，返回连接后的字符串
    ```js
    'a'.concat('b') // "ab"
    ''.concat(1, 2, 3) // "123"，如果参数不是字符串，concat方法会将其先转为字符串，然后再连接
    ```
    * **indexOf(searchvalue,fromindex?)**：返回字符串中检索指定字符第一次出现的位置或-1
    ```js
    'hello world'.indexOf('o') // 4
    'JavaScript'.indexOf('script') // -1
    'hello world'.indexOf('o', 6) // 7，第二个参数表示从该位置开始向后匹配
    ```
    * **lastIndexOf(searchvalue,fromindex?)**：返回字符串中检索指定字符最后一次出现的位置或-1
    ```js
    'hello world'.lastIndexOf('o') // 7
    'hello world'.lastIndexOf('o', 6) // 4，第二个参数表示从该位置起向前匹配
    ```
    * **match(searchvalue/regexp)**：找到一个或多个正则表达式的匹配，返回结果数组或null
    ```js
    var str = "bbbabbabb";
    str.match(/a/g) // [ 'a', 'a' ]
    str.match('a') // [ 'a', index: 3, input: 'bbbabbabb' ]
    str.match('c') // null
    ```
    * **search(searchvalue/regexp)**：检索与正则表达式相匹配的值，返回匹配的第一个位置或-1
    ```js
    var str = "bbbabbabb";
    str.search('a') // 3
    str.search('c') // -1
    str.search(/a/g) // 3 //忽略标志 g和regexp的lastindex属性，总是从第一个位置开始匹配
    ```
    * **replace(regexp/substr,replacement)**：替换与正则表达式匹配的子串，返回替换后的字符串
    ```js
    'aaa'.replace('a', 'b') // "baa"
    'aaa'.replace(/a/g, 'b') // "bbb"

    /*replace() 方法的第二个参数可以是函数而不是字符串。
    在这种情况下，每个匹配都调用该函数，它返回的字符串将作为替换文本使用。
    该函数的第一个参数是匹配模式的字符串。
    接下来的参数是与模式中的子表达式匹配的字符串，可以有 0 个或多个这样的参数。
    接下来的参数是一个整数，声明了匹配在 stringObject 中出现的位置。
    最后一个参数是 stringObject 本身。*/
    "Doe, John".replace(/(\w+)\s*, \s*(\w+)/, "$2 $1"); //"John Doe"
    '"a", "b"'.replace(/"([^"]*)"/g, "'$1'"); //"'a', 'b'"
    'aaa bbb ccc'.replace(/\b\w+\b/g, function(word){
        return word.substring(0,1).toUpperCase()+word.substring(1);
    }); //"Aaa Bbb Ccc"
    ```
    * **split(regexp/substr,maxLength?)**：把字符串分割为子字符串数组，返回分割的数组
    ```js
    'a|b|c'.split('|') // ["a", "b", "c"]
    'a|b|c'.split('') // ["a", "|", "b", "|", "c"]
    'a|b|c'.split() // ["a|b|c"]
    'a||c'.split('|') // ['a', '', 'c']
    '|b|c'.split('|') // ["", "b", "c"]
    'a|b|'.split('|') // ["a", "b", ""]

    'a b c'.split(/\s+/) // ["a", "b", "c"]

    'a|b|c'.split('|', 0) // []
    'a|b|c'.split('|', 1) // ["a"]
    'a|b|c'.split('|', 2) // ["a", "b"]
    'a|b|c'.split('|', 3) // ["a", "b", "c"]
    'a|b|c'.split('|', 4) // ["a", "b", "c"] //maxLength只截取不延长
    ```
    * **slice(start,end?)**：提取字符串的片断，并在新的字符串中返回被提取的部分
    ```js
    //第一个参数是子字符串的开始位置，第二个参数是子字符串的结束位置（不含该位置）
    'JavaScript'.slice(0, 4) // "Java"
    //如果省略第二个参数，则表示子字符串一直到原字符串结束
    'JavaScript'.slice(4) // "Script"
    //如果参数是负值，表示从结尾开始倒数计算的位置，即该负值加上字符串长度
    'JavaScript'.slice(-6) // "Script"
    'JavaScript'.slice(0, -6) // "Java"
    'JavaScript'.slice(-2, -1) // "p"
    //如果第二个参数位置小于第一个参数位置，返回空字符串
    'JavaScript'.slice(2, 1) // ""
    ```
    * **substring(start,end?)**：提取字符串中两个指定的索引号之间的字符
    ```js
    //第一个参数是子字符串的开始位置，第二个参数是子字符串的结束位置（不含该位置）
    'JavaScript'.substring(0, 4) // "Java"
    //如果省略第二个参数，则表示子字符串一直到原字符串结束
    'JavaScript'.substring(4) // "Script"
    //如果第二个参数大于第一个参数，substring方法会自动更换两个参数的位置
    'JavaScript'.substring(10, 4) // "Script"
    //如果参数是负数，substring方法会自动将负数转为0
    'Javascript'.substring(-3) // "JavaScript"
    'JavaScript'.substring(4, -3) // "Java"
    ```
    * **substr(start,length?)**：从起始索引号提取字符串中指定数目的字符
    ```js
    //第一个参数是子字符串的开始位置，第二个参数是子字符串的长度
    'JavaScript'.substr(4, 6) // "Script"
    //如果省略第二个参数，则表示子字符串一直到原字符串结束
    'JavaScript'.substr(4) // "Script"
    //如果第一个参数是负数，表示倒数计算的字符位置。如果第二个参数是负数，将被自动转为0，返回空字符串
    'JavaScript'.substr(-6) // "Script"
    'JavaScript'.substr(4, -1) // ""
    ```
    * **trim()**：移除字符串首尾空白
    ```js
    '  hello world  '.trim() // "hello world"
    //该方法去除的不仅是空格，还包括制表符（\t、\v）、换行符（\n）和回车符（\r）
    '\r\nabc \t'.trim() // 'abc'
    ```
    * **toString()**：返回字符串对象值
    * **toLowerCase()**：把字符串转换为小写
    ```js
    'Hello World'.toLowerCase() // "hello world"
    ```
    * **toUpperCase()**：把字符串转换为大写
    ```js
    'Hello World'.toUpperCase() // "HELLO WORLD"
    //toUpperCase或toLowerCase也可以将布尔值或数组转为大或小写字符串，但是需要通过call方法使用
    String.prototype.toUpperCase.call(true) // 'TRUE'
    String.prototype.toUpperCase.call(['a', 'b', 'c']) // 'A,B,C'
    ```
    * **toLocaleLowerCase()**：根据主机的语言环境把字符串转换为小写，只有几种语言（如土耳其语）具有地方特有的大小写映射
    * **toLocaleUpperCase()**：根据主机的语言环境把字符串转换为大写，只有几种语言（如土耳其语）具有地方特有的大小写映射
    * **localeCompare()**：用本地特定的顺序来比较两个字符串
    ```js
    /*返回一个整数，如果小于0，表示第一个字符串小于第二个字符串；
    如果等于0，表示两者相等；如果大于0，表示第一个字符串大于第二个字符串*/
    'apple'.localeCompare('banana') // -1
    //该方法的最大特点，就是会考虑自然语言的顺序。举例来说，正常情况下，大写的英文字母小于小写字母
    'B' > 'a' // false  JavaScript采用的是Unicode码点比较
    'B'.localeCompare('a') // 1  localeCompare方法会考虑自然语言的排序情况
    ```
    * **charCodeAt()**：返回指定索引位置字符的 Unicode 值
    ```js
    'abc'.charCodeAt(1) // 98
    //如果没有任何参数，charCodeAt返回首字符的Unicode码点
    'abc'.charCodeAt() // 97
    //如果参数为负数，或大于等于字符串的长度，charCodeAt返回NaN
    'abc'.charCodeAt(-1) // NaN

    /*charCodeAt方法返回的Unicode码点不大于65536（0xFFFF），也就是说，只返回两个字节的字符的码点。
    如果遇到Unicode码点大于65536的字符，必需连续使用两次charCodeAt，
    不仅读入charCodeAt(i)，还要读入charCodeAt(i+1)，将两个16字节放在一起，才能得到准确的字符。*/
    ```
    * **fromCharCode()**：将指定的 Unicode 值转换为字符串
    ```js
    String.fromCharCode(104, 101, 108, 108, 111) // "hello"

    //该方法不支持Unicode码点大于0xFFFF的字符，即传入的参数不能大于0xFFFF
    String.fromCharCode(0x20BB7) // "ஷ"
    /*上面代码返回字符的编号是0x0BB7，而不是0x20BB7。
    它的根本原因在于，码点大于0xFFFF的字符占用四个字节，而JavaScript只支持两个字节的字符。
    这种情况下，必须把0x20BB7拆成两个字符表示*/
    String.fromCharCode(0xD842, 0xDFB7)// "????"
    /*上面代码中，0x20BB7拆成两个字符0xD842和0xDFB7（即两个两字节字符，合成一个四字节字符），就能得到正确的结果。
    码点大于0xFFFF的字符的四字节表示法，由UTF-16编码方法决定*/
    ```
    * **显示字体**：
    ```js
    document.write("abc".anchor("myanchor")) //创建 HTML 锚，<a name="myanchor">abc</a>
    document.write("abc".big()) //大号字体
    document.write("abc".blink()) //闪动，此方法无法工作于 Internet Explorer 中
    document.write("abc".bold()) //粗体
    document.write("abc".fixed()) //打字机字体
    document.write("abc".fontcolor("Red")) //指定颜色字体
    document.write("abc".fontsize(7)) //指定字体尺寸，参数必须是从 1 至 7 的数字
    document.write("abc".italics()) //斜体
    document.write("abc".link("http://www.w3school.com.cn")) //超链接
    document.write("abc".small()) //小号字体
    document.write("abc".strike()) //添加删除线
    document.write("abc".sub()) //下标
    document.write("abc".sup()) //上标
    ```

#### Array
* 对象属性
    * **length**：设置或返回数组中元素的数目
* 对象方法
    * **concat(arrayX,......,arrayX)**：连接两个或更多的数组，并返回数组
    ```js
    [1,2,3].concat(4,5); //[1,2,3,4,5]
    [1,2,3].concat([4,5]); //[1,2,3,4,5]
    ```
    * **join(separator?)**：把数组的所有元素通过指定的分隔符进行分隔放入一个字符串，返回字符串
    ```js
    [1,2,3].join(); //"1,2,3"
    [1,2,3].join("."); //"1.2.3"
    ```
    * **shift()**：删除并返回数组的第一个元素，空数组不操作并返回undefined
    ```js
    const arr = [1,2,3];
    arr.shift(); //1
    arr; //[2,3]
    ```
    * **pop()**：删除并返回数组的最后一个元素，空数组不操作并返回undefined
    ```js
    const arr = [1,2,3];
    arr.pop(); //3
    arr; //[1,2]
    ```
    * **unshift(newelement1,....,newelementX)**：向数组的开头添加一个或更多元素，并返回新的长度
    ```js
    const arr = [1,2,3];
    arr.unshift(8,9); //5 //IE7 undefined
    arr; //[8,9,1,2,3]
    ```
    * **push(newelement1,....,newelementX)**：向数组的末尾添加一个或更多元素，并返回新的长度
    ```js
    const arr = [1,2,3];
    arr.push(4,5); //5
    arr; //[1,2,3,4,5]
    ```
    * **splice(index,howmany,item1?,.....,itemX?)**：删除元素，并向数组添加新元素
    ```js
    let arr = [1,2,3];
    arr.splice(1); //[2,3]
    arr; //[1]

    arr = [1,2,3];
    arr.slice(1,1); //[2]
    arr; //[1,3]

    arr = [1,2,3];
    arr.slice(-3); //[1,2,3]
    arr; //[]

    arr = [1,2,3];
    arr.slice(-3,2); //[1,2]
    arr; //[3]

    arr = [1,2,3];
    arr.slice(-3,2,"a"); //[1,2]
    arr; //["a",3]
    ```
    * **slice(start,end?)**：从某个已有的数组返回选定的元素
    ```js
    const arr = [1,2,3];
    arr.slice(1); //[2,3]
    arr.slice(1,2); //[2]
    arr.slice(-3); //[1,2,3]
    arr.slice(-3,2); //[1,2]
    arr; //[1,2,3]
    ```
    * **reverse()**：颠倒数组中元素的顺序
    ```js
    const arr = [1,2,3];
    arr.reverse(); //[3,2,1]
    arr; //[3,2,1]
    ```
    * **sort(sortfun?)**：对数组的元素进行排序
    ```js
    const arr = [2,1,3];
    arr.sort(); //[1,2,3]
    arr; //[1,2,3]

    function sortNumber(a,b){
        return a - b
    }
    const arr1 = ["100","5", "25"];
    arr1.sort(); //["100","25", "5"]
    arr1.sort(sortNumber); //["5","25", "100"]
    ```
    * **toString()**：把数组转换为字符串，并返回结果
    ```js
    [1,2,3].toString(); //1,2,3
    {a:1}.toString(); //[object Object]
    ```
    * **toLocaleString()**：把数组转换为本地字符串，并返回结果
    ```js
    const arr = [1,2,3];
    arr.toLocaleString(); //1,2,3
    arr; //[1,2,3]
    ```

    **技巧**============================================================================
    * **过滤数组中的所有假值**
    ```js
    const compact = arr => arr.filter(Boolean)
    compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34])  //[ 1, 2, 3, 'a', 's', 34 ]
    ```

#### Boolean
* false：0、-0、null、""、false、undefined、NaN
* 对象方法
    * **toString()**：把逻辑值转换为字符串，并返回"true" 或 "false"
    ```js
    new Boolean(NaN).toString(); //"false"
    ```

#### Date
* 日期对象也可用于比较两个日期
* 对象方法
    * **Date()**：返回当日的日期和时间
    * **getDate()**：从 Date 对象返回一个月中的某一天 (1 ~ 31)
    * **getDay()**：从 Date 对象返回一周中的某一天 (0 ~ 6)
    * **getMonth()**：从 Date 对象返回月份 (0 ~ 11)
    * **getFullYear()**：从 Date 对象以四位数字返回年份
    * **getHours()**：返回 Date 对象的小时 (0 ~ 23)
    * **getMinutes()**：返回 Date 对象的分钟 (0 ~ 59)
    * **getSeconds()**：返回 Date 对象的秒数 (0 ~ 59)
    * **getMilliseconds()**：返回 Date 对象的毫秒(0 ~ 999)
    * **getTime()**：返回 1970 年 1 月 1 日至今的毫秒数
    * **parse()**：返回1970年1月1日午夜到指定日期（字符串）的毫秒数
    * **setDate()**：设置 Date 对象中月的某一天 (1 ~ 31)
    * **setMonth()**：设置 Date 对象中月份 (0 ~ 11)
    * **setFullYear()**：设置 Date 对象中的年份（四位数字）
    * **setHours()**：设置 Date 对象中的小时 (0 ~ 23)
    * **setMinutes()**：设置 Date 对象中的分钟 (0 ~ 59)
    * **setSeconds()**：设置 Date 对象中的秒钟 (0 ~ 59)
    * **setMilliseconds()**：设置 Date 对象中的毫秒 (0 ~ 999)
    * **setTime()**：以毫秒设置 Date 对象
    * **toDateString()**：把 Date 对象的日期部分转换为字符串
    * **toTimeString()**：把 Date 对象的时间部分转换为字符串
    * **toString()**：把 Date 对象转换为字符串

#### Math：执行常见的算数任务
* 对象属性
    * **E**：返回算术常量 e，即自然对数的底数（约等于2.718）
    * **LN2**：返回 2 的自然对数（约等于0.693）
    * **LN10**：返回 10 的自然对数（约等于2.302）
    * **LOG2E**：返回以 2 为底的 e 的对数（约等于 1.414）
    * **LOG10E**：返回以 10 为底的 e 的对数（约等于0.434）
    * **PI**：返回圆周率（约等于3.14159）
    * **SQRT1_2**：返回返回 2 的平方根的倒数（约等于 0.707）
    * **SQRT2**：返回 2 的平方根（约等于 1.414）
* 对象方法
    * **ceil(x)**：对数进行上舍入（返回大于等于 x最接近的整数）
    * **floor(x)**：对数进行下舍入（返回小于等于 x最接近的整数）
    * **round(x)**：把数四舍五入为最接近的整数
    * **abs(x)**：返回数的绝对值
    * **max(x,y)**：返回 x 和 y 中的最高值
    * **min(x,y)**：返回 x 和 y 中的最低值
    * **random()**：返回 0 ~ 1 之间的随机数
    * **sqrt(x)**：返回数的平方根
    * **acos(x)**：返回数的反余弦值
    * **asin(x)**：返回数的反正弦值
    * **atan(x)**：以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值
    * **atan2(y,x)**：返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）
    * **cos(x)**：返回数的余弦
    * **exp(x)**：返回 e 的指数
    * **log(x)**：返回数的自然对数（底为e）
    * **pow(x,y)**：返回 x 的 y 次幂
    * **sin(x)**：返回数的正弦
    * **tan(x)**：返回角的正切

    **技巧**============================================================================
    * **精确到指定位数的小数**
    ```js
    const round = (n, decimals = 0) => Number(`${Math.round(`${n}e${decimals}`)}e-${decimals}`)
    round(1.345, 2) // 1.35
    round(1.345, 1) // 1.3
    ```

#### RegExp：正则表达式
```js
//pattern 是一个字符串，指定了正则表达式的模式或其他正则表达式
//attributes 是一个可选的字符串，包含属性修饰符 "g"（全局匹配）、"i"（不区分大小写匹配） 和 "m"（多行匹配）
//如果 pattern 是正则表达式，而不是字符串，则必须省略 attributes 参数
new RegExp(pattern, attributes);
```
> **方括号**：用于查找某个范围内的字符
    >> [abc]：查找方括号之间的任何字符

    >> ^abc ：查找任何不在方括号之间的字符

    >> [0-9]：查找任何从 0 至 9 的数字

    >> [a-z]：查找任何从小写 a 到小写 z 的字符

    >> [A-Z]：查找任何从大写 A 到大写 Z 的字符

    >> [A-z]：查找任何从大写 A 到小写 z 的字符

    >> (red|blue|green)：查找任何指定的选项

    >> [\u4E00-\uFA29]|[\uE7C7-\uE7F3]：中文

    >> [\-]：特殊字符 - 需要转义

> **元字符**：有特殊含义的字符
    >> .：查找单个字符，除了换行和行结束符

    >> \w：查找单词字符（A-z0-9）

    >> \W：查找非单词字符

    >> \d：查找数字（0-9）

    >> \D：查找非数字字符

    >> \s：查找空白字符

    >> \S：查找非空白字符

    >> \b：匹配单词边界

    >> \B：匹配非单词边界

    >> \0：查找 NUL 字符

    >> \n：查找换行符

    >> \f：查找换页符

    >> \r：查找回车符

    >> \t：查找制表符

    >> \v：查找垂直制表符

    >> \xxx：查找以八进制数 xxx 规定的字符

    >> \xdd：查找以十六进制数 dd 规定的字符

    >> \uxxxx：查找以十六进制数 xxxx 规定的 Unicode 字符

> **量词**
    >> n+：匹配任何包含至少一个 n 的字符串

    >> n*：匹配任何包含零个或多个 n 的字符串

    >> n?：匹配任何包含零个或一个 n 的字符串

    >> n{X}：匹配包含 X 个 n 的序列的字符串

    >> n{X,Y}：匹配包含 X 至 Y 个 n 的序列的字符串

    >> n{X,}：匹配包含至少 X 个 n 的序列的字符串

    >> n$：匹配任何结尾为 n 的字符串

    >> ^n：匹配任何开头为 n 的字符串

    >> ?=n：匹配任何其后紧接指定字符串 n 的字符串

    >> ?!n：匹配任何其后没有紧接指定字符串 n 的字符串

* 对象属性：
    * **lastIndex**：一个整数，标示开始下一次匹配的字符位置
    ```js
    //不具有标志 g 和不表示全局模式的 RegExp 对象不能使用 lastIndex 属性
    //如果在成功地匹配了某个字符串之后就开始检索另一个新的字符串，需要手动地把这个属性设置为 0
    ```
    * **global**：RegExp 对象是否具有标志 g
    * **ignoreCase**：RegExp 对象是否具有标志 i
    * **multiline**：RegExp 对象是否具有标志 m
    * **source**：正则表达式的源文本
* 对象方法：
    * **compile(regexp,modifier)**：编译正则表达式
    ```js
    //regexp：正则表达式，modifier：g|i|gi

    var str="Every man in the world! Every woman1 on earth!";
    const patt=/man/g;
    str.replace(patt,"person"); //Every person in the world! Every woperson on earth!
    patt.compile(/(wo)?man/g);
    str.replace(patt,"person"); //Every person in the world! Every person on earth!
    ```
    * **exec(string)**：检索字符串中指定的值。返回结果数组或null
    ```js
    var str = "bbbabbabb";
    var patt = new RegExp("a","g"); //全局匹配
    patt.exec(str) //[ 'a', index: 3, input: 'bbbabbabb' ]
    patt.lastIndex //4
    patt.exec(str) //[ 'a', index: 6, input: 'bbbabbabb' ]
    patt.lastIndex //7
    patt.exec(str) //null
    patt.lastIndex //0

    patt = new RegExp("a"); //非全局匹配
    patt.exec(str) //[ 'a', index: 3, input: 'bbbabbabb' ]
    patt.lastIndex //0
    ```
    * **test(string)**：检索字符串中指定的值。返回 true 或 false
    ```js
    var str = "bbbabbabb";
    var patt = new RegExp("a","g"); //全局匹配
    patt.test(str) //true
    patt.lastIndex //4
    patt.exec(str) //true
    patt.lastIndex //7
    patt.exec(str) //false
    patt.lastIndex //0

    patt = new RegExp("a"); //非全局匹配
    patt.exec(str) //true
    patt.lastIndex //0
    ```

#### 全局对象
* 全局函数：
    * **isNaN(x)**：检查某个数字是否是NaN
    ```js
    isNaN(5-2) //false
    isNaN("Hello") //true
    ```
    * **parseInt(string, radix?)**：指定基数解析一个字符串并返回一个整数
    ```js
    parseInt("19",10) //19 (10+9)
    parseInt("11",2) //3 (2+1)
    parseInt("17",8) //15 (8+7)
    parseInt("1f",16) //31 (16+15)

    parseInt(" 19 ") //19，开头和结尾的空格是允许的
    parseInt("19a11") //19，只有字符串中的第一个数字会被返回
    parseInt("a19") //NaN，字符串的第一个字符不能被转换为数字

    //radix 的值为 0，或没有设置该参数时，parseInt() 会根据 string 来判断数字的基数
    parseInt("10") //10，1 ~ 9 的数字开头解析为十进制的整数
    parseInt("0x10") //16，"0x" 开头解析为十六进制的整数
    parseInt("010") //未定：10 或 8，"0" 开头解析为八进制或十六进制的数字
    ```
    * **parseFloat(string)**：解析一个字符串并返回一个浮点数
    ```js
    parseFloat(" 19 ") //19，开头和结尾的空格是允许的
    parseFloat("19a11") //19，只有字符串中的第一个数字会被返回
    parseFloat("a19") //NaN，字符串的第一个字符不能被转换为数字
    parseFloat("10.00") //10
    parseFloat("-10.13") //-10.13
    parseFloat("314e-2") //3.14
    ```
    * **Number(object)**：把对象的值转换为数字
    ```js
    Number(new Date()) //1539846443589，返回从 1970 年 1 月 1 日至今的毫秒数
    Number("8 9") //NaN，对象的值无法转换为数字
    Number(true|false) //1|0
    Number([]) //0
    Number([20]) //20
    Number(null|"") //0
    ```
    * **String(object)**：把对象的值转换为字符串
    ```js
    String(new Date()) //"Thu Oct 18 2018 15:23:09 GMT+0800 (中国标准时间)"
    String(true|false) //"true"|"false"
    String("8 9") //"8 9"
    String(123) //"123"
    ```
    * **eval(string)**：计算 JavaScript 字符串，并把它作为脚本代码来执行
    ```js
    eval("x=10;y=20;document.write(x*y)") //200
    eval("2+3") //5
    ```
    * **isFinite(number)**：检查某个值是否为有穷大的数
    ```js
    isFinite(5-2) //true
    isFinite(-Infinity) //false
    isFinite(NaN) //false
    isFinite("abc") //false
    ```
    * **encodeURI(URIstring)**：把字符串编码为 URI
    ```js
    encodeURI("http://www.w3school.com.cn/My first/") //"http://www.w3school.com.cn/My%20first/"
    ```
    * **decodeURI(URIstring)**：解码某个编码的 URI
    ```js
    decodeURI("http://www.w3school.com.cn/My%20first/") //"http://www.w3school.com.cn/My first/"
    ```
    * **encodeURIComponent(URIstring)**：把字符串编码为 URI 组件
    ```js
    encodeURIComponent("http://www.w3school.com.cn/p 1/") //"http%3A%2F%2Fwww.w3school.com.cn%2Fp%201%2F"
    encodeURIComponent(",/?:@&=+$#") //"%2C%2F%3F%3A%40%26%3D%2B%24%23"
    ```
    * **decodeURIComponent()**：	解码一个编码的 URI 组件
    * **escape()**：对字符串进行编码
    * **unescape()**：对由 escape() 编码的字符串进行解码
    * **getClass()**：返回一个 JavaObject 的 JavaClass
* 全局属性：
    * **NaN**：指示某个值是不是数字值
    * **undefined**：指示未定义的值
    * **Infinity**：代表正的无穷大的数值
    * **java**：代表 java.* 包层级的一个 JavaPackage
    * **Packages**：根 JavaPackage 对象

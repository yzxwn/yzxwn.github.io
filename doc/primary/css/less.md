## less

[原文](http://lesscss.org)

[原文：中文](http://lesscss.cn/)

#### 变量
```less
//可应用于选择器名称，属性名称，URL和@import语句
//变量是延迟加载的，不必在使用之前声明
@nice-blue: #5B83AD;
#header {
  color: @light-blue;
}
```
#### Extend：继承
```less
//匹配多个 .e:extend(.f, .g) {}
//匹配嵌套 .e:extend(ul li) {}
nav ul {
  &:extend(.inline);
}
.inline {
  color: red;
}
//等于
.inline,
nav ul {
  color: red;
}
//.a:extend(.b all) {}
.a.b.test,
.test.c {
  color: orange;
}
.test {
  &:hover {
    color: green;
  }
}
.replacement:extend(.test all) {}
//等于
.a.b.test,
.test.c,
.a.b.replacement,
.replacement.c {
  color: orange;
}
.test:hover,
.replacement:hover {
  color: green;
}
```
#### Mixins：混合
```less
.my-mixin {
  color: black;
}
.my-other-mixin(@color: red) {//可传参，可设置默认值
  background: @color;
}
.class {
  .my-mixin;
  .my-other-mixin(white);//或者.my-other-mixin(@color: white)
}
//等于
.my-mixin {
  color: black;
}
.class {
  color: black;
  background: white;
}
//@arguments
.box-shadow(@x: 0; @y: 0; @blur: 1px; @color: #000) {
  -webkit-box-shadow: @arguments;
     -moz-box-shadow: @arguments;
          box-shadow: @arguments;
}
.big-block {
  .box-shadow(2px; 5px);
}
//等于
.big-block {
  -webkit-box-shadow: 2px 5px 1px #000;
     -moz-box-shadow: 2px 5px 1px #000;
          box-shadow: 2px 5px 1px #000;
}
//可变数量的参数
.mixin(@a: 1; ...) {}
//模式匹配：参数值
.mixin(dark; @color) {
  color: darken(@color, 10%);
}
.mixin(light; @color) {
  color: lighten(@color, 10%);
}
.mixin(@_; @color) {
  display: block;
}
.class {
  .mixin(light; #888);
}
//模式匹配：参数个数
.mixin(@a) {
  color: @a;
}
.mixin(@a; @b) {
  color: fade(@a; @b);
}
```
#### Mixins：函数
```less
//变量、函数作为返回值
.mixin() {
  @size: in-mixin;
  @definedOnlyInMixin: in-mixin;
  .doSomething() {
      declaration: 5;
    }
}

.class {
  margin: @size @definedOnlyInMixin;
  .mixin();
}
@size: globaly-defined-value;
//等于
.class {
  margin: in-mixin in-mixin;
  declaration: 5;
}
```
#### Mixins：规则集
```less
//变量包含css属性集合
@detached-ruleset: { background: red; };
.top {
    @detached-ruleset();
}
//等于
.top {
  background: red;
}
```
#### Mixins：条件
```less
//关键字：when
.mixin (@a) when (lightness(@a) >= 50%) {
  background-color: black;
}
.mixin (@a) when (lightness(@a) < 50%) {
  background-color: white;
}
.mixin (@a) {
  color: @a;
}
.class1 { .mixin(#ddd) }
.class2 { .mixin(#555) }
//等于
.class1 {
  background-color: black;
  color: #ddd;
}
.class2 {
  background-color: white;
  color: #555;
}
//关键字：and
.mixin (@a) when (isnumber(@a)) and (@a > 0) { ... }
//等于
.mixin (@a) when (@a > 10), (@a < -10) { ... }
//关键字：not
.mixin (@b) when not (@b > 0) { ... }
//is函数
/*
基本类型：iscolor、isnumber、isstring、iskeyword、isurl
特定单位：ispixel、ispercentage、isem、isunit
*/
.mixin (@a; @b: 0) when (isnumber(@b)) { ... }
.mixin (@a; @b: black) when (iscolor(@b)) { ... }
//default函数可用于根据其他混合匹配进行混合匹配，您可以使用它来创建类似于else或default语句（分别为if和case结构）的“条件混合”
.mixin (@a) when (@a > 0) { ...  }
.mixin (@a) when (default()) { ... }
```
#### Mixins：Guard表达式
```less
button when (@my-option = true) {
  color: white;
}
& when (@my-option = true) {
  button {
    color: white;
  }
  a {
    color: blue;
  }
}
//递归循环
.generate-columns(4);
.generate-columns(@n, @i: 1) when (@i =< @n) {
  .column-@{i} {
    width: (@i * 100% / @n);
  }
  .generate-columns(@n, (@i + 1));
}
```
#### Mixins：合并
```less
//+
.mixin() {
  box-shadow+: inset 0 0 10px #555;
}
.myclass {
  .mixin();
  box-shadow+: 0 0 20px black;
}
//等于
.myclass {
  box-shadow: inset 0 0 10px #555, 0 0 20px black;
}
//+_
.mixin() {
  transform+_: scale(2);
}
.myclass {
  .mixin();
  transform+_: rotate(15deg);
}
//等于
.myclass {
  transform: scale(2) rotate(15deg);
}
```
#### @import
```less
//扩展：@import (keyword) "filename"允许多个：@import (keyword，keyword) "filename"
/*
reference：使用Less文件但不输出
inline：在输出中包含源文件但不处理它
less：无论文件扩展名是什么，都将文件视为Less文件
css：无论文件扩展名是什么，都将文件视为CSS文件
once：只包含一次文件（这是默认行为）
multiple：多次包含该文件
optional：找不到文件时继续编译
*/
```
#### 内置函数
* **逻辑函数**
    * **if((condition), value1, value2)**：根据条件返回两个值中的一个
    * **boolean(condition)**：评估为真或假
* **字符串函数**
    * **escape(string)**：将字符串中的特殊字符用URL编码转换后返回
    * **e(string)**：按原样返回其内容，但不带引号。可以用于输出CSS值，该值不是有效的CSS语法，或者使用Less无法识别的专有语法
    * **%(string, arguments ...)**：格式化带占位符的字符串
    ```less
    format-a-d: %("repetitions: %a file: %d", 1 + 2, "directory/file.less");
    format-a-d-upper: %('repetitions: %A file: %D', 1 + 2, "directory/file.less");
    format-s: %("repetitions: %s file: %s", 1 + 2, "directory/file.less");
    format-s-upper: %('repetitions: %S file: %S', 1 + 2, "directory/file.less");
    //等于
    format-a-d: "repetitions: 3 file: "directory/file.less"";
    format-a-d-upper: "repetitions: 3 file: %22directory%2Ffile.less%22";
    format-s: "repetitions: 3 file: directory/file.less";
    format-s-upper: "repetitions: 3 file: directory%2Ffile.less";
    ```
    * **replace(string, pattern, replacement, flags?)**：替换字符串中的文本
    ```less
    replace("Hello, Mars?", "Mars\?", "Earth!");
    replace("One + one = 4", "one", "2", "gi");
    replace('This is a string.', "(string)\.$", "new $1.");
    replace(~"bar-1", '1', '2');
    //等于
    "Hello, Earth!";
    "2 + 2 = 4";
    'This is a new string.';
    bar-2;
    ```
* **列表函数**
    * **length(list)**：返回列表中的元素数
    ```less
    //list：逗号或空格分隔的值列表
    @list: "banana", "tomato", "potato", "peach";
    n: length(@list);
    //等于
    n: 4;
    ```
    * **extract(list, index)**：返回列表中指定位置的值（index从1开始）
    * **range(start?, end, step?)**：生成跨越一系列值的列表
    ```less
    value: range(4); //value: 1 2 3 4;
    value: range(10px, 30px, 10); //value: 10px 20px 30px;
    ```
    * **each(list, mixin)**：将mixin绑定到列表的每个成员
    ```less
    @selectors: blue, green, red;
    each(@selectors, {
      .sel-@{value}- @{key}-@{index} {
        a: b;
      }
    });
    //等于
    .sel-blue-one-1 {
      a: b;
    }
    .sel-green-two-2 {
      a: b;
    }
    .sel-red-three-3 {
      a: b;
    }
    //
    .set-2() {
      one: blue;
      two: green;
      three: red;
    }
    .set-2 {
      each(.set-2(), .(@v, @k, @i) {
        @{k}-@{i}: @v;
      });
    }
    //等于
    .set-2 {
      one-1: blue;
      two-2: green;
      three-3: red;
    }
    ```
* **数学函数**
    * **ceil(number)**：向上取整
    * **floor(number)**：向下取整
    * **round(number, decimalPlaces)**：四舍五入按照指定舍入的小数位数
    * **percentage(number)**：将浮点数转换为百分比字符串
    * **min(value1, ..., valueN)**：返回一个或多个值中的最小值
    * **max(value1, ..., valueN)**：返回一个或多个值中的最高值
    * **sqrt(number)**：计算数字的平方根。保持单位不变
    * **abs(number)**：计算数字的绝对值。保持单位不变
    * **sin(number)**：计算正弦函数
    * **asin(number)**：正弦反函数
    * **cos(number)**：计算余弦函数
    * **acos(number)**：余弦的倒数
    * **tan(number)**：计算切线函数
    * **atan(number)**：反正切函数
    * **pi()**：返回π（pi）
    * **pow(number, number)**：返回第一个参数的值，该值是第二个参数的幂
    * **mod(number, number)**：返回第一个参数模数第二个参数的值
* **类型函数**
    * **isnumber(value)**：1, 5px, 7.8%
    * **isstring(value)**："string"
    * **iscolor(value)**：#ff0, blue
    * **iskeyword(value)**：keyword
    * **isurl(value)**：url(...)
    * **ispixel(value)**：56px
    * **isem(value)**：7.8em
    * **ispercentage(value)**：7.8%
    * **isunit(value, unit)**：值是指定单位的数字
    * **isruleset(value)**：值是规则集
* **杂项函数**
    * **color(string)**：将表示颜色的字符串变为颜色
    * **image-size(string)**：从文件中获取图像尺寸
    * **image-width(string)**：从文件中获取图像宽度
    * **image-height(string)**：从文件中获取图像高度
    * **convert(number, identifier)**：将数字从一个单位转换为另一个单位
    ```less
    convert(9s, "ms") //9000ms
    convert(14cm, mm) //140mm
    convert(8, mm) //8
    ```
    * **data-uri(mimetype?, url)**：url()如果ieCompat选项打开且资源太大，或者在浏览器中使用该函数，则内联资源并回退。如果未给出MIME类型，则node使用mime包来确定正确的mime类型
    * **default()**：仅在保护条件内可用，并且true仅在没有其他mixin匹配时返回，false否则返回
    * **unit(dimension, unit?)**：删除或更改数字的单位
    * **get-unit(number)**：返回数字的单位
    * **svg-gradient(escaped, list/color, color, color...)**：生成多站svg渐变
    ```less
    div {
      @list: red, green 30%, blue;
      background-image: svg-gradient(to right, @list);
    }
    //等于
    div {
      background-image: svg-gradient(to right, red, green 30%, blue);
    }
    //等于（生成的背景图像左侧为红色，绿色为其宽度的30％，以蓝色结束）
    div {
      background-image: url('data:image/svg+xml,%3C%3Fxml%20version%3D%221.0%22%20%3F%3E%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20version%3D%221.1%22%20width%3D%22100%25%22%20height%3D%22100%25%22%20viewBox%3D%220%200%201%201%22%20preserveAspectRatio%3D%22none%22%3E%3ClinearGradient%20id%3D%22gradient%22%20gradientUnits%3D%22userSpaceOnUse%22%20x1%3D%220%25%22%20y1%3D%220%25%22%20x2%3D%22100%25%22%20y2%3D%220%25%22%3E%3Cstop%20offset%3D%220%25%22%20stop-color%3D%22%23ff0000%22%2F%3E%3Cstop%20offset%3D%2230%25%22%20stop-color%3D%22%23008000%22%2F%3E%3Cstop%20offset%3D%22100%25%22%20stop-color%3D%22%230000ff%22%2F%3E%3C%2FlinearGradient%3E%3Crect%20x%3D%220%22%20y%3D%220%22%20width%3D%221%22%20height%3D%221%22%20fill%3D%22url(%23gradient)%22%20%2F%3E%3C%2Fsvg%3E');
    }
    ```
* **颜色定义函数**
    * **rgb()**：
    * **rgba()**：
    * **argb()**：
    * **hsl()**：
    * **hsla()**：
    * **hsv()**：
    * **hsva()**：
* **颜色通道函数**
    * **hue()**：
    * **saturation()**：
    * **lightness()**：
    * **hsvhue()**：
    * **hsvsaturation()**：
    * **hsvvalue()**：
    * **red()**：
    * **green()**：
    * **blue()**：
    * **alpha()**：
    * **luma()**：
    * **luminance()**：
* **颜色操作函数**
    * **saturate()**：
    * **desaturate()**：
    * **lighten()**：
    * **darken()**：
    * **fadein()**：
    * **fadeout()**：
    * **fade()**：
    * **spin()**：
    * **mix()**：
    * **tint()**：
    * **shade()**：
    * **greyscale()**：
    * **contrast()**：
* **颜色混合函数**
    * **multiply()**：
    * **screen()**：
    * **overlay()**：
    * **softlight()**：
    * **hardlight()**：
    * **difference()**：
    * **exclusion()**：
    * **average()**：
    * **negation()**：
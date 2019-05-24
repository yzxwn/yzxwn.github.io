## css扩展

* [css权重](#css权重)
* [水平垂直居中](#水平垂直居中)
* [盒模型](#盒模型)
* [响应式布局](#响应式布局)


[css](https://juejin.im/tag/CSS)


#### css权重
* 权重规则：
```
!important 优先级最高，但也会被权重高的important所覆盖
行内样式总会覆盖外部样式表的任何样式(除了!important)
单独使用一个选择器的时候，不能跨等级使css规则生效
如果两个权重不同的选择器作用在同一元素上，权重值高的css规则生效
如果两个相同权重的选择器作用在同一元素上：以后面出现的选择器为最后规则.
权重相同时，与元素距离近的选择器生效
```
* 权重等级：
```
!important;
行内样式;
ID选择器, 权重:100;
class,属性选择器和伪类选择器，权重:10;
标签选择器和伪元素选择器，权重:1;
```
* 等级关系：**!important>行内样式>ID选择器 > 类选择器 | 属性选择器 | 伪类选择器 > 元素选择器**


#### 水平垂直居中
```css
.parent{
display:flex;
display: -webkit-flex;
justify-content:center;
align-items:center;
}
-------------------
.parent{
display:flex;//或者display: grid;
display: -webkit-flex;
}
.children{
margin: auto;
}
-------------------
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
-webkit-transform: translate(-50%, -50%);
----------------------
//行内元素水平居中（inline、inline-block、inline-table、inline-flex）
.parent{//在父容器设置
    text-align:center;
}
//块级元素水平居中
1）.child{
    width: 100px;//确保该块级元素定宽
    margin:0 auto;
}
2）.child {
    display: table;//在表现上类似block元素，但是宽度为内容宽
    margin: 0 auto;
  }
//单行内联元素垂直居中
#box {
   height: 120px;
   line-height: 120px;
}
//多行内联元素垂直居中
.parent {
    display: table;
}
.child {
    display: table-cell;
    vertical-align: middle;
}
//块级元素垂直居中
.parent {
    display: table-cell;
    vertical-align: middle;
}
```

#### 盒模型
```
W3C 标准盒模型：content
IE 盒模型：content+padding+border
box-sizing：默认content-box
FC（Formatting Context）：视觉格式化模型，用来描述盒子布局规则
```
* **BFC:block**
```
布局规则：
1）内部的盒子会在垂直方向，一个个地放置
2）BFC是页面上的一个隔离的独立容器
3）属于同一个BFC的 两个相邻Box的 上下margin会发生重叠
4）计算BFC的高度时，浮动元素也参与计算
5）每个元素的margin box的左边，与包含块border box的左边相接触，即使存在浮动也是如此
6）BFC的区域不会与float盒子重叠
作用：
1）阻止元素被浮动元素覆盖
2）可以包含浮动元素（清除内部浮动）
3）分属于不同的BFC时可以阻止margin重叠
4）自适应两列布局
触发条件：
1）html根元素
2）float的值不为none
3）overflow的值不为visible
4）position的值为absolute、fixed
5）display的值为inline-block、table-cell、table-caption
```
* **IFC:inline**
```
布局规则：
1）框会从包含块的顶部开始，一个接一个地水平摆放
2）摆放这些框时，它们在水平方向的 内外边距+边框 所占用的空间都会被考虑； 在垂直方向上，这些框可能会以不同形式来对齐： 水平的margin、padding、border有效，垂直无效。不能指定宽高;
3）行框的宽度是 由包含块和存在的浮动来决定; 行框的高度至少会高到足以包含他内部的所有框
4）当一行上的行级总宽度（某一个小框的宽度或者若干个小框的总宽度）小于行宽的时候，他们在行宽内的水平方向上的排布由text-align决定
5）当一个行内框的宽度超过了该行的行宽的时候，就会被分成几个框。但是如果设置这个框就不能被分割的话（white-space：nowrap）那么这时候该行内框就会溢出该行的行宽
6）一般情况下行宽的左边紧贴在他的包含块的左边，同样他的右边也是紧贴在其包含块的右边。但是也不一定，比如出现浮动的话，浮动元素可能会插在包含块和行框之间
7）计算行框内各个框的高度，对于非替换元素就是起line-height,而对于替换元素就是边界框的高度了。 行框的高是最顶端框的顶边到最底端框的底边的距离
触发条件：
1）input、a、img、span
2）display的值为inline-block
```
* **FFC:flex**
    * [原文](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
    * 块级元素display: flex; 行内元素display: inline-flex;
    * 兼容：加上-webkit前缀
    * **容器的属性**
    ```
    flex-direction：决定主轴的方向
        row（默认：从左到右） | row-reverse（从右到左） | column（从上到下） | column-reverse（从下到上）
    flex-wrap：如何换行
        nowrap（默认：不换行） | wrap（换行，第一行在上方） | wrap-reverse（换行，第一行在下方）
    flex-flow：flex-direction属性和flex-wrap属性的简写形式
        row nowrap（默认）
    justify-content：定义项目在主轴上（水平方向）的对齐方式
        flex-start（默认：左对齐） | flex-end（右对齐） | center（居中） | space-between（两端对齐，项目之间的间隔都相等） | space-around（每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍）
    align-items：定义项目在交叉轴上（垂直方向）的对齐方式
        stretch（默认：如果项目未设置高度或设为auto，将占满整个容器的高度） | flex-start（上对齐） | flex-end（下对齐） | center（居中） | baseline（项目的第一行文字的基线对齐）
    align-content：定义多根轴线（多行）的对齐方式
        stretch（默认：轴线占满整个交叉轴） | flex-start（上对齐） | flex-end（下对齐） | center（居中） | space-between（两端对齐，轴线之间的间隔平均分布） | space-around（每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍）
    ```
    * **项目的属性**
    ```
    order：定义项目的排列顺序。数值越小，排列越靠前，默认为0
    flex-grow：定义项目的放大比例。默认为0，即如果存在剩余空间，也不放大
    flex-shrink：定义项目的缩小比例。默认为1，即如果空间不足，该项目将缩小
    flex-basis：定义了在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
    flex：flex-grow、flex-shrink、flex-basis的简写
    快捷值：auto (1 1 auto)， none (0 0 auto)
    align-self：允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch
        auto | flex-start | flex-end | center | baseline | stretch
    ```
* **GFC:gridLayout**
```
触发条件：display的值为grid
```

#### 响应式布局
```
rem：相对于（html）根元素的字体大小的单位
```
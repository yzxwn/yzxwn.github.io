## css技巧

* [伸缩布局（flex）](#伸缩布局（flex）)
* [水平垂直居中](#水平垂直居中)
* [文字省略号](#文字省略号)

#### 伸缩布局（flex）
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

#### 水平垂直居中
```css
.parent{
display:flex;
display: -webkit-flex;
justify-content:center;
align-items:center;
}
-------------------
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
 -webkit-transform: translate(-50%, -50%);
```

#### 文字省略号
```
// css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
width: 60px;
```
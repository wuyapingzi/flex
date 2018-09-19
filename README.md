# flex
布局的传统解决方案，基于盒状模型，依赖display属性+position属性+float属性。它对于特殊的布局非常不方便，比如垂直居中就不容易实现。2009年w3c提出了一种新的方案--flex布局，可以渐变、完整、响应式的实现各种页面布局，目前，它已经得到了所有浏览器的支持。
# 一、Flex布局是什么？
Flex是Flexible Box的缩写，意为“弹性布局”，用来为盒状模型提供最大的灵活性。任何一个容器都可以指定为Flex布局。
```
.box{
  display: flex
}
```
行内元素也可以使用Flex布局
```
.inline-box{
  display: inline-flex
}
```
### 注意，设置为Flex布局以后，子元素的float、clear和vertical-align属性都将失效。
# 二、基本概念
采用flex布局的元素成为flex容器，它所有的子元素自动成为容器成员，称为flex项目。

容器默认存在两根轴，水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴开始的位置（与边框的交叉点）叫做main start，结束位置叫做main end，交叉轴开始的位置叫做cross start，结束位置叫做 cross end。

项目默认沿主轴排列，单个项目占据主轴空间叫做main size ，占据的交叉轴空间叫做cross size。
# 三、容器的属性
### 3.1 flex-direction属性
```
.box{
  flex-direction: row | row-reverse | column | column-reverse;
}
row（默认值）：主轴为水平方向，起点在左端。
 row-reverse ：主轴为水平方向，起点在右端。
 column ： 主轴为垂直方向，起点在上沿。
 column-reverse ：主轴为垂直方向，起点在下沿。
```
### 3.2 flex-wrap属性
默认情况下，flex项目都排在一条线上，flex-wrap属性定义，如果一条轴线排不下，如何换行。
```
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
nowrap（默认） ：不换行
wrap ：换行，第一行在上方
wrap-reverse ：换行，第一行在下方
```
### 3.3 flex-flow属性
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
```
.box{
  flex-flow: <flex-direction> || <flex-wrap>
}
```
### 3.4 justify-content属性
justify-content属性定义了项目在主轴方向上的对齐方式。
```
.box{
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
flex-start（默认值） ：左对齐
flex-end ：右对齐
center ：居中
space-between ：两端对齐，项目之间的间隔相等
space-around ：每个项目两侧间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```
### 3.5 align-items属性
align-items属性定义项目在交叉轴上如何对齐。
```
.box{
  align-items: flex-start | flex-end | center | baseline | stretch
}
flex-start ：交叉轴的起点对齐
flex-end ：交叉轴的终点对齐
center ：交叉轴的中点对齐
baseline ：项目第一行文字的基线对齐
stretch ：如果项目没有设置高度或者设为auto，将占满整个容器的高度。
```
### 3.6 align-content属性
align-content属性定义了多根轴线的对齐方式，如果项目只有一根轴线，改属性不起作用。
```
.box{
  align-content: flex-start | flex-end | center | space-between | space-around | stretch
}
flex-start ：与交叉轴起点对齐
flex-end ：与交叉轴终点对齐
center ：与交叉轴中点对齐
space-between ：与交叉轴两端对齐，轴线之间的间隔平均分配
space-around ：每根轴线两侧的间隔相等，所以轴线之间的间隔比轴线与边框的间隔大一倍
stretch ：轴线占满整个交叉轴
```
# 四、项目的属性
### 4.1 order属性
order属性定义项目的排列顺序。数值越小排列越靠前，默认值为0
```
.item{
  order: <integer>; /*default 0*/
}
```
### 4.2flex-grow属性
flex-grow属性定义项目的放大比例，默认值为0，即如果存在剩余空间，也不放大
```
.item{
  flex-grow: <integer>; /*default 0*/
}
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间比其他项目多一倍。
```
### 4.3 flex-shrink属性
flex-shrink属性定义了项目的缩小比例，默认值为1，即如果空间不足，该项目将缩小
```
.item{
  flex-shrink: <number> /*default 1*/
}
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。
```
### 4.4 flex-basis属性
flex-basis属性定义了分配多余空间之前，项目占据的主轴空间，浏览器根据这个属性计算主轴是否有多余空间，它的默认值为auto，即项目的本来大小。
```
.item{
  flex-basis: <length> | auto /*default auto*/
}
它可以设置为width 或者height 属性一样的值（比如350px），则项目将占据固定空间。
```
### 4.5 flex属性
flex属性是flex-grow属性，flex-shrink属性和flex-basis属性的简写，默认值为0 1 auto
```
.item{
  flex: none | [<flex-grow> <flex-shrink>? || <flex-basis>]
}
该属性有两个快捷键值： auto(1 1 auto)和none(0 0 auto)，建议先使用这个属性，而不是单独写三个分离属性，因为浏览器会推算相关值
```
### 4.6 align-self属性
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
```
.item{
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```



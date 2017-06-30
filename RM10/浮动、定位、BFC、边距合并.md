## 浮动元素有什么特征？对父容器、其他浮动元素、普通元素、文字分别有什么影响? 
浮动元素脱离文档流。根据``` float ``` 属性的值而左右移动，直到它的外边缘碰到包含框或者另一个风动元素的框的边缘才停止移动。
**对父容器的影响：**子元素浮动会导致父容器高度塌陷。
**对其他浮动元素的影响：**如果包含块太窄无法容纳水平排列的全部浮动元素，那么其它浮动元素会向下移动，直到有足够的空间，而如果浮动元素的高度不同，那么向下移动的时候可能会被卡住。
**对普通元素的影响：**由于浮动元素脱离了文档流，普通元素会对视浮动元素视而不见不见，占据浮动元素原有的位置，但会被浮动元素遮罩。
**对文字影响：**浮动样式最初设计便是用于设置文字环绕效果，如今也一样，文字会对浮动元素流出空间，环绕它

## 清除浮动指什么? 如何清除浮动? 列出两种以上方法
**清除浮动：**使父容器恢复原来的样子，其他元素也不再受浮动元素影响
- **方案一(推荐)：**
```
.clearfix:after{
    centent:"";//内容随意设置
    height:0;//高度为0，可以换成line-height:0
    display:block;//将文本转为块级元素
    visibility:hidden;//将元素隐藏
    clear:both//清除浮动
}
.clearfix{
    zoom:1;//兼容IE
}
```
- **方案二（定位局限性较强）：**
```
.clearfix{
    overflow:hidden;//父元素创建BFC
    zoom:1;
}
```
- **方案三（浪费标签）：**
```
<div style="clear:both;"></div>//直接在需要清楚浮动的地方创建一个清楚浮动的标签
```
[参考：CSS float浮动的深入研究-张鑫旭](http://www.zhangxinxu.com/wordpress/?p=594)

## 有几种定位方式，分别是如何实现定位的，参考点是什么，使用场景是什么？z-index 有什么作用? 如何使用?
[DEMO-TEST](http://js.jirengu.com/hoxejolopa/5/edit)
1. ```position: relative;```相对定位，
参考点：自身原来的位置，原位置在文档流中占位； 
使用场景：相对于自身位置进行偏移；为后代固定定位元素设定参照物；
2. ```position: absolute;```绝对定位，
参考点：根元素或者相对定位的父元素
使用场景：使元素相对于参照物固定位置，脱离文档流
3. ```position: fixed;```绝对定位
参考点：视窗
使用场景：使元素固定在视窗固定位置，脱离文档流

**z-index:**绝对定位的元素脱离了普通流，所以绝对定位的元素可以覆盖页面上的其它元，设置z-index属性控制叠放顺序，值越高，元素位置越靠上。
![z-index](http://image.zhangxinxu.com/image/blog/200912/z-index.jpg)

## position:relative和负margin都可以使元素位置发生偏移?二者有什么区别
position:relative;相对自己原本位置偏移，不影响其它普通流中元素的位置。
margin：偏移时候影响其它普通流中的元素。

## BFC 是什么？如何生成 BFC？BFC 有什么作用？举例说明
**BFC：**BlockFormattingContent（块级格式化上下文）
浮动、绝对定位（绝对定位、固定定位）元素、块级容器（如inline-block、 table-cell、table-caption）并不是块级盒子，还包括哪些overflow属性值取值visible以外的块级盒子，会为它们的内容物创建一个新的块级格式化上下文。
**生成BFC：**
```
float: left | right;
overflow: hidden | auto | scroll;
display: table-cell | table-caption | inline-block;
position: absolute | fixed;
```
**BFC作用：**
（1） 解决margin重叠问题。所谓margin重叠是指处于同一个BFC的相邻元素、嵌套元素，只要它们之间没有阻挡（如：边框、非空内容、padding等）就会发生margin重叠。这是只要让其中一个元素生成新的BFC就能解决margin重叠问题。
（2） 清除浮动。因为BFC可以包含浮动，所以让父容器生成新的BFC可以让父容器在视觉上包围了浮动的子元素，因而清除了浮动。

## 在什么场景下会出现外边距合并？如何不让相邻元素外边距合并？给个父子外边距合并的范例
（1）两个垂直外边距相遇或一个空元素有上下外边距时，会发生外边距合并。合并后外边距的长度为合并前外边距较大的那个长度
（2）
 - 使元素形成BFC；
 - 父子间：添加 ``` border ``` 或 ``` padding； ``` ；设置 ``` display: inline-block；```
 - 使元素 ``` float ``` 浮动
 - 设置属性 ``` overflow: hidden; ```
（3）父子元素间没有阻挡（如：border、非content、padding等）
[DEMO-父子元素外边距合并](http://js.jirengu.com/tafomasebu/2/edit)

## 代码

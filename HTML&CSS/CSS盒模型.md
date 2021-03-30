## 盒模型的基本认识

下图是W3C规范中的配图，从图中可以看出

- 每个盒子都有一个内容区域`content`，周围由`padding`, `border`,`margin`区域构成。
- 周围的区域是可选的，分别由`padding`,` border`,`margin`属性控制，这几个属性可以分到`top`, `right`,`bottom`,`left`四个方向上。
- 影响盒子内容区域的尺寸的有：
  - 生成盒子的元素是否设置了`width`和`height`属性；
  - 盒子是否包含文本或其他盒子；
  - 盒子是否是表格等。
- 外边距`margin`区域始终是透明的。
- 除外边距意外的区域的背景样式由`background`属性决定。

![盒模型](https://www.w3.org/TR/CSS2/images/boxdim.png)

## 标准盒模型和IE盒模型有什么区别

区别：两种盒模型的主要区别是计算盒子宽度和高度的方式不一样，

- w3c标准盒模型：`盒子宽度/高度 = width/height + padding + border`；
- IE盒模型：`盒子宽度/高度 = width/height = 内容宽度/高度+padding + border`;

## 怎么切换两种盒模型

CSS3中新增加了`box-sizing`属性来控制盒模型的类型：

- `box-sizing`属性默认取值`content-box`即标准盒模型；
- 将`box-sizing`设置为`border-box`,则采用IE盒模型。

## 获取盒模型的宽高有哪些方式

- `element.stle.width/height`,这种方式**只能取到行内样式的宽高**，`style`标签和`link`外链的取不到。
- `element.getBoundingClientRect().width/height`,获取的是渲染后的宽度和高度，IE9及以上支持，还可获取相对视窗的`left`,`top`,`right`,`bottom`的值。
- `window.getComputedStyle(element).width/height`,获取的是渲染后的宽度和高度，IE9及以上支持。
- `element.currentStyle.width/height`,获取的是渲染后的宽度和高度，**只有IE支持**。

## 参考

- [box dimensions](https://www.w3.org/TR/CSS2/box.html#box-dimensions)
- [css盒模型介绍](https://segmentfault.com/a/1190000013069516?utm_source=sf-similar-article)
- [Introduction to the CSS basic box model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)


## BFC的定义

MDN上是这样定义的：**块格式化上下文（Block Formatting Context，BFC）** 是Web页面的可视CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。

## BFC有哪些特性

- 在一个BFC内部，元素是由上而下一个接着一个排列的，元素之间的间距有margin决定。
- 在同一个BFC中相邻的块级元素在垂直方向会发生[边距折叠](https://www.yuque.com/baige-yid0a/qqvsy2/ez4bd1)。
- BFC是一个独立的容器，内外的元素不会相互影响。
- BFC能够包含浮动元素，计算高度的时候，浮动元素也参与计算。
- BFC区域不会和浮动区域发生重叠。
- 在一个BFC中每个元素的左边缘与容器块元素的左边缘接触。如果是从右往左格式化，则右边缘接触。

## 如何创建BFC

- 根元素或者包含根元素的元素。
- 浮动元素，`float: left | right |inhert`,不是`none`。
- 绝对定位元素，`position: absolute | fixed`。
- `display: inline-block | table-cell | table-caption | flow-root`的元素。
- display为`flex | inline-flex | grid | inline-grid`的元素的直接子元素。
- overflow计算值为`hidden | auto | scroll`不为`visible`的元素。
- 多列容器，元素的`column-count`或`column-width`不为`auto`，包括`column-count`为1。
- `column-span`为`all`的元素始终会创建一个新的BFC。
- 匿名表格单元格元素（元素的[`display`为 `table`,`table-row`、 `table-row-group`,`table-header-group`,`table-footer-group`（分别是HTML table、row、tbody、thead、tfoot 的默认属性）或 `inline-table`）

## BFC有什么应用

**清除浮动**

- 浮动元素会脱离文档流，导致无法计算准确的高度，为了能够计算准确的高度，需要**清除浮动**。更多清除浮动的知识可参考：**[清除浮动](https://www.yuque.com/baige-yid0a/qqvsy2/lu15w2)**。

<img src="https://cdn.nlark.com/yuque/0/2021/png/2743865/1617017807724-5a94a51b-a738-4dcc-a957-29ba65e23265.png" alt="clear" style="zoom:67%;" />

```html
<style>
    .container {
        background: rgb(30, 210, 30);
        border: 1px solid #000;
        width: 150px;
        overflow: hidden; // clear float
    }

    .child {
        float: left;
        width: 50px;
        height: 50px;
        margin: 10px;
        background: rgb(210, 30, 30);
    }
</style>

<div class="container">
    <div class="child"></div>
    <div class="child"></div>
</div>
```

在上面的例子中，如果父元素不设置`overflow: hidden`,结果如左边的图，父元素无法被撑开，通过设置`overflow`来创建`BFC`,从而清除浮动的影响，结果如右边的图，父元素被撑开。

**避免边距折叠**

边距折叠的知识请参考：**[边距折叠](https://www.yuque.com/baige-yid0a/qqvsy2/ez4bd1)**

<img src="https://cdn.nlark.com/yuque/0/2021/png/2743865/1617018517624-54a38bd5-c6a4-4388-ac78-0e94326e5bae.png" alt="image.png" style="zoom:67%;" />

```html
<style>
    .container {
        margin: 10px;
        width: 150px;
        background: rgb(30, 210, 30);
        /* overflow: hidden; */
    }

    .child {
        width: 50px;
        height: 50px;
        margin: 20px;
        background: rgb(210, 30, 30);
    }
</style>

<div class="container">
    <div class="child"></div>
    <div class="child"></div>
</div>
```

上面的例子，左图中父元素与子元素在`margin-bottm`和`margin-top`均发生了边距折叠现象，通过给父元素设置`overflow:hidden`创建`BFC`避免折叠，结果如右图，父元素的内容包含了子元素的`margin`。

## 参考

- [block fotmating contexts](https://www.w3.org/TR/2011/REC-CSS2-20110607/visuren.html#block-formatting)
- [CSS BFC特性](https://segmentfault.com/a/1190000017969917)
- [前端面试-BFC](https://juejin.cn/post/6844903480801525773)
- [块级格式化上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)


## 什么是hasLayout

hasLayout是IE浏览器渲染引擎的一个内部实现，在IE浏览器中，一个元素可以自己计算大小和组织内容，也可以依赖父元素来计算大小和组织内容，为了区分这两种情况，渲染引起采用hasLayout属性实现。当一个元素的hasLayout为true，这个元素便拥有了一个布局layout，该元素不依赖祖先元素进行渲染，它会自己对自己和子孙元素进行布局，这也意味着要花更多的代价来维护自身和相关的内容；当为false的时候，会依赖于某个祖先元素进行布局，这也造成了很多IE的Bug。

## 默认触发hasLayout的元素

- `html、body`
- `table、tr、th、td`
- `img`
- `hr`
- `input`、`button`、`file`、`select`、`textarea`、`fieldset`
- `marquee`
- `frameset`、`frame`、`iframe`
- `objects`、`applets`、`embed`

## 那些CSS会触发hasLayout

- `position: absolute`(IE5+)
- `float: left|right`(IE5+)
- `display: inline-block`(IE5+)
- `width|height: “auto”`以外的任何值(IE5+; 只对block元素有效)
- `zoom: “normal”`以外的任何值(IE5.5+; IE私有属性)
- `writing-mode: tb-rl`(IE5+; IE私有属性)
- `overflow: hidden|scroll|auto`(IE7; 此属性在IE6及更早版本中不能应用在未触发hasLayout的元素上)
- `overflow-x|-y: hidden|scroll|auto`(IE7; 此属性在IE6及更早版本中不触发hasLayout; 此属性在CSS3中才获支持)
- `position: fixed`(IE7)
- `min-width: 任何值`(IE7; 即使是0)
- `max-width: “none”`以外的任何值*(IE7)
- `min-height: 任何值`(IE7)
- `max-height: “none”`以外的任何值*(IE7)
- `position: fixed`(IE7)

## 那些CSS会清除hasLayout

- `position: static`(IE5+)
- `float: none`(IE5+)
- `display: “inline-block”`以外的任何值(IE5+)
- `width|height: “auto”`(IE5+; 对inline元素无效)
- `zoom: “normal”`(IE5.5+; IE私有属性)
- `writing-mode: 从’tb-rl’到’lr-tb’`(IE5+; IE私有属性)
- `max-width|max-height: “none”`(IE7)
- `overflow: visible`(IE7)

## hasLayout的应用

- [清除浮动](https://www.yuque.com/baige-yid0a/qqvsy2/lu15w2),浮动元素可以被layout元素包含，利用这个特点，可以清除IE(6-7)浏览器下的浮动。

## hasLayout造成的问题

- IE6 及更低版本的双空白边浮动 bug, 修复方案: display:inline;
- IE5-6的 3 像素偏移 bug, 修复方案: _height:1%;
- IE6 的躲躲猫(peek-a-boo) bug, 修复方案: _height:1%;
- IE6-7负margin隐藏Bug, 修复方案: 去掉父元素的hasLayout; 或者赋hasLayout给子元素, 并添加position:relative;

>hasLayout 功能只存在于**IE7及低版本**的浏览器上, IE8中已删除 hasLayout 功能.
>hasLayout 触发后, 没有办法直接设置 hasLayout=false, 只有将那些触发 hasLayout 的 css 属性去除, 才能恢复原样.

## 参考：

- [详解IE7以下独有的hasLayout](https://louiszhai.github.io/2016/03/31/css-hasLayout/)
- [hasLayout详解](https://www.cnblogs.com/xiaohuochai/p/4845314.html)
\[TOC\]

\# 水平

\#\# 它是inline或者inline-\*元素（如文本或链接）吗？

你可以在块级父元素中水平居中inline或者inline-\*元素：

\`\`\`

父元素中的CSS样式：

text-align: center;

他的子元素\(inline或者inline-\*元素\)会水平居中

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/HulzB\](http://codepen.io/chriscoyier/pen/HulzB\)\)

适用于inline, inline-block, inline-table, inline-flex等。

\#\# 它是block元素吗？

你可以给block元素的margin-left和margin-right样式定义auto（需要定义width，否则会充满父元素）。通常这样写：

\`\`\`

在需要居中的元素里定义

.center-me {

margin: 0 auto;

}

此时相对父元素水平居中

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/eszon\](http://codepen.io/chriscoyier/pen/eszon\)\)

无论什么宽度的block元素都会以父元素水平居中。

注意，你不能float将一个元素放到中心。\[有一个诡计\]\([https://css-tricks.com/float-center/\)（伪类）。](https://css-tricks.com/float-center/%29（伪类）。)

\#\# 是否有多个block元素?

如果你有两个或更多的block元素需要在一行中水平居中。这里有一个inline-block例子和一个flexbox例子：

\`\`\`

inline-block例子

.inline-block-center {

text-align: center;

}

首先父元素设置样式让子元素水平居中

.inline-block-center div {

display: inline-block;

text-align: left;

}

然后子元素转为inline-blick类型让子元素有宽度高度特性又具有inline的同行特性，使得多个元素在一行相对父元素水平居中。

缺点：inline-blick如果他们高度不一，会以最高的块底部对齐。

flexbox例子

.flex-center {

display: flex;

justify-content: center;

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/ebing\](http://codepen.io/chriscoyier/pen/ebing\)\)

\[block，inline和inlinke-block\]\([http://www.cnblogs.com/KeithWang/p/3139517.html\](http://www.cnblogs.com/KeithWang/p/3139517.html\)\)  这篇文章有一句错了，正确的是inline元素的margin和padding属性竖直方向也都是有效的。

Flex布局是未来布局的首选，缺点是它不支持IE10以下等游览器。

Flex 布局教程：\[语法篇\]\([http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm\_source=tuicool\](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool\)\)

Flex 布局教程：\[实例篇\]\([http://www.ruanyifeng.com/blog/2015/07/flex-examples.html\](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html\)\)

如果不需要多个block元素在一行，这种方法可以让上下多点空隙并且水平居中：

\`\`\`

margin: 5px auto;

\`\`\`

注意设置宽度

\[例子\]\([http://codepen.io/chriscoyier/pen/haCGt\](http://codepen.io/chriscoyier/pen/haCGt\)\)

\# 垂直

垂直居中在CSS中有点棘手。

\#\# 它是inline或者inline-\*元素（如文本或链接）吗？

\#\#\# 是单行吗？

有时，inline/text元素可能显示为垂直居中，只是因为它们之上和之下有相等的填充。

\`\`\`

.link {

padding-top: 30px;

padding-bottom: 30px;

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/ldcwq\](http://codepen.io/chriscoyier/pen/ldcwq\)\)

如果padding由于某种原因不能用，并且你试图居中一些你知道多大的文本，有一个技巧使文本line-height的高度与元素高度相等。

\`\`\`

.center-text-trick {

height: 100px;

line-height: 100px;

}

\`\`\`

将行高和放置文本容器的高度一样，就能实现垂直居中。

\[例子\]\([http://codepen.io/chriscoyier/pen/LxHmK\](http://codepen.io/chriscoyier/pen/LxHmK\)\)

\#\#\# 是多行吗？

顶部和底部的相等填充也可以为多行文本提供垂直居中效果，但是如果这不起作用，也许文本所在的元素可能是表单元格，或者字面上还是表现得像一个CSS。在这种情况下，用\[vertical-align\]\([https://css-tricks.com/almanac/properties/v/vertical-align/\)属性处理，它通常是连续处理元素的对齐。（\[更多\]\(https://css-tricks.com/what-is-vertical-align/\)。）](https://css-tricks.com/almanac/properties/v/vertical-align/%29属性处理，它通常是连续处理元素的对齐。（[更多]%28https://css-tricks.com/what-is-vertical-align/%29。）)

\`\`\`

vertical-align: middle;

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/ekoFx\](http://codepen.io/chriscoyier/pen/ekoFx\)\)

也许你可以使用flexbox？单个flex-child可以很容易地在flex-parent中居中。

\`\`\`

.flex-center-vertically {

display: flex;

justify-content: center;

flex-direction: column;

height: 400px;

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/uHygv\](http://codepen.io/chriscoyier/pen/uHygv\)\)

请记住，只有父容器有固定高度（px，％等），这才是真正相关的，这就是为什么这里的容器有一个高度。

如果这两种方法都没用，你可以使用“ghost element”技术，其中一个全高度的伪元素被放置在容器内，文本与它垂直对齐。

\`\`\`

.ghost-center {

position: relative;

}

.ghost-center::before {

content: " ";

display: inline-block;

height: 100%;

width: 1%;

vertical-align: middle;

}

.ghost-center p {

display: inline-block;

vertical-align: middle;

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/ofwgD\](http://codepen.io/chriscoyier/pen/ofwgD\)\)

\#\# 它是block元素吗？

\#\#\# 你知道元素的高度吗？

不知道网页布局中的高度这是很常见的，有很多原因：如果宽度改变，文本回流可以改变高度。文本样式中的方差可以更改高度。文本量的变化可以改变高度。具有固定宽高比的元素（如图像）可以在调整大小时更改高度。等等。

但如果你知道高度，你可以像这样垂直居中：

\`\`\`

.parent {

position: relative;

}

.child {

position: absolute;

top: 50%;

height: 100px;

margin-top: -50px; /\* 如果不使用 box-sizing: border-box; \*/

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/HiydJ\](http://codepen.io/chriscoyier/pen/HiydJ\)\)

知道高度了，通过margin-top进行微调实现垂直居中。

\#\#\# 你未知元素的高度吗？

\`\`\`

.parent {

position: relative;

}

.child {

position: absolute;

top: 50%;

transform: translateY\(-50%\);

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/uHygv\](http://codepen.io/chriscoyier/pen/uHygv\)\)

逻辑是砍了父元素一半，在砍自己一半实现居中。

\#\#\# 可以使用flexbox吗？

这在flexbox中容易多了。

\`\`\`

.parent {

display: flex;

flex-direction: column;

justify-content: center;

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/FqDyi\](http://codepen.io/chriscoyier/pen/FqDyi\)\)

两个微妙的属性，旋转盒子+水平居中。还可以直接垂直居中：

\`\`\`

display: flex;

align-items: center;

\`\`\`

\# 水平和垂直

您可以以任何方式组合上述方法，以实现完全居中。一般分为三个阵营：

\#\# 是固定宽度和高度的元素吗？

使用等于宽度和高度一半的负边距，在您已将其定位在50％/ 50％之后，再通过margin来居中：

\`\`\`

.parent {

position: relative;

}

.child {

width: 300px;

height: 100px;

padding: 20px;

position: absolute;

top: 50%;

left: 50%;

margin: -70px 0 0 -170px;

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/JGofm\](http://codepen.io/chriscoyier/pen/JGofm\)\)

\#\# 是未知宽度和高度的元素吗？

如果您不知道宽度或高度，可以使用transform属性和向中心的两个方向（基于元素的当前宽度/高度）的50％的负向平移：

\`\`\`

.parent {

position: relative;

}

.child {

position: absolute;

top: 50%;

left: 50%;

transform: translate\(-50%, -50%\);

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/lgFiq\](http://codepen.io/chriscoyier/pen/lgFiq\)\)

\#\# 你可以使用flexbox吗？

要使用flexbox在两个方向居中，您需要使用两个居中属性：

\`\`\`

.parent {

display: flex;

justify-content: center;

align-items: center;

}

\`\`\`

\[例子\]\([http://codepen.io/chriscoyier/pen/msItD\](http://codepen.io/chriscoyier/pen/msItD\)\)

\# 结论

你可以在CSS中完全居中所有的东西。

&gt; 欢迎补充！

&gt; 清除浮动防溢出就不介绍了，还有很多居中场景遇到了在继续补充。


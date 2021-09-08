CSS中有个重要的概念BFC，搞懂BFC可以让我们理解CSS中某些原本诡异(??)的地方。

## 1. 简介

在解释BFC之前，先说一下文档流。我们常说的文档流其实分为**定位流**、**浮动流**、**普通流**三种。而普通流其实就是指BFC中的FC。FC(Formatting Context)，直译过来是格式化上下文，它是页面中的一块渲染区域，有一套渲染规则，决定了其子元素如何布局，以及和其他元素之间的关系和作用。常见的FC有BFC、IFC，还有GFC和FFC。

**BFC**(Block Formatting Context)块级格式化上下文，是用于布局块级盒子的一块渲染区域。[MDN上的解释](https://link.segmentfault.com/?url=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FGuide%2FCSS%2FBlock_formatting_context)：BFC是Web页面 CSS 视觉渲染的一部分，用于决定块盒子的布局及浮动相互影响范围的一个区域。

注意：一个BFC的范围包含创建该上下文元素的所有子元素，但**不包括**创建了新BFC的子元素的内部元素。这从另一方角度说明，一个元素不能同时存在于两个BFC中。因为如果一个元素能够同时处于两个BFC中，那么就意味着这个元素能与两个BFC中的元素发生作用，就违反了BFC的隔离作用。

## 2. 三种文档流的定位方案

**常规流(Normal flow)**

- 在常规流中，盒一个接着一个排列;
- 在块级格式化上下文里面， 它们竖着排列；
- 在行内格式化上下文里面， 它们横着排列;
- 当position为static或relative，并且float为none时会触发常规流；
- 对于静态定位(static positioning)，position: static，盒的位置是常规流布局里的位置；
- 对于相对定位(relative positioning)，position: relative，盒偏移位置由top、bottom、left、right属性定义。即使有偏移，仍然保留原有的位置，其它常规流不能占用这个位置。

**浮动(Floats)**

- 左浮动元素尽量靠左、靠上，右浮动同理
- 这导致常规流环绕在它的周边，除非设置 clear 属性
- 浮动元素不会影响块级元素的布局
- 但浮动元素会影响行内元素的布局，让其围绕在自己周围，撑大父级元素，从而间接影响块级元素布局
- 最高点不会超过当前行的最高点、它前面的浮动元素的最高点
- 不超过它的包含块，除非元素本身已经比包含块更宽
- 行内元素出现在左浮动元素的右边和右浮动元素的左边，左浮动元素的左边和右浮动元素的右边是不会摆放浮动元素的

**绝对定位(Absolute positioning)**

- 绝对定位方案，盒从常规流中被移除，不影响常规流的布局；
- 它的定位相对于它的包含块，相关CSS属性：top、bottom、left、right；
- 如果元素的属性position为absolute或fixed，它是绝对定位元素；
- 对于position: absolute，元素定位将相对于上级元素中最近的一个relative、fixed、absolute，如果没有则相对于body；

## 3. BFC触发方式

1. 根元素，即HTML标签
2. 浮动元素：float值为`left`、`right`
3. overflow值不为 visible，为 `auto`、`scroll`、`hidden`
4. display值为 `inline-block`、`table-cell`、`table-caption`、`table`、`inline-table`、`flex`、`inline-flex`、`grid`、`inline-grid`
5. 定位元素：position值为 `absolute`、`fixed`

**注意：**display:table也可以生成BFC的原因在于Table会默认生成一个匿名的table-cell，是这个匿名的table-cell生成了BFC。

## 4. 约束规则

浏览器对BFC区域的约束规则：

1. 生成BFC元素的子元素会一个接一个的放置。
2. 垂直方向上他们的起点是一个包含块的顶部，两个相邻子元素之间的垂直距离取决于元素的margin特性。在BFC中相邻的块级元素的[外边距会折叠(Mastering margin collapsing)](https://link.segmentfault.com/?url=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FCSS%2FCSS_Box_Model%2FMastering_margin_collapsing)。
3. 生成BFC元素的子元素中，每一个子元素左外边距与包含块的左边界相接触（对于从右到左的格式化，右外边距接触右边界），即使浮动元素也是如此（尽管子元素的内容区域会由于浮动而压缩），除非这个子元素也创建了一个新的BFC（如它自身也是一个浮动元素）。

规则解读：

1. 内部的Box会在垂直方向上一个接一个的放置
2. 内部的Box垂直方向上的距离由margin决定。（完整的说法是：属于同一个BFC的两个相邻Box的margin会发生折叠，不同BFC不会发生折叠。）
3. 每个元素的左外边距与包含块的左边界相接触（从左向右），即使浮动元素也是如此。（这说明BFC中子元素不会超出他的包含块，而position为absolute的元素可以超出他的包含块边界）
4. BFC的区域不会与float的元素区域重叠
5. 计算BFC的高度时，浮动子元素也参与计算

## 5. 作用

BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面元素，反之亦然。我们可以利用BFC的这个特性来做很多事。

### 5.1 阻止元素被浮动元素覆盖

一个正常文档流的block元素可能被一个float元素覆盖，挤占正常文档流，因此可以设置一个元素的float、display、position值等方式触发BFC，以阻止被浮动盒子覆盖。

[使用BFC阻止元素被浮动元素覆盖](https://codepen.io/SHERlocked93/pen/pazdzB)点击预览

### 5.2 可以包含浮动元素

通过改变包含浮动子元素的父盒子的属性值，触发BFC，以此来包含子元素的浮动盒子。

[使用BFC包含浮动元素](https://codepen.io/SHERlocked93/pen/OQLOqG)点击预览

注意，这里触发BFC并不能阻止其它形式的脱离文档流的元素覆盖正常流元素。

[BFC内部其他形式脱离文档流(absolute fixed)](https://codepen.io/SHERlocked93/pen/MQjZPG)点击预览

### 5.3 阻止因为浏览器因为四舍五入造成的多列布局换行的情况

有时候因为多列布局采用小数点位的width导致因为浏览器因为四舍五入造成的换行的情况，可以在最后一列触发BFC的形式来阻止换行的发生。比如下面栗子的特殊情况

[使用BFC阻止多列布局最后一列换行](https://codepen.io/SHERlocked93/pen/yvVOvG)点击预览

### 5.4 阻止相邻元素的margin合并

属于同一个BFC的两个相邻块级子元素的上下margin会发生重叠，(设置writing-mode:tb-rl时，水平margin会发生重叠)。所以当两个相邻块级子元素分属于不同的BFC时可以阻止margin重叠。
这里给任一个相邻块级盒子的外面包一个div，通过改变此div的属性使两个原盒子分属于两个不同的BFC，以此来阻止margin重叠。

[使用BFC阻止margin合并](https://codepen.io/SHERlocked93/pen/eVOevN)点击预览

但是这里有个[疑问](https://codepen.io/SHERlocked93/pen/VQZrxQ)点击预览：
如果外面包一层div，设置能触发BFC的任何属性都能阻止相邻元素的margin合并。因为分属不同BFC不会发生margin合并。
而如果在外面不包一个div的话，当设置display为inline-block、inline-flex、table-captain，和position为absolute、fixed，float为left、right是可以阻止margin合并的。这里问题来了：

我们知道设置position和float会让元素脱离文档流并且又创建新的BFC，所以两个元素就不是相邻元素了，因此可以阻止相邻元素margin合并，但是inline-block、inline-flex、inline-grid、table-captain为什么可以呢？如果有人知道为什么，请告知~

------

网上的帖子大多深浅不一，甚至有些前后矛盾，在下的文章都是学习过程中的总结，如果发现错误，欢迎留言指出~
## css世界备忘录



用 tab 能选中的就是 焦点元素 可以通过设置 tabindex 设置选择顺序

块级元素 和 display 的 block 不是一个概念

清除浮动可以给伪元素如 after display 为块级 然后 clear：both

IE 浏览器的伪元素不能设置为 list-item (不常用)

元素分为内外盒子

display block 内外都是块级 inline-block 外内联内块级 inline 内外都是内联

元素的宽高是作用在内盒子上的

width:auto 有四种情况

​	充分利用可利用的 如 div

​	包裹到合适 如 span

​	收缩到最小 容易出现在table-layout为auto的表格 表现大致是 每行都只有一个字 

​	超长容器限制 内容很长的连续英文和数字 或者被设置了不换行

内部尺寸由内部元素决定 以上四种只有第一个宽度是由外部尺寸决定



##### 鑫三无准则: 无宽度 无图片 无浮动

position 为 absolute 或 fixed 的元素 宽度默认是包裹性的 但同时设置left right 这种对立性的属性 就会格式化宽度 由他定位的父元素决定



button 元素 就是一个inline-block 的好例子  具有包裹性 会自动换行

但 input 的 button 不行 因为 input 的 white-space 默认是 pre 要重置为 normal 才能自动换行

 

##### 文字少居中 文字多居左

外部容器设置为 text-align center

放文字的标签 设置为 inline-block 然后  text-align 为left



首选最小宽度为 东亚文字为每个字的宽度

西方文字为连续的英文字母 一般终止与 空格 短横线 问号 等非字母

#### css 流体布局下 宽度分离原则

宽度最后和margin padding border 等不要同时设置 可以嵌套一层（这样可维护性强，不用每次都计算）

 达到的效果和 border-box差不多

但是 border-box 的设计初衷是为了解决 input，textarea等文本元素自适应父元素



绝对定位的元素的宽高百分比计算是按padding-box来的



max-*默认是none 而min-*默认是auto

min-width 优先 于 max-width 优先于 width！important

高度不定的任意元素展开动画 可以通过设置 max-height 来实现（将max-h设置为比实际尺寸大即可）

​	例：收起时max-height:0 展开max-height: 2000px 

 

内联元素的内联指的是外盒子内联

（止 前三章杂记）

#### 第四章 盒尺寸四大家族


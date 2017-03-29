# BOOTSTRAP使用之旅
这里记录了在一无所知的情况下使用Bootstrap的历程。

## 缘起
YY表示，最近Bootstrap很火，于是想借助这个玩意儿来美化界面。

## Card
看到Card这个组件，觉得可以用在我们闪电心算的界面上。所以动手开始。

### 如何将一个Card铺满全屏？
将`<html>`、`<body>`及`.card`都加入`height: 100%;`。这样，`.card-header`和`.card-footer`占据一头一尾，而`.card-block`会填满屏幕中间。

### 如何将`.card-block`中的文字水平垂直居中？
1. 在`.card-block`中加入`display: flex;`
2. 在`.card-text`中加入`margin: auto;`

### 如何创造出响应式的文本？
基于`vw`(视窗宽度)来设置`font-size`属性。

## Button
按钮是网页的重要组件，Bootstrap的按钮设计得很漂亮，但是有些细节需要注意的。

### `.disabled`应用之后为何还会触发`onclick`事件？
`.disabled`样式只是显示效果上看起来不能点击。实际意义上的不能点击需要依靠`disabled`属性

## jQuery
使用Bootstrap怎么能少得了jQuery？这里记录jQuery的几个常用方法。

### jQuery选择器的基本使用方法？
- $(#XXX): 选择`id`为XXX的组件
- $(.XXX): 选择样式具有XXX的组件

### 如何添加、删除、开关样式？
- 添加: `$().addClass(XXX)`或`$().toggleClass(XXX, true)`
- 删除: `$().removeClass(XXX)`或`$().toggleClass(XXX, false)`
- 开关: `$().toggleClass(XXX)`

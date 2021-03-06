---
title: flex布局
date: 2019-12-25 14:05:19
tags:
cover:http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071002.png
---

# 弹性布局(伸缩布局)

> Flex是Flexible Box的缩写，翻译成中文就是“弹性盒子”，用来为盒装模型提供最大的灵活性。**任何一个容器都可以指定为Flex布局**。

CSS3在布局方面做了非常大的改进，使得我们对块级元素的布局排列变得十分灵活，适应性非常强，其强大的伸缩性，在响应式开中可以发挥极大的作用。

【演示：01-伸缩布局初体验.html】

当给一个盒子设置了display：flex之后，这个盒子就有了***主轴*** 和***侧轴*** 的概念。
主轴：Flex容器的主轴主要用来配置Flex项目，默认是水平方向
侧轴：与主轴垂直的轴称作侧轴，默认是垂直方向的
方向：默认***主轴从左向右*** ，默认***侧轴从上到下*** 

![](/flex布局/flex01.png)

## 给容器设置的样式

### flex-direction

> flex-diretion主要是用来调整主轴的方向的，默认是水平方向
>
> 了解即可，一般来说，很少调整主轴的方向。

可选值

```javascript
row：主轴方向为水平向右
column：主轴方向为竖直向下
row-reverse:主轴方向为水平向左
column-reverse:主轴方向是竖直向上。
```


### justify-content(重点)

> justify-content主要用来设置***主轴方向的对齐方式*** ，可选的值有：

可选值：

```javascript
flex-start: 弹性盒子元素将向起始位置对齐
flex-end: 弹性盒子元素将向结束位置对齐。
center: 弹性盒子元素将向行中间位置对齐
space-around: 弹性盒子元素会平均地分布在行里
space-between:第一个贴左边，最后一个贴右边，其他盒子均分，保证每个盒子之间的空隙是相等的。
```

### align-items(重点)

> align-items用于调整***侧轴的对其方式*** ，可选的值有：

```javascript
flex-start： 元素在侧轴的起始位置对其。 
flex-end： 元素在侧轴的结束位置对其。
center： 元素在侧轴上居中对其。
stretch： 元素的高度会被拉伸到最大（不能给死高度）。
```

### flex-wrap

> flex-wrap属性控制flex容器是单行或者多行,默认不换行

```javascript
nowrap： 不换行（默认），会压缩子盒子的宽度。
wrap： 当宽度不够的时候，会换行。
```

### align-content

> align-content用来设置多行的flex容器的排列方式。

```javascript
flex-start： 各行向侧轴的起始位置堆叠。 
flex-end： 各行向弹性盒容器的结束位置堆叠。
center： 各行向弹性盒容器的中间位置堆叠。
space-between： 各行在侧轴中平均分布。 
space-around： 第一行贴上边，最后一个行贴下边,其他行在弹性盒容器中平均分布。 
stretch：拉伸，不设置高度的情况下。
```

align-items与align-content的区别

```javascript
align-items调整的是侧轴的对其方式，不换行一般用align-items
align-content:必须是多行才生效，如果单行，没有效果。换行了就用align-content。
```

## 给子元素设置的样式

> 上述给容器设置的样式，都是用于对子元素进行排列的
>
> 下列的属性更多的是用于设置子元素自身的样式。

### flex属性

flex属性与用于子元素分配主轴的空间。

```css
flex:1;
```

### order属性

> order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

```javascript
order:1;
```

### align-self

> align-self也是用于设置在侧轴的位置，但是align-self给子元素设置，优先级比align-items的优先级高。

```javascript
取值与align-items的取值一样。（注意align-content）

```

【案例：六面骰子】

# 携程旅行网

> flex布局的应用。

# 360浏览器

## fullpage的使用

> fullPage.js 是一个基于 jQuery 的插件，它能够很方便、很轻松的制作出全屏网站。

参考文档 [http://www.dowebok.com/77.html](http://www.dowebok.com/77.html)

下载地址 [https://github.com/alvarotrigo/fullPage.js](https://github.com/alvarotrigo/fullPage.js)

### 基本使用

1. 引入jQuery文件，因为fullpage是jquery插件
2. 引入fullpage的js文件
3. 页面结构
4. 编写js代码

```html
<!-- 页面结构 -->
<div id="box">
    <!--每一个class为section的div都是一屏,section这个类是固定的-->
    <div class="section">我是内容1</div>
    <div class="section">我是内容2</div>
    <div class="section">我是内容3</div>
    <div class="section">我是内容4</div>
</div>

```

```javascript
//编写js代码
$(function () {
    $("#box").fullpage();
});

```


### 鼠标滚动事件(了解)

```javascript
  /* 监听鼠标滚轮事件 */
  window.addEventListener("mousewheel", function( e ) {
    // e.wheelDelta 鼠标滚动的量, 大于0向上滚, 小于0向下滚
    if (e.wheelDelta > 0) {
      console.log("往上滚动");
    }
    else {
      console.log("往下滚动");
    }
  });

```

### 常用参数

| 属性名称                 | 描述                                                         |
| ------------------------ | ------------------------------------------------------------ |
| ***sectionsColor***      | 设置每一个section的背景颜色（数组）                          |
| verticalCentered         | 设定每一个section的内容是否垂直居中，默认true，              |
| ***scrollingSpeed***     | 设置滚动的速度，默认700毫秒                                  |
| easing                   | 设置动画的方式，一般不修改, 默认是easeInOutCubic, 如果想要修改此参数，需要引入jquery.easing.js |
| css3                     | 是否使用css3 transform来实现滚动效果，默认true，不用修改，CSS3的动画效率比较js高。 |
| loopTop                  | 滚动到顶部后是否连续滚动到底部，默认false                    |
| loopBottom               | 滚动到底部后是否连续滚动到顶部，默认false                    |
| ***continuousVertical*** | 是否循环滚动，默认为false，如果设置为true，则页面会循环滚动，不会出现loopTop与loopBottom那样的跳动。 |
| autoScrolling            | 是否使用插件的滚动方式，默认true，如果选择false，会出现浏览器子代的滚动条，将不会按页滚动，按照滚动进行滚动。 |
| scrollBar                | 是否包含滚动条，默认false，如果设置为true，那么浏览器自定的滚动条会出现，这个时候，页面滚动还是按页滚动，但是浏览器也能滚动。不建议开启，不然会不同步。 |
| paddingTop/paddingBottom | 给每一个section设置一个paddingTop或者paddingBottom,默认值为0，如果需要给页面设置一个固定定位的头部菜单或者底部菜单的时候，可以使用这两个选项。 |
| keyboardScrolling        | 是否可以使用键盘方向键导航，默认true                         |
| ***navigation***         | 是否显示导航，默认为false，设置为true，会显示小圆点，作为导航 |
| navigationPositon        | 导航小圆点的位置，设置left或者right，默认是right             |
| navigationTooltips       | 小圆点的提示信息，鼠标一上去能看到提示信息                   |
| showActiveTooltip        | 是否显示当前页面的导航的tooltip信息，默认是false             |
| slidesNavigation         | 是否显示横向幻灯片的导航，默认为false                        |
| slidesNavPosition        | 设置横向幻灯片的位置，top或者bottom，默认bottom              |
| sectionSelector          | section的选择器，默认是.section                              |
| slideSelector            | slide的选择器，默认是.slide                                  |

### 常用回调函数

| 方法名                                                       | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| afterLoad(anchorLink, index)                                 | 滚动到某一个section,当滚动结束后，会触发一次这个回调函数，anchorLink是锚链接的名称，index从1开始计算 |
| onLeave(index,nextIndex,diretion)                            | 当我们离开一个section时，会触发这个函数，index是离开的页面的序号，从1开始计算。  nextIndex是滚动到的页面的序号，direction是往上还是往下滚动，值是up或者down.  return false可以取消滚动 |
| afterResize()                                                | 窗口大小发生改变后会触发的回调函数                           |
| afterSlideLoad(anchor,index,  slideAnchor,slideIndex)        | 页面滚动到某一个幻灯片的时候会触发这个回调函数               |
| afterSlideLeave(anchor,index,slideIndex,  diretion,nextSlideIndex) | 当离开某一个幻灯片的时候会触发一次这个回调函数。             |
---
title: CSS属性简写
date: 2008-09-02 10:00:00
updated: 2008-09-02 10:00:00
tags: "css"
categories: "Develop"
---

高效的 css 写法中的一条就是使用简写。通过简写可以让你的 CSS 文件更小，更易读。而了解 CSS 属性简写也是前端开发工程师的基本功之一。今天我们系统地总结一下 CSS 属性的缩写。

# 色彩缩写

色彩的缩写最简单，在色彩值用 16 进制的时候，如果每种颜色的值相同，就可以写成一个：
`color：#113366` 可以简写为 `color：#136`
所有用到 16 进制色彩值的地方都可以使用简写，比如`background-color`、`border-color`、`text-shadow`、`box-shadow`等。

<!-- more -->

# 盒子大小

这里主要用于两个属性：`margin`和`padding`，我们以`margin`为例，`padding`与之相同。盒子有上下左右四个方向，每个方向都有个外边距：

```css
margin-top: 1px;
margin-right: 1px;
margin-botton: 1px;
margin-left: 1px;
```

这四个值可以缩写到一起：

```css
margin: 1px 1px 1px 1px;
```

缩写的顺序是上->右->下->左。顺时针的方向。相对的边的值相同，则可以省掉：

```css
margin: 1px; /* 四个方向的边距相同，等同于margin:1px 1px 1px 1px; */
margin: 1px 2px; /* 上下边距都为1px，左右边距均为2px，等同于margin:1px 2px 1px 2px; */
margin: 1px 2px 3px; /* 右边距和左边距相同，等同于margin:1px 2px 3px 2px; */
margin: 1px 2px 1px 3px; /* 注意，这里虽然上下边距都为1px，但是这里不能缩写。 */
```

# 边框(border)

`border`是个比较灵活的属性，它有`border-width`、`border-style`、`border-color`三个子属性。

```css
border-width: /* 数字 + 单位 */ ;
border-style: /* none || hidden || dashed || dotted || double || groove || inset || outset || ridge || solid */ ;
border-color: /* 颜色 */ ;
```

它可以按照`width`、`style`和`color`的顺序简写：

```css
border: 5px solid #369;
```

有的时候，`border`可以写的更简单些，有些值可以省掉，但是请注意哪些是必须的，你也可以测试一下：

```css
border: groove red; /* 大家猜猜这个边框的宽度是多少？ */
border: solid; /* 这会是什么样子？ */
border: 5px; /* 这样可以吗？ */
border: 5px red; /* 这样可以吗？？ */
border: red; /* 这样可以吗？？？ */
```

通过上面的代码可以了解到，`border`默认的宽度是`3px`，默认的色彩是`black`—黑色。
默认的颜色是该规则中的`color`属性的值，而`color`默认是黑色的。
`border`的缩写中`border-style`是必须的。
同时，还可以对每条边采用缩写：

```css
border-top: 4px solid #333;
border-right: 3px solid #666;
border-bottom: 3px solid #666;
border-left: 4px solid #333;
```

还可以对每个属性采用缩写：

```css
border-width：1px 2px 3px; /* 最多可用四个值，缩写规则类似盒子大小的缩写，下同 */
border-style：solid dashed dotted groove;
border-color:red blue white black;
```

# outline

`outline`类似`border`，不同的是`border`会影响盒模型，而`outline`不会。

```css
outline-width: /* 数字 + 单位 */ ;
outline-style: /* none || dashed || dotted || double || groove || inset || outset || ridge || solid */ ;
outline-color: /* 颜色 */ ;
```

可以缩写为：

```css
outline: 1px solid red;
```

同样，`outline`的简写中，`outline-style`也是必须的，另外两个值则可选，默认值和`border`相同。

# 背景(background)

`background`是最常用的简写之一，它包含以下属性：

```css
background-color: /* color || #hex || RGB(% || 0-255) || RGBa */ ;
background-image: /* url() */ ;
background-repeat: /* repeat || repeat-x || repeat-y || no-repeat */ ;
background-position: /* X Y || (top||bottom||center) (left||right||center) */ ;
background-attachment: /* scroll || fixed */ ;
```

background 的简写可以大大的提高 css 的效率：

```css
background: #fff url(img.png) no-repeat 0 0;
```

background 的简写也有些默认值：

```css
background: transparent none repeat scroll top left;
```

background 属性的值不会继承，你可以只声明其中的一个，其它的值会被应用默认的。

# font

font 简写也是使用最多的一个，它也是书写高效的 CSS 的方法之一。
font 包含以下属性：

```css
font-style: /* normal || italic || oblique */ ;
font-variant: /* normal || small-caps */ ;
font-weight: /* normal || bold || bolder || || lighter || (100-900) */ ;
font-size: /* (number + unit) || (xx-small - xx-large) */ ;
line-height: /* normal || (number + unit) */ ;
font-family: /* name, "more names" */ ;
```

font 的各个属性也都有默认值，记住这些默认值相对来说比较重要：

```css
font-style: normal;
font-variant: normal;
font-weight: normal;
font-size: inherit;
line-height: normal;
font-family: inherit;
```

事实上，`font`的简写是这些简写中最需要小心的一个，稍有疏忽就会造成一些意想不到的后果，所以，很多人并不赞成使用`font`缩写。
不过这里正好有个小手册，相信会让你更好的理解 font 的简写：
![css-shorthand](/blog/images/css-shorthand.jpg)

# 列表样式

可能大家用的最多的一条关于列表的属性就是：

```css
list-style: none;
```

它会清除所有默认的列表样式，比如数字或者圆点。
list-style 也有三个属性：

```css
list-style-type: /* none || disc || circle || square || decimal || lower-alpha || upper-alpha || lower-roman || upper-roman */
list-style-position:  /* inside || outside || inherit */
list-style-image:  /* (url) || none || inherit */
```

list-style 的默认属性如下：

```css
list-style: disc outside none;
```

需要注意的是，如果 list-tyle 中定义了图片，那么图片的优先级要比 list-style-type 高，比如：

```css
list-style: circle inside url(../img.gif);
```

这个例子中，如果 img.gif 存在，则不会显示前面设置的 circle 符号。
PS:其实`list-style-type`有很多种很有用的样式，感兴趣的同学可以[参考一下](https://developer.mozilla.org/en/CSS/list-style-type)

# border-radius(圆角半径)

border-radius 是 css3 中新加入的属性，用来实现圆角边框。
这个属性目前不好的一点儿是，各个浏览器对它的支持不同，IE 尚不支持，Gecko(firefox)和 webkit(safari/chrome)等需分别使用私有前缀-moz-和-webkit-。
更让人纠结的是，如果单个角的 border-radius 属性的写法在这两个浏览器的差异更大，你要书写大量的私有属性：

```css
-moz-border-radius-bottomleft: 6px;
-moz-border-radius-topleft: 6px;
-moz-border-radius-topright: 6px;
-webkit-border-bottom-left-radius: 6px;
-webkit-border-top-left-radius: 6px;
-webkit-border-top-right-radius: 6px;
border-bottom-left-radius: 6px;
border-top-left-radius: 6px;
border-top-right-radius: 6px;
```

呃，是不是你已经看的眼花了？这只是要实现左上角不是圆角，其它三个角都是圆角的情况。所以对于 border-radius，神飞强烈建议使用缩写：

```css
-moz-border-radius: 0 6px 6px;
-webkit-border-radius: 0 6px 6px;
border-radius: 0 6px 6px;
```

就总结这么多，还有其它的可以缩写的属性吗？欢迎大家提出一起讨论。

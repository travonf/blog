---
title: CSS禅意花园
date: 2008-09-02 09:00:00
updated: 2008-09-02 09:00:00
tags: "css"
categories: "Develop"
---

# 第一章 追本溯源

概述“CSS 禅意花园”的来历及 CSS 的发展历程，讨论正确的标记结构和设计。

打好 CSS 布局的基础

1. 带有语义的标记
   CSS 用来表现样式，HTML 用来表明结构。
2. 创建良好的标记
   选择 DOCTYPE
   指定语言和字符集
   指定标题：`<title>css Zen Garden:The beauty in CSS Designs</title>`
   选用恰当的元素
   避免过度使用`div`和`span`
   尽可能少的使用标签
   适当地使用`class`和`id`
3. 时间的检验
4. 禅意花园的 HTML 源代码
5. HTML 结构的图示
6. 提供足够的灵活性

# 第二章 设计

阐述基本设计元素及其在 Web 设计中的应用，包括色彩理论、比例、位置、文字和图片之间的关系以及如何协调地使用 Adobe Photoshop 和 CSS。

# 第三章 正文布局

详细阐述如何创建复杂的 CSS 布局，包括分栏、浮动内容和定位方案。

## 理解绝对定位和浮动

1. 布局基础
   绝对定位：可以丝毫不差的精确控制任何元素的位置，应用绝对定位的元素被不留痕迹的从常规文档流中完全移除
   浮动：采用浮动的元素仍会保留在文档流中，其周围环绕的元素也都清楚它的位置
2. 布局方法
   使用绝对定位时页脚不好计算，所以可以采用绝对定位与浮动结合的方案
3. 绝对定位的补充

## 当代 Web 设计中的居中布局

1. 固定布局和流式布局
   固定布局指页面有着固定的宽度，居左，居右对齐，或者居中，但是内容的宽度不随着浏览器窗口的宽度变化而变化
   流式布局又称为不固定布局或动态布局。这种布局的页面用百分比指定，而不是某个固定的宽度，所以当浏览器窗口大小变化时，页面宽度也随之变化，始终保持填满浏览器
2. 让作品居中显示
   **使用自动外边距实现居中**

   ```css
   div#container {
     margin-left: auto;
     margin-right: auto;
     width: 168px;
   }
   ```

   说明：左右边距设为自动，那么应该有宽度，否则填满窗口

   **使用 text-align 实现居中**

   ```css
   body {
     text-align: center;
   }
   #container {
     text-align: left;
   }
   ```

   说明：body 设置居中，那么子元素必须重置，否则会继承居中

   **组合使用自动外边距和文本对齐**

   ```css
   body {
     text-align: center;
   }
   #container {
     margin-left: auto;
     margin-right: auto;
     width: 168px;
     text-align: left;
   }
   ```

   说明：将自动外边距与 text-align 居中对齐结合使用达到浏览器兼容最大化

   **负外边距解决方案**

   ```css
   #container {
     position: absolute;
     left: 50%;
     width: 800px;
     margin-left: -400px;
   }
   ```

   说明：绝对定位之后，设置左移到窗口的一半（也就是中线），然后负左边距宽度的一半，刚好实现一半在中线左，另一半在中线右边，实现居中

3. 创建有效布局的法则与步骤

## Web 页面的布局法则

三思而后行

### 布局的实现方式

### 布局的灵感和法则

用户界面设计

- 了解将浏览页面的用户
- 在页面和站点中给用户足够的导向
- 使用被人们熟知的象征符号
- 保证与功能相关的特性在页面中足够显眼
- 保证设计元素的一致性
- 了解页面中的关键元素
- 清楚的表达页面的内容

可用性

- 重要信息应放在显眼的位置
- 永远在 title 元素中给出页面的简单介绍
- 尽可能的保证页面中的导航链接有着一致的表现
- 对于中型或大型站点来说，强烈建议提供搜索功能
- 用缩进和偏移将栏中内容分开

### 遵守设计流程

#### 在垂直的世界中使用水平布局

1. 从印刷作品中找到灵感
   打破常规
2. 水平带来的挑战
   考虑固定定位
   考虑浏览器缺陷
   利用子选择器为不支持固定定位的浏览器附加另外的样式
3. 学到的东西

###3 含义丰富的定位，充分理解网格

1. 元素的位置以及其带来的含义
   思考：元素分别位于左上象限，右上象限，底部带来的效果及用户的关注度
2. 网格
3. 创建网格
   页首
   内容区域
4. 跳出网格的限制
   **绝对定位**  
   理解绝对定位的前提就是理解文档流的概念，HTML 是线性的，不应用任何样式的情况下，HTML 解释器将从头到尾按顺序解析文档中的元素，并自上向下将元素依次显示在浏览器中，而绝对定位则不仅可以将某元素置于页面中的任何位置之上，还能够将其从文档流中移除。绝对定位元素不会影响到文档中的其他元素，其他元素依然会以线性的方式进行布局，就像绝对定位元素根本不存在一样。
   在唯一一种情况下，绝对定位元素也会影响到页面中的其他元素，即当某个元素被包含在该绝对定位元素中，且同样应用了 CSS 定位时。
   **相对定位**  
   相对定位则不会把元素从文档流中移除，而是基于其原位置进行一定得偏移。页面中其他元素不会占据其偏移后留下的空白空间，就像该元素仍在原位置一样。

#### 处理布局中常见的溢出问题

1. 内容溢出
2. 浮动导致的内容溢出
   用标签清除浮动

   ```css
   .clear {
     clear: both;
   }
   ```

   ```html
   <div class="clear"></div>
   ```

   精确控制浮动元素
   增大区域的宽度
   限制内容宽度并注意斜体
   限制内容溢出：overflow 属性

3. 绝对定位导致的内容溢出
   垂直溢出
   - 用浮动代替绝对布局
   - 在设计中尝试避免该问题
   - 限制溢出：overflow 属性
   - 使用脚本
   - 用 em 而不是 px 作为长度单位
4. 设计时考虑溢出

# 第四章 图像

使用图像改善布局以及如何生成图像，包括图像替换、图形文件格式及寻找图像素材。

理解图像文件格式以及优化方法

在 CSS 中为作品应用图像

1. 实际应用
   背景图像方法才能用于实际开发中
   ```css
   h1 {
     background: url(bg.gif) top left no-repeat;
     width: 400px;
     height: 20px;
   }
   ```
   说明：最好为容器指定大小，背景图像的位置声明，先水平再垂直。
2. 图像替换
   Fahrner 图像替换法

   ```html
   <h1 id="pageHeader"><span> css Zen Garden</span></h1>
   ```

   ```css
   #pageHeader {
     background: url(bg.gif) top left no-repeat;
     width: 400px;
     height: 20px;
   }
   #pageHeader span {
     display: none;
   } /*可以使用display:none或者visibility:hidden隐藏*/
   ```

3. 图像替换的责任
4. 更好的技术

   **Leahy 和 Langridge 方案**

   ```html
   <h3 id="header">I like cola.</h3>
   ```

   ```css
   #header{
       padding:25px 0 0 0;
       overflow:hidden;
       background:url(bg.gif) no-repeat;
       height:0px !important;
       height /** /:25px;
       }
   ```

   **Rundle 的方案**

   ```html
   <h3 id="header">I like cola.</h3>
   ```

   ```css
   #header {
     text-indent: -9999px;
     background: url(bg.gif) no-repeat;
     height: 25px;
   }
   ```

   **Levin 的方案**

   ```html
   <h3 class="replace" id="myhl">I like cola.<span></span></h1>
   ```

   ```css
   .repalce {
     position: relative;
     margin: 0px;
     padding: 0px;
     /*hide overflow:hidden from IE5/Mac */
     overflow: hidden;
   }
   .replace span {
     display: block;
     position: absolute;
     top: 0px;
     left: 0px;
     z-index: 1; /*for Oprea 5 and 6*/
   }
   #myhl,
   #myhl span {
     height: 25px;
     width: 300px;
     background: url(bg.gif);
   }
   ```

5. 选择
   应该选择哪种方法完全靠自己选择

# 第五章 文字排印

Web 上字体的局限性及其避免方法等有关文字的方方面面，包括字号、字体的选择和基于图像的文字等。

# 第六章 特效

掌握基本知识后该做什么？根据用户使用的浏览器采用不同样式的高级 CSS 效果、创建灵活布局的技巧，以及使用巧妙的代码克服技术的局限性。

## 级联和分层效果

1. 级联
   特殊性
   - 控制特殊性
   - 调试特殊化行为
   - 覆盖特殊性
2. 分层
   z-index 属性
3. 结合

## 基于同一样式表的两种设计

1. MOSe
   子选择器
   ```css
   div#container > p {
     color: orange;
   }
   ```
   说明：所有#container 元素的直接子段落元素都将显示为橙色。
   邻接选择器
   ```css
   div#warning p + p {
     color: red;
   }
   ```
   说明：这条规则会让第一个在#warning 区域中的段落元素的所有兄弟段落元素都显示为红色
   属性选择器以及模式匹配
   ```css
   [id] {
     color: red;
   }
   [id="warning"] {
     color: red;
   }
   [href~="http://www.molly.com/"]
   {
     text-decoration: none;
   }
   ```
2. CSS 签名
3. 为 IE 实现独特的样式
4. 能经受住未来考验的设计

# 第七章 重构

介绍 6 位设计师进行重构的方法。给出了这 6 件设计作品创建的过程，详细阐述了每一步。综合运用本书其他 5 章介绍的设计原则，就能在这里获得最佳的效果。

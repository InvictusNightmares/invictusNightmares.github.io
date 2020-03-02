---
layout:     post
title:      "FE training"
subtitle:   "前端培训课程"
tags:
   - 前端开发
---

# 前端培训课程

本次课程主要的目的是让大家能够了解前端的基本组成和一些前端的基本知识。

众所周知，前端是有三部分组成：**HTML**，**CSS**，**JavaScript**，三者的关系可以用比较通俗的方式来理解：

HTML可以理解为一只小鸟的骨架，CSS可以理解为小鸟各种五彩缤纷的皮肤，而JS就是让小鸟飞起来的一些特性。下面来对这三个部分进行展开：

### HTML

HTML的英文全称是 Hypertext Marked Language，即超文本标记语言，现在绝大数浏览器里的网页都是采用HTML写的。

```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge" >
      <title>first project</title>
  </head>
  <body>
      <p>content</p>
  </body>
</html>
```



* !DOCTYPE文档类型声明 

* html标签，需要把属性lang中的"en"值改为"zh-CN"，不同语言环境考虑不同值； 

* meta标签，字符编码为"UTF-8"，表示面向全人类的字符编码；

* meta标签，在viewport（浏览器视窗）的属性中加上兼容手机，禁用缩放的属性值；

* meta标签，网页的兼容性模式设置为IE浏览器需要使用最新内核； 

* 需要有title标签，标签中的内容将显示浏览器的标题栏中；
* body里面的元素显示在浏览器中



#### 常见的标签

* h1~h6 呈现了六个不同的级别的标题，h1 级别最高，而 h6 级别最低。

* section 表示一个包含在HTML文档中的独立部分，它没有更具体的语义元素来表示，一般来说会有包含一个标题。 

* article 表示文档、页面、应用或网站中的独立结构，其意在成为可独立分配的或可复用的结构，如在发布中，它可能是论坛帖子、杂志或新闻文章、博客、用户提交的评论、交互式组件，或者其他独立的内容项目。

* p 元素（或者说 HTML 段落元素）表示文本的一个段落。该元素通常表现为一整块与相邻文本分离的文本，或以垂直的空白隔离或以首行缩进。另外，p是块级元素。

* header用于展示介绍性内容，通常包含一组介绍性的或是辅助导航的实用元素。它可能包含一些标题元素，但也可能包含其他元素，比如 Logo、搜索框、作者名称，等等。

* footer表示最近一个章节内容或者根节点（sectioning root ）元素的页脚。一个页脚通常包含该章节作者、版权数据或者与文档相关的链接等信息。

* main元素呈现了文档的body或应用的主体部分。主体部分由与文档直接相关，或者扩展于文档的中心主题、应用的主要功能部分的内容组成。  

* aside表示旁支内容，元素表示一个和其余页面内容几乎无关的部分，被认为是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。

* div是一个通用型的流内容容器



#### 常用的全局属性

* class 一个以空格分隔的元素的类名（classes ）列表，它允许 CSS 和 Javascript 通过类选择器 (class selectors) 或DOM方法( document.getElementsByClassName)来选择和访问特定的元素。 

* contenteditable一个枚举属性（enumerated attribute），表示元素是否可被用户编辑。 如果可以，浏览器会调整元素的部件（widget）以允许编辑。 true 或者空字符串，表明元素是可被编辑的； false，表明元素不能被编辑。

* hidden布尔属性表示该元素尚未或不再相关。例如，它可用于隐藏在登录过程完成之前无法使用的页面元素。浏览器不会呈现此类元素。不得使用此属性隐藏可合法显示的内容。

* id定义唯一标识符（ID），该标识符在整个文档中必须是唯一的。 其目的是在链接（使用片段标识符），脚本或样式（使用CSS）时标识元素。

* style含要应用于元素的CSS样式声明。



## CSS

每个html元素都有一组样式属性，可以通过css来设定。当html元素的同一个样式属性有多种样式值的时候，css就要靠层叠机智来决定最终应用哪种样式。

#### CSS规则

![](https://user-gold-cdn.xitu.io/2017/7/19/e13f641a5c8164a6937228f0c220f214)

#### 添加样式的三种方法

- 写在元素标签里（也叫行内样式，只能影响它所在的标签，会覆盖嵌入样式和链接样式）

- 写在 `<style>`标签里（也就嵌入样式，应用范围仅限于当前页面，页面样式会覆盖外部样式表中的样式，但会被行内样式覆盖）

- 写在单独css样式表中（也叫链接样式，样式表是一个扩展名为.css 的文件，可以在任意多个HTML页面链接同一个样式表文件。链接样式的作用范围是整个网站）

对这个基本的结构有三种方法可以进行扩展：

**1.**多个声明包含在一条规则里。

```css
p {color: red; font-size: 12px; font-weight: bold;}
```

**2.**多个选择器组合在一起。例如：如果想让`<h1>`、`<h2>`和 `<h3>`的文本都变成蓝色粗体可以这么写：

```css
h1 {color: blue; font-weight: bold;}
h2 {color: blue; font-weight: bold;}
h3 {color: blue; font-weight: bold;}
```

也可以这么写：

```css
h1, h2, h3 {color: blue; font-weight: bold;}
```

**分组选择符以逗号作为分隔符**

**3.** 多条规则应用给一个选择符。
例如，写完上边的规则，还想把h3变成斜体，那么可以再为h3单独写一条规则：

```css
h1, h2, h3 {color: blue; font-weight: bold;}
h3 {font-style: italic;}
```

#### 选择特定元素的选择符

**1.上下文选择符**

上下文选择符，叫后代组合式选择符，就是一组以空格分隔的标签名。用于选择作为特定祖先元素后代的标签。

```
标签1 标签2 {声明}
```

```css
article p {font-weight: bold;}
```

这个例子就是只有article后代的p元素才会应用后边的样式。

**2.ID和类选择符**

**类属性**

```html
<h1 class="specialtext">This is text</h1>
```

```css
.specialtext {color: red;}
```

##### ID属性

```html
<h1 id="specialtext">This is text</h1>
```

```css
#specialtext {color: red;}
```

#### 继承

CSS属性的值会向下传递。

比如我们添加一条这样的规则：

```css
body: {font-family: arial;}
```

那么文档的所有元素都将继承这个样式。



#### Flex 

其实对于后端工程师来说，CSS才是最难学的部分，早期的CSS思想确实比家别扭，不过现代前端基本上已经都是Flex布局，下面来介绍下：

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

**容器属性**

- `flex-direction`
- `flex-wrap`
- `flex-flow`
- `justify-content`
- `align-items`
- `align-content`

**1.** `flex-direction`属性决定主轴的方向（即项目的排列方向)

```
row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。
```

**2.**  `flex-wrap`属性

```
nowrap（默认）：不换行。
wrap：换行，第一行在上方。
wrap-reverse：换行，第一行在下方。
```

**3.**  `flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`

**4.** `justify-content`属性定义了项目在主轴上的对齐方式

```
flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```

**5.** ``align-items`属性定义项目在交叉轴上如何对齐`

```
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```

**6.** `align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

```
flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴。
```

**元素属性**

- `order`
- `flex-grow`
- `flex-shrink`
- `flex-basis`
- `flex`
- `align-self`

**1.**  `order`属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

**2.** `flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

**3.** `flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

**4.** `flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

**5.** `flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

​    该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

​    建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

**6.** `align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。

​    默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

​    该属性可能取6个值，除了auto，其他都与align-items属性完全一致。



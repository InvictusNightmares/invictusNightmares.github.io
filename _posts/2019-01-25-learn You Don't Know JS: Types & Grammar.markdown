---
layout:     post
title:      "learn You Don't Know JS: Types & Grammar"
subtitle:   "你不知道的JavaScript学习-类型和语法"
tags:
   - javascript
---
# 你不知道的JavaScript学习-类型和语法

## 类型

大多数开发者都认为JS是没有类型的，或者不像Java那样有强制类型（静态类型），但是在日常开发中，强制类型转换我们几乎都能遇到，正确的认识JS的类型，对我们处理这些头疼的问题有很大的帮助。

### 1.内置类型
JS有七种内置类型：

* **null**
* **undefined**
* **boolean**
* **number**
* **string**
* **object**
* **symbol**(ES6新增) 

其中除了**object**是叫**引用类型**，其他六种叫**基本类型**。

我们可以在控制台上自己试一下看一下效果：
<center><img src='../../../../img/201901/js1.png'></center>
我们会发现少了一个**null**，那`typeof null`是什么呢？在控制台打印一下：
<center><img src='../../../../img/201901/js2.png'></center>
发现并不是我们预期的结果**null**
这个bug由来已久，在JS中已经存在了将近二十年，也许永远也不会修复，因为这牵涉到太多的 Web系统，“修复”它会产生更多的bug，令许多系统无法正常工作。
那么我们就需要用复合条件来判断null值：

```
var a = null;
(!a && typeof a === 'object'); // true
```

我们再来看看我们常用的**function**, **array**，在控制台打印：
<center><img src='../../../../img/201901/js3.png'></center>
<center><img src='../../../../img/201901/js4.png'></center>

虽然`typeof function`打印出来的是**“function”**，但是它实际上是**object**的一个“子类型”。具体来说，函数是“可调用对象”，它有一个内部属性**[[Call]]**，该属性使其可以被调用。它不仅仅是对象，还可以拥有属性，就像图里的：因为该函数声明了两个命名参数，b 和 c，所以其 length 值为 2。

再来看数组，数组也是对象，确切的说也是**object**的一个“子类型”。它的元素按数字顺序来进行索引(而非普通像对象那样通过字符串键值)，其length属性是元素的个数。

### 3.值和类型
JS中变量是没有类型的，只有值才有。变量可以随时持有任何类型。

**3.1 undefined 和 undeclared**
在控制台里打印：
<center><img src='../../../../img/201901/js5.png'></center>
这确实让人头疼的一件事，在这里大家可以这样理解：**“undefined”** 和 **“is not defined”** 是两码事；已在作用域中声明但还没有赋值的变量，是 **undefined** 的。相反，还没有在作用域中声明过的变量，是 **undeclared** 的。但是对于 undeclared 变量，
typeof照样返回 “undefined”，这是因为typeof有一个特殊的安全防范机制。

## 值

### 1.数组
和其他强类型语言不同，在JS中，数组可以容纳任何类型的值：
<center><img src='../../../../img/201901/js6.png'></center>
数组通过数字进行索引，但它们也是对象，可以包含字符串键值和属性：
<center><img src='../../../../img/201901/js7.png'></center>

### 2.字符串
在JS中，字符串是不可变的，数组是可变的。字符串不可变是指字符串的成员函数不会改变其原始值，而是创建并返回一个新的字符串。而数组的成员函数都是在其原始值上进行操作：
<center><img src='../../../../img/201901/js8.png'></center>

### 3.数字
JS只有一种数值类型:number(数字)，包括“整数”和带小数的十进制数。此处 “整数”之所以加引号是因为和其他语言不同，JavaScript 没有真正意义上的整数，这也是它一直以来为人诟病的地方。这种情况在将来或许会有所改观，但目前只有数字类型。

JS中的“整数”就是没有小数的十进制数。所以 42.0 即等同于“整数”42。

JS中的数字类型是基于IEEE754标准来实现的，该标准通常也被称为“浮点数”。使用的是“双精 度”格式(即 64 位二进制)。

**0.1 + 0.2 问题**

二进制浮点数最大的问题(所有遵循IEEE754规范的语言都是如此)，是会出现如下情况:

```
0.1 + 0.2 === 0.3 // false
```
简单来说就是因为二进制浮点数中的 0.1 和 0.2 并不是十分精确，它们相加的结果并非刚好等于 0.3，而是一个比较接近的数字 0.30000000000000004。

那应该怎么判断，就是设置一个误差范围值，通常称为“机器精度”，对JS来说，这个值通常是2^-52 (2.220446049250313e-16)。

在ES6中，这个值定义在Number.EPSILON，在ES6之前可以这样写polyfill：

```
if(!Number.EPSILON) {
  Number.EPSILON = Math.pow(2,-52);
}
```

这样我们就可以判断 `0.1 + 0.2 = 0.3` 了：
<center><img src='../../../../img/201901/js9.png'></center>

### 4.特殊数值

**不是值的值**
undefined 和 null 常被用来表示“空的”值或“不是值”的值。但两者也有区别：

* **undefined** 指从未赋值(empty value)
* **null** 指曾赋过值，但是目前没有值(missing value)

这里要特别注意：null 是一个特殊关键字，不是标识符，我们不能将其当作变量来使用和赋值。然而undefined 却是一个标识符，可以被当作变量来使用和赋值。

通过**void**运算符我们可以得到**undefined**值

**NaN**
是指“不是一个数字”，但它仍然是数字类型。而且**NaN**是唯一一个非自反的值，意思就是它和自身不相等；

```
NaN != NaN // true
``` 

**Infinity**

在JS中，“除以0”的结果为**Infinity**

```
var a = 1 / 0; // Infinity
var b = -1 / 0; // -Infinity
```

**0 和 -0**

-0除了可以作为常量以外，可以作为某些数学运算的返回值：

```
var a = 0 / -3; // -0
var b = 0 * -3 // -0
```

在控制台打印一下：
<center><img src='../../../../img/201901/js10.png'></center>
那么**-0**的作用是什么？比如在程序中数据需要以级数形式表示（比如动画帧的移动速度），符号位用来代表其他信息（比如移动方向）。此时如果一个值为 0 的变量失去了它的符号位，它的方向信息就会丢失。所以保留 0 值的符号位可以防止这类情况发生。

由于**NaN**和**-0**在相等比较的时候有些特别，ES6引入了一个新方法`Object.is(...)`来判断两个值是否绝对相等：
<center><img src='../../../../img/201901/js11.png'></center>

### 值和引用
JS中没有指针，变量不可能成为指向 另一个变量的引用。JS引用指向的是值。如果一个值有 10 个引用，这些引用指向的都是同一个值，**它们相互之间没有引用/指向关系**。

基本类型值总是通过值复制的方式来赋值/传递；而引用类型值总是通过引用复制的方式来赋值/传递。

下面来看一个例子：
<center><img src='../../../../img/201901/js12.png'></center>

赋值 / 参数传递是通过引用还是值复制完全 由值的类型来决定，所以使用哪种类型也间接决定了赋值 / 参数传递的方式。

## 原生函数

### 内部属性 [[Class]]
所有 typeof 返回值为 "object" 的对象(如数组)都包含一个内部属性 [[Class]]。我们可以通过这个思路来解决一个常见的面试题：如何判断一个值是对象还是数组：
<center><img src='../../../../img/201901/js13.png'></center>

### 封装对象包装
由于基本类型值没有 .length 和 .toString() 这样的属性和方法，需要通过封装对象才能访问，此时JS会自动为基本类型值包装一个封装对象:

```
var a = 'abc';
a.length; // 3
```

## 强制类型转换


### 值类型转换
将值从一种类型转换为另一种类型通常称为类型转换；书中分为显式强制类型转换和隐式强制
类型转换。看例子：

```
var a = 42;
var b = a + ''; // 隐式强制类型转换
var c = String(a); // 显式强制类型转换
```

### 抽象值操作

**ToString**
基本类型值的字符串化规则为：null 转换为 "null"，undefined 转换为 "undefined"，true 转换为 "true"。数字的字符串化则遵循通用规。对于普通对象，除非自行定义，否则 toString()返回内部属性 [[Class]] 的值，如果对象有自己的 toString() 方法，字符串化时就会调用该方法并 使用其返回值。

**ToNumber**
 ES5规范定义了true 转换为 1，false 转换为 0。undefined 转换为 NaN，null 转换为0。对字符串进行字面量上的转换，失败返回 NaN。对于对象会先转换成基本类型，再按照上述规则进行转换。
这里要提一下JS的ToPrimitive（抽象操作）算法，会首先该值是否有 valueOf() 方法。 如果有并且返回基本类型值，就使用该值进行强制类型转换。如果没有就使用 toString()的返回值(如果存在)来进行强制类型转换。
 
 **ToBoolean**
 JS中的值可以分为以下两类:
 
*  可以被强制类型转换为 false 的值
*  其他(被强制类型转换为 true 的值)

ES5规范定义了这些假值：

* undefined
* null
* false
* +0 -0 NaN
* ""

这里说一下 `||` 和 `&&`，书里面说把它们叫“逻辑运算符”不太准确，应该称它们为“选择器运算 符”，因为在JS中它们返回的值不是布尔值。它们的返回值是两个操作数中的一个(且仅一个)。即选择两个操作数中的一个，然后返回它的值。其实我们在日常开发中也会经常碰到：

```
function foo(a) {
  a = a || 'hello';
}

function bar() {
  console.log(b);
}
var b = 42;
b && bar();
```

### == 和 ===
我们常见的误区是“== 检查值是否相等，=== 检查值和类型是否相等”。但正确的解释是“== 允许在相等比较中进行强制类型转换，而 === 不允许”。

github上有人列出了各种相等比较的情况：
<center><img src='../../../../img/201901/js14.png'></center>

### < 和 >
比较双方首先调用 ToPrimitive，如果结果出现非字符串，就根据 ToNumber 规则将双方强 制类型转换为数字来进行比较；如果比较双方都是字符串，则按字母顺序来进行比较；

## 语法

看下面这个例子：

```
var a= 3 * 6;
var b = a;
b;
```
这三行代码都是包含表达式的语句。`var a = 3 * 6`和`var b = a`称为“声明语句”。因为它们声明了变量(还可以为其赋值)。`a = 3 * 6` 和 `b = a`(不带 var)叫作“赋值表达式”。第三行代码中只有一个表达式 b，同时它也是一个语句(虽然没有太大意义)。这样的情况通常叫作“表达式语句”

### 语句的结果值
语句都有结果值，在控制台里输入`var a = 42`会得到undefined，因为规范定义var的结果值是undefined。所以在我们在控制台上会看到很多语句的返回值为udefined，其实控制台中显示的就是语句的结果值。

### 运算符优先级
下面列出MDN上整理的JS运算符优先级（从高到低）：
<center><img src='../../../../img/201901/js15.png'></center>

### 自动分号(ASI)
有时在代码里如果缺少了必要的**;** 程序将无法运行，所以JS引入了自动分号插入(ASI)，提高了语言的容错性。注意ASI只在换行符处起作用而不会在代码行的中间插入分号。

### 错误
在编译阶段发现的代码错误叫作“早期错误”(early error)。语法错误是早期错误的一种(如 a = ,)。

**暂时性死区(TDZ)**
这个概念是ES6新引入的，是指由于代码中的变量还没有初始化而不能被引用的情况。

最直观的例子就是let块作用域：

```
 {
   a = 2;      // ReferenceError!
   let a;
 }
```

### try...finally
finally 中的代码总是会在 try 之后执行，如果有 catch 的话则在 catch 之后执行。也可以将 finally 中的代码看作一个回调函数，即无论出现什么情况最后一定会被调用。如果 finally 中抛出异常(无论是有意还是无意)，函数就会在此处终止。如果此前 try 中 已经有 return 设置了返回值，则该值会被丢弃。通常来说，在函数中省略return的结果和return;及return undefined;是一样的，但是 在 finally 中省略 return 则会返回前面的 return 设定的返回值。

## 总结
其实这块知识使我们平时比较容易忽略的地方，但是也是非常重要的，掌握了这些知识之后我们再回过头来看代码里的某些片段肯定会理解的更加透彻。其实这块知识点我个人觉得书上讲的都是一些偏理论的知识，这块知识点我们日常用的最多的应该是JS几种数据类型自带的方法。以后我会总结一下String，Array， Object这三种我们日常开发中用的最多的数据类型它们自带的所有方法。

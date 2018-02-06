#                       JavaScript学习笔记

## 一、JavaScript简介

JS是一种专为网页交互而设计的一门脚本语言，它分为以下几个部分：

1、ECMAScript，由ECMA-262定义，提供核心语言功能；

2、DOM（文档对象模型），提供访问和操作网页内容的方法和接口；

3、BOM（浏览对象模型），提供与浏览器交互的方法和接口。

## 二、在HTML中使用JavaScript

### 1. < script>元素

< script>元素的六个属性：

    1. async：可选。异步加载属性，属性。只对外部脚本有效，表示立即下载脚本，但不妨碍页面

​           的其他操作。

    2. charset：字符编码属性，可选。默认是utf-8编码，主要表示通过src属性指定的

​            代码的字符集，大多浏览器会忽略它的值，所以很少有人使用。

  3.defer：脚本延迟属性，可选。用来延迟脚本的执行时间，直到HTML文档已经全

​         部被解析和显示之后再执行，只对外部脚本文件有效。

  4.language：脚本类型属性，不是标准组成的一部分，已废弃。大多数浏览器

​              会忽略这个属性，已没必要使用。

  5.src：链接外部文件属性，可选。表示包含要执行代码的外部文件。注意，

​        一旦设置src属性，script元素中编写的JavaScript代码就可能无效。

    6. type：脚本类型属性，可选。默认值为text/javascript。可以看成language

​          的替代属性，表示编写代码所使用的内容类型（也叫mime类型）。

使用< script>元素有两种方式：直接嵌入和用JS外部文件。

**直接嵌入：** 只需为< script>元素指定type属性，然后像下面一般放在元素内部：

< script type="text/javascript">

..........

< /script>

包含在< script>中的元素就会从上到下依次被解释。

**外部JS文件** ：导入外部JS脚本，一定要加上src属性。

例如：< script type="text/javascript" src="example.js">< /script>

另外，src属性还可以包含来自外域的JS文件。

例如：< script type="text/javascript" src="http:// www.somewhere. com/afile.js">< /script>

#### 1.1标签位置

一般来说，所有的< script>元素都应该包含在< head>元素中，例如：

```
<!DOCTYPE html>
<html>
<head>
    <title>Title</title>
    <style type=text/css >

    </style>
    <script type="text/javascript " src="example.js"></script>
</head>
<body>
<!--内容-->
</body>
</html>
```

但是对于那些JavaScript代码很多的页面来说，这会导致浏览器在加载页面的时候出现明显的延迟，为避免这一问题，现代web应用程序一般都把全部JavaScript引用放在< body>元素内容后面，例如：

```
<!DOCTYPE html>
<html>
<head>
    <title>Title</title>
    <style type=text/css >

    </style>
</head>
<body>
<!--内容-->
 <script type="text/javascript " src="example.js"></script>
</body>
</html>
```

#### 1.2延迟脚本

< script>的defer属性，用途就是表明脚本在执行时不会影响页面的构造。也就是说，脚本会

被延迟到整个页面都解析完毕后再运行。因此，在< script>中设置defer属性，相当于告诉浏览器立即下载，但延迟执行。例如：

```
<!DOCTYPE html>
<html>
<head>
    <title>Title</title>
    <script type="text/javascript " src="example.js" defer="defer"></script>
</head>
<body>
<!--内容-->
</body>
</html>
```

**注意：** defer属性只对外部脚本文件有效。

#### 1.3异步脚本

async只适用于外部脚本，并告诉浏览器立即下载文件，但与defer不同的是，标记为async的脚本不保证按照指定顺序执行。

`<script type="text/javascript" async src="example1.js" ></script>` 

`<script type="text/javascript" async src="example2.js" ></script>` 

像以上两个脚本文件，第二个脚本文件可能先于第一个脚本文件执行。指定async属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。为此，建议异步脚本不要在加载期间修改DOM。 异步脚本一定会在页面的load时间前执行，但可能会在DOMContentLoaded时间触发之前或是之后执行。

#### 1.4在XHTML中的用法

可扩展超文本标记语言，即XHTML。不推荐使用，跳过。

### 2.嵌入代码与外部文件

最好使用JavaScript外部文件。

### 3.文档模式

IE5.5引入了文档模式的概念。文档模式：混杂模式和标准模式。混杂模式会让IE的行为与IE5相同，而标准模式与                                                                              IE的行为更接近标准行为。虽然这两种模式主要影响css，但是某些情况也会影响到JS的解释行为。随后其他浏览器纷纷效仿，IE有提出一种所谓的准标准模式，基本符合标准，但也不尽然。其中，混杂模式不值得推荐，在不同浏览器中这种模式的行为差异很大，如果不使用hack技术，跨浏览器的行为根本就没有一致性可言。

#### 4.< noscript>元素

早期浏览器都面临一个问题当浏览器不支持JS时如何做到让页面平稳地退化。解决方案是创造一个< noscript>元素，在不支持JS的浏览器中显示替代内容。这个元素可以出现在< body>中出现 < script>中的任何一个元素。在两种情况下才会显示：

 浏览器不支持脚本

浏览器支持脚本，但脚本被禁用

##  三、基本概念

### 1.语法

#### .区分大小写

#### .标识符

指变量，函数，属性的名字，函数的参数。其第一个字符必须是英文字母，数字或$，其他字符可以是字母，数字，下划线，美元符号。

**注意：** 不要把关键字、保留字、null、false、true

#### .注释

//单行注释         /*........................ */多行注释

#### .严格模式

ECMAScript5引入了严格模式的概念。严格模式是为JS定义了一种不同的解析与执行模型。在严格模式下，ECMAScript3中的一些不确定的行为将得到处理，而且对某些不安全的操作会抛出错误。启用严格模式，可以在顶部添加如下代码：”use strict”，在函数内部的上方包含这条编译指示，也可以指定在严格模式下执行。

#### .语句

语句结束以分号结尾。

### 2.关键字和保留字

见图

### 3.变量

定义变量用var，如果省略了var，就是定义了全局变量，只要调用了一次函数，这个变量就有了定义，就可以在函数外部的任何地方被访问到。

可以使用一条语句定义多个变量，只要用逗号分隔开，如：

var  message =0,

​        age=29;

### 4.数据类型

ECMAScript中有5种简单数据类型（基本数据类型）：undefined、null、boolean、number和string。还有一种复杂数据类型—object,object本质上是由一组无序的名值对组成的。

**.Undefined类型** 在使用var声明变量但未初始化，这个变量就是Undefined。

**.null类型** 也只有一个值null，逻辑角度是一个空的对象指针，使用typeof返回object的原因。如果定义的变量用于保存对象，最好初始化为null而不是其他值。由于undefined是派生于null，所以两者相等性测试为true。不必显示的设置一个变量的值为undefined，但是null正相反，如果一个变量将用于保存对象，最好设置为null，不仅体现null作为空对象指针的惯例，也可以区分两者。
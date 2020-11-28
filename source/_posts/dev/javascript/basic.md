---
title: JavaScript基础
date: 2008-09-03 08:00:00
updated: 2008-09-03 08:00:00
tags: "javascript"
categories: ["Develop", "Javascript"]
---

## JS 基础

| JS 实现   |            | `<script>` 和 `</script>` 之间的代码行包含了 `JavaScript`                                 | `HTML` 的 `<script>` 标签用于把 `JavaScript` 插入 `HTML` 页面当中                                |
| --------- | ---------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| JS 放置   | `head`部分 | `<head><script type="text/javascript">....</script></head>`                               | 当页面载入时，会执行位于 `body` 部分的 `JavaScript`                                              |
|           | `body`部分 | `<body><script type="text/javascript">....</script></body>`                               | 当被调用时，位于 `head` 部分的 `JavaScript` 才会被执行                                           |
|           | 外部脚本   | `<head><script src="xxx.js">....</script></head>`                                         | 引用外部脚本文件                                                                                 |
| JS 语句   | 分号       | `;`                                                                                       | 分号用于分隔 `JavaScript` 语句                                                                   |
|           | 代码块     | `{}`                                                                                      | `JavaScript` 是由浏览器执行的语句序列                                                            |
|           | 换行       | `\`                                                                                       | 您可以在文本字符串中使用反斜杠对代码行进行换行                                                   |
| JS 注释   | 单行注释   | `//`                                                                                      | `JavaScript` 注释可用于增强代码的可读性                                                          |
|           | 多行注释   | `/* */`                                                                                   | 多行注释以 `/*` 开始，以 `*/` 结尾                                                               |
| JS 变量   | 声明变量   | `var a;` `var b=10;`                                                                      | 变量是用于存储信息的容器： `x=5;` `length=66.10;`                                                |
| JS 运算符 | 算数运算符 | `+ - * / % ++ --`                                                                         | 运算符 `=` 用于赋值, 运算符 `+` 用于加值                                                         |
|           | 赋值运算符 | `= += -= *= /= %=`                                                                        |                                                                                                  |
|           | 逻辑运算符 | `&& \|\| !`                                                                               |                                                                                                  |
|           | 比较运算符 | `== === != > < >= <=`                                                                     | `===` 全等（值与类型）                                                                           |
| JS 语句   | 条件语句   | `if (){}; if (){} else{}; if (){} else if{} else{}; switch(n){case 1:;case 2:;default:;}` | 条件语句用于基于不同的条件来执行不同的动作 `switch` 语句用于基于不同的条件来执行不同的动作       |
|           | 循环语句   | `for for/in while do/while`                                                               | 循环可以将代码块执行指定的次数                                                                   |
| JS 函数   | 无参数函数 | `function funcName() { 代码．．． }`                                                      | 函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块                                       |
|           | 有参数函数 | `function funcName(var1,var2,...,varX) { 代码．．． }`                                    |                                                                                                  |
|           | 返回值函数 | `function prod(a,b){ x=a*b; return x }`                                                   |                                                                                                  |
| JS 事件   |            |                                                                                           | 事件是可以被 `JavaScript` 侦测到的行为                                                           |
| JS 异常   | 捕获异常   | `try{ //在此运行代码}catch(err){ //在此处理错误}`                                         | `try...catch` 的作用是测试代码中的错误                                                           |
|           | 抛出异常   | `throw(exception)`                                                                        | `throw` 声明的作用是创建 `exception`（异常或错误）                                               |
| JS 字符   | 特殊字符   | `\' \" \& \\ \n \r \t \b \f`                                                              | 在 `JavaScript` 中使用反斜杠来向文本字符串添加特殊字符                                           |
| JS 方针   | 注意事项   |                                                                                           | `JavaScript` 对大小写敏感 `JavaScript` 会忽略多余的空格 在文本字符串内部使用反斜杠对代码进行折行 |

<!-- more -->

## JS 对象

| JS 对象        | 属性 方法                                                                                                                                                                                   | `document.write(txt.length)`<br /> `document.write(str.toUpperCase())`                                                                                                                                                | 属性指与对象有关的值 方法指对象可以执行的行为（或者可以完成的功能）                                                                                                                                                                                                                                                                                                                                                                                          | 对象只是一种特殊的数据。对象拥有属性和方法                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
|                | 字符串对象<br /> 日期对象<br /> 数组对象<br /> 逻辑对象<br /> 算数对象<br /> 正则对象<br /> --------<br /> BOM 对象<br /> -<br />-<br />-<br />-<br />-<br /> --------<br /> DOM 对象<br /> | `String`<br /> `Date`<br /> `Array`<br /> `Boolean`<br /> `Math`<br /> `RegExp`<br /> --------<br /> `Window`<br /> `Navigator`<br /> `Screen`<br /> `History`<br /> `Location`<br /> --------<br /> `Document`<br /> | 字符串对象用于处理已有的字符块<br /> 日期对象用于处理日期和时间<br /> 数组对象的作用是：使用单独的变量名来存储一系列的值<br /> Boolean（逻辑）对象用于将非逻辑值转换为逻辑值（true 或者 false）<br /> Math（算数）对象的作用是：执行常见的算数任务<br /> RegExp 对象用于规定在文本中检索的内容<br /> --------<br /> -<br />-<br />-<br />-<br /> --------<br /> 除了内置的 JavaScript 对象以外，你还可以使用 JavaScript 访问并处理所有的 HTML DOM 对象<br /> |                                                                                                              |
| 创建对象       | 属性<br /> 方法                                                                                                                                                                             | 对象名.属性名<br /> 对象名.方法名                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                                              |
| 创建对象的方法 | 1. 创建对象的实例<br /> -<br />-<br /> 2. 创建对象的模板<br />                                                                                                                              | 定义对象<br /> 添加属性<br /> 添加方法<br /> 定义对象结构<br /> 分配内容<br /> 添加方法<br />                                                                                                                         | `personObj=new Object()`<br /> `personObj.name="John"`<br /> `personObj.sleep()`<br /> `function person(name)`<br /> `{ this.name=name }`<br /> `myFather=new person("John")`<br /> `document.write(myFather.name)`<br />                                                                                                                                                                                                                                    | 有多种不同的办法来创建对象<br /> 一旦拥有模版，你就可以创建新的实例<br /> 方法只是依附于对象的函数而已<br /> |

## JS 高级

1. JavaScript 的核心 ECMAScript 描述了该语言的语法和基本对象；
2. DOM 描述了处理网页内容的方法和接口；
3. BOM 描述了与浏览器进行交互的方法和接口。

![javascript](/blog/images/javascript1.png)

ECMAScript 仅仅是一个描述，定义了脚本语言的所有属性、方法和对象。
DOM（文档对象模型）是 HTML 和 XML 的应用程序接口（API）。

### 操作 HTML 元素

如需从 JavaScript 访问某个 HTML 元素，您可以使用 `document.getElementById(id)` 方法。
请使用 "id" 属性来标识 HTML 元素

### JavaScript 数组

创建数组

```javascript
var cars = new Array();
cars[0] = "Audi";
cars[1] = "BMW";
cars[2] = "Volvo";
```

或者

```javascript
var cars = new Array("Audi", "BMW", "Volvo");
```

或者

```javascript
var cars = ["Audi", "BMW", "Volvo"];
```

### JavaScript 对象

对象由花括号分隔。
在括号内部，对象的属性以名称和值对的形式 (name : value) 来定义。
属性由逗号分隔：

```javascript
var person = { firstname: "Bill", lastname: "Gates", id: 5566 };
```

可以换行

```javascript
var person = {
  firstname: "Bill",
  lastname: "Gates",
  id: 5566,
};
```

对象寻址（引用）：

```javascript
name = person.lastname;
name = person["lastname"];
```

### 声明变量类型

当您声明新变量时，可以使用关键词 "new" 来声明(指定)其类型：

```javascript
var s = new String(); // 声明一个字符串类型变量
var n = new Number(); // 声明一个数字类型变量
var b = new Boolean(); // 声明一个布尔类型变量
var a = new Array(); // 声明一个数组类型变量
var o = new Object(); // 声明一个对象类型变量
```

JavaScript 变量均为对象。当您声明一个变量时，就创建了一个新的对象。
在 JavaScript 中，对象是拥有属性和方法的数据。
个人理解：属性就是一个对象的静态值，方法就是一个对象的行为序列;
汽车的属性：

```javascript
car.name=Fiat
car.model=500
car.weight=850kg
car.color=white
```

汽车的方法：

```javascript
car.start();
car.drive();
car.brake();
```

#### 访问对象的属性

访问对象属性的语法是：
`objectName.propertyName`

#### 访问对象的方法

您可以通过下面的语法调用方法：
`objectName.methodName()`

函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块。

### JavaScript 函数语法

函数就是包裹在花括号中的代码块，前面使用了关键词 function：

```javascript
function functionName() {
  // 这里是要执行的代码
}
```

当调用该函数时，会执行函数内的代码。
通过使用 return 语句就可以实现带有返回值的函数。
在使用 return 语句时，函数会停止执行，并返回指定的值。

### JavaScript 变量的生存期

JavaScript 变量的生命期从它们被声明的时间开始。
局部变量会在函数运行以后被删除。
全局变量会在页面关闭后被删除。

### 条件运算符

JavaScript 还包含了基于某些条件对变量进行赋值的条件运算符。
语法

```javascript
variablename = condition ? value1 : value2;
```

例子

```javascript
greeting = visitor == "PRES" ? "Dear President " : "Dear ";
```

如果变量 visitor 中的值是 "PRES"，则向变量 greeting 赋值 "Dear President "，否则赋值 "Dear"。

### 不同类型的循环

JavaScript 支持不同类型的循环：

- `for` - 循环代码块一定的次数
- `for/in` - 循环遍历对象的属性
- `while` - 当指定的条件为 true 时循环指定的代码块
- `do/while` - 同样当指定的条件为 true 时循环指定的代码块

## 内存模型

|              | 简化                                           | 限制                                   |                                                                                                                                                                                                                                              |     |
| ------------ | ---------------------------------------------- | -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| 引用计数算法 | 对象是否不再需要 -> 对象有没有其他对象引用到它 | 循环引用                               |                                                                                                                                                                                                                                              |     |
| 标记清除算法 | 对象是否不再需要 -> 对象是否可以获得           | 那些无法从根对象查询到的对象都将被清除 | 这个算法假定设置一个叫做根（root）的对象（在 Javascript 里，根是全局对象）。<br />垃圾回收器将定期从根开始，找所有从根开始引用的对象，然后找这些对象引用的对象……从根开始，<br />垃圾回收器将找到所有可以获得的对象和收集所有不能获得的对象。 |     |

### 参考

- http://www.ibm.com/developerworks/web/library/wa-memleak/
- http://msdn.microsoft.com/en-us/magazine/ff728624.aspx
- https://developer.mozilla.org/en-US/docs/Mozilla/Performance

## 其他

```javascript
window.innerHeight; // 获取窗口高度
```

```javascript
$(document).height(); // 返回文档高度（当前显示的高度）
```

```javascript
$(document).scrollTop(); // 返回滚动条与顶部的距离,在最上部时为0
$(document).height() - window.innerHeight; // 在最下部时
```

```javascript
$(document).scrollTop($(document).height() - window.innerHeight);
```

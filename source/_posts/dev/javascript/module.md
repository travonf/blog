---
title: JavaScript Module
date: 2008-09-03 09:00:00
updated: 2008-09-03 09:00:00
tags: "javascript"
categories: "Develop"
---

## 编译时和运行时的区别

JavaScript 声明有两种：

|          |                       | 编译时                                     | 运行时     |
| -------- | --------------------- | ------------------------------------------ | ---------- |
| 声明变量 | `var`、`const`、`let` | 开辟内存空间指向变量名，赋值为 `undefined` | 变量初始化 |
| 声明方法 | `function`            | 开辟内存空间，赋值为函数体                 |            |

| 名称      | 代表      | 定义/导出                                             | 加载/导入                    |
| --------- | --------- | ----------------------------------------------------- | ---------------------------- |
| AMD       | RequireJS | `define(id?, dependencies?, factory)`                 | `require([module], factory)` |
| CMD       | SeaJS     | `define(factory)` <br />`define(id?, deps?, factory)` | `require(id)`                |
| CommonJS  |           | `module.exports` <br />`exports`                      | `require`                    |
| ES Module | ECMA      | `export` <br />`export default`                       | `import`                     |

<!-- more -->

## 特点

### CommonJs

1. CommonJS 模块是对象，是运行时加载，运行时才把模块挂载在 exports 之上（加载整个模块的所有），加载模块其实就是查找对象属性。
2. CommonJS 模块输出的是一个值的拷贝
3. CommonJS 模块是运行时加载

### ES Module

1. ES Module 不是对象，是使用 export 显示指定输出，再通过 import 输入。此法为编译时加载，编译时遇到 import 就会生成一个只读引用。等到运行时就会根据此引用去被加载的模块取值。所以不会加载模块所有方法，仅取所需。
2. ES6 模块输出的是值的引用
3. ES6 模块是编译时输出接口

## CommonJS 与 AMD/CMD 的差异

`AMD`/`CMD` 是 `CommonJS` 在浏览器端的解决方案。
`CommonJS` 是同步加载（代码在本地，加载时间基本等于硬盘读取时间）。
`AMD`/`CMD` 是异步加载（浏览器必须这么干，代码在服务端）

## AMD 与 CMD 的差异

`AMD` 是提前执行（RequireJS2.0 开始支持延迟执行，不过只是支持写法，实际上还是会提前执行），
`CMD` 是延迟执行
`AMD` 推荐依赖前置，
`CMD` 推荐依赖就近

## 前端工程模块化

1. javascript 模块化方案

* CommonJS

 CommonJS 对模块的定义十分简单，主要包括模块定义、模块引用和模块标示3个部分。

(1) 模块引用

```javascript
  var math = require('math')
```
> 在 commonJS规范中，存在一个 `require()` 方法，这个方法接受模块标识，以此引入一个模块的API到当前上下文中。

(2) 模块定义


***注意***
> CommonJS 不适用于浏览器端模块，因为其采用的是`同步加载`方式
> Node 基于CommonJS的Modules规范实现了一套非常易用的模块系统。

* AMD (Asynchronous Module Defination)

日后总结：[参考这里](http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html)

* ES6 的 Module

日后总结：[参考这里](http://es6.ruanyifeng.com/#docs/module)

*** 注意 ***
> ES6 模块的设计思想是尽量的静态化，使得在编译时就能确定模块的依赖关系，以及输入和输出的变量。AMD和CommonJS模块，都只能在运行时确定这些东西。
> AMD和CommonJS属于`运行时加载`，而 ES6 的Module 属于`编译时加载`或者静态加载，

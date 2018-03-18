## 前端工程与模块化
日后整理，参考：

[前端工程-基础篇](https://github.com/fouber/blog/issues/10#issuecomment-138308585)

[前端工程与模块化框架](https://github.com/fouber/blog/issues/4)

[前端工程之模块化](http://fex.baidu.com/blog/2014/03/fis-module/)

###前端工程

前端工程一般经历四个阶段：

（1）库与框架选型
> 根据项目特征进行技术选型

（2）简单构建优化
> 对代码进行压缩、校验，之后以页面为单位进行简单的资源合并。常见的构建工具：grunt和gulp

（3）JS和CSS的模块化开发
> JS的模块化方案一般有 AMD、Common.JS、ES6 Module等，CSS的模块化开发一般是在LESS、SASS、Stylus等预处理的import/mixin特性支持下实现的。

（4）组件化开发与资源管理
> 前端相比于其他的软件开发，在基础架构上更加迫切的需要组件化开发与资源管理，而解决资源管理的一般思路：一个通用的资源表生成工具和基于表的资源加载框架。

* 组件化开发

分治的确是非常重要的工程优化手段，前端作为一种GUI软件，光有JS/css的模块化还不够，对于UI组件的分治也有同样迫切的需求。

![](https://github.com/buptwangsong/FE-Knowledge-collection/blob/master/img/components.png)

如上图，这是我所信仰的web组件化开发理念。解释如下：

* 页面上每个独立的可视/可交互区域视为一个组件

* 每个组件对应一个工程目录，组件所需的所有资源都在这个目录下就近维护

* 由于组件具有独立性，因此组件和组件之间可以自由组合。

* 页面不过是组件的组合，负责组合组件形成功能完整的界面

* 当不需要某个组件，或者替换某个组件时，可以整个目录删除/替换




### 前端模块化

前端模块化是能够独立提供功能且能够复用的模块化代码，根据复用方式的不同，分为Template模块、JS模块、CSS模块。

> CSS 模块是最简单的模块，他只涉及CSS代码和HTML代码

> JS 模块稍复杂， 它涉及JS代码、CSS代码和HTML代码，一般，JS组件可以封装CSS组件的代码

> Template模块涉及的代码最多，可以综合处理Javascript/css/html各种模块化资源，一般情况下，Template会将JS资源封装生私有的JS模块，将CSS资源封装成私有的CSS模块

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

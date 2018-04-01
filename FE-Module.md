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

```javascript
 //math.js
 
 exports.add = function(){
   var sum = 0,
   for(var i = 0; i<arguments.length; i++){
    sum += arguments[i];
   }
   return sum;
 }
```
> 根据`CommonJS`规范，一个单独的文件就是一个模块，每一个模块都有一个独立的作用域，也就是说，模块内的变量无法被模块外的代码读取，除非使用`exports`对象导出。

> 在模块中，上下文提供了`require()`方法来引入外部模块。对应引入的功能，上下文提供了`exports`对象用于导出当前模块的方法或者变量，并且它是唯一的导出的出口。在模块中还有一个`module`对象，它代表模块自身，`exports`对象就是`module`对象的属性。

> 模块的定义十分简单，意义在于将类聚的方法和变量等限定在私有作用域中，同时支持引入和导出功能以顺畅的连接上下游依赖。

（3）模块标识

> 模块标识实际上就是传递给`require()`方法的参数，它必须是符合小驼峰命名规则的字符串。


***注意***
> CommonJS 不适用于浏览器端模块，因为其采用的是`同步加载`方式
> Node 基于CommonJS的Modules规范实现了一套非常易用的模块系统。

* AMD (Asynchronous Module Defination)

日后总结：[参考这里](http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html)

> AMD，即异步模块定义。它采用异步方式加载模块，模块的加载不影响它后面语句的执行，所有依赖这个模块的操作都定义在一个回调函数里。等模块加载完成后，这个回调函数才会执行。

> AMD规范的javascript 库 `require.js`

**require.js**
主要解决了一下两个问题：

> 1. 异步下载js 文件，避免页面失去响应。

> 2. 管理模块之间的依赖性，便于编写和维护


(1)模块定义

```javascript
 difine(id?, dependencies?, factory);

```
> `id`：可选参数，用来定义模块的标识，如果没有提供该参数，则使用文件名。

> `dependencies`：当前模块依赖的模块名称数组

> `factory`：工厂方法，模块初始化要执行的函数或者对象，如果为函数，它只会被执行一次，如果是对象，该对象应该是模块的输出。

```javascript
 define(['moduleA', 'moduleB', 'moduleC'], function(moduleA, moduleB, moduleC){
   // some code here
   
   return {
    // ... 抛出对象对外接口
   }
 })
```

（2）模块引用

```javascript

 require(['moduleA', 'moduleB', 'moduleC'], function(moduleA, moduleB, moduleC){
   //some code..
 });

```




* ES6 的 Module

日后总结：[参考这里](http://es6.ruanyifeng.com/#docs/module)

*** 注意 ***
> ES6 模块的设计思想是尽量的静态化，使得在编译时就能确定模块的依赖关系，以及输入和输出的变量。AMD和CommonJS模块，都只能在运行时确定这些东西。
> AMD和CommonJS属于`运行时加载`，而 ES6 的Module 属于`编译时加载`或者静态加载，

* CMD （Common Module Defination）

日后总结，[参考这里](https://www.cnblogs.com/futai/p/5258349.html)

CMD是在国内发展起来的，就像AMD有require.js， CMD有个浏览器端的实现Sea.js。 RequireJS和SeaJS要解决的问题是一样的，只不过两者在模块定义方式和模块加载时机上有所区别。

(1)模块定义

```javascript
 define(id?, deps? factory);
```
> 参数的意义与`AMD`相同。

> `sea.js`推崇一个文件一个模块。

> `CMD`推崇依赖就近，因此一般不再`define`函数中写依赖，也就是说，省略`deps`参数。

> `factory` 方法有三个参数：

```javascript
 factory(require, exports, module)

```

>> `require(id)`：用于在`factory`函数中引入其他模块的对外接口

>> `exports`： 是一个对象，用来向外提供模块接口。

>> `module`：是一个模块，指的是当前对象。

```javascript
// 定义模块  myModule.js
define(function(require, exports, module) {
  var $ = require('jquery.js')
  $('div').addClass('active');
  
  exports = {
   //抛出模块对外接口
  }
});

// 加载模块
seajs.use(['myModule.js'], function(my){

});
```

***AMD VS CMD

> 两者最明显的区别就是，在模块定义时对依赖的处理不同

>> AMD推崇依赖前置，在定义模块的时候就要声明其依赖的模块

>> CMD推崇就近依赖，只有在用到某个模块的时候再去require

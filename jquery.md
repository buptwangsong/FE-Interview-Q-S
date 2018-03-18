## jQuery核心原理的理解

日后总结，参考这里：

[浅谈jquery实现原理](http://blog.csdn.net/zhouziyu2011/article/details/70256659)

[jquery的实现原理及核心](https://www.cnblogs.com/Scar007/p/7718066.html)

1. 外层沙箱

```javascript
  (function(window, undefined){
    // 用一个函数域包裹起来就是所谓的沙箱
    // 在这里面用var定义的变量都属于这个函数域的局部变量，避免污染全局变量
    // 把当前沙箱需要的外部变量通过函数参数引进来
    // 只要保证参数对内提供接口的一致性，可以随意替换这个传进来的参数
    
    window.jQuery = window.$ = jQuery;
  })(window)
```

> jQuery 将源码封装在一个匿名的自执行函数里，有助于防止污染全局作用域。

> 通过传入`window`对象参数，可以将window作为局部变量使用。好处是，当jQuery访问window对象的时候，就不需要将作用域链回退到顶层作用域了，从而可以更快的访问window对象

> jQuery 将一些原型属性和方法封装在了 jQuery.prototype中，为了缩短命名，又赋值给jQuery.fn，这是一种很形象的写法。

> jQuery 实现的链式调用可以节约代码，通过在方法最后 return this 来实现。

2. jQuery 无new 构造

日后整理

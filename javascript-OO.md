## 面向对象的程序设计
> 深刻理解对象、对象创建、原型链及继承

### 创建对象

1. 对象字面量

```javascript
  var person = {
    name: "Nicholas",
    age : 29,
    job : "Doctor",
    sayName : function(){
      alert(this.name);
    }
  }；
```

> 对象字面量方式创建对象，本质上一种单例

>> 关于单例模式，多说两句：

>>> 单例模式的定义及特点：保证一个类仅有一个实例，且提供一个访问它的全局访问点。

>>> 一个使用闭包创建单例的例子，如下

```javascript
  var Singleton = function(name){
    this.name = name;
  }
  
  Singleton.prototype.sayName = function(){
    alert(this.name);
  }
  
  Singleton.getInstance = (function(name){
    var instance;
    return function(name){
      if(!instance){
        instance = new Singleton(name);
      }
      return instance;
    };
  })(name)
```
>>> 更多细节，[参考这里](http://blog.csdn.net/yisuowushinian/article/details/52003127)
> 这种方式的缺点是，使用同一个接口创建很多对象，会产生大量重复的代码。

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

2. 工厂模式

```javascript
  function（name, age, job）{
    var obj = new Object();
    obj.name = name;
    obj.age  = age;
    obj.job  = obj;
    obj.sayName = function(){
      alert(this.name);
    };
  }
```
> 缺点：无法识别对象

3. 构造函数模式

```javascript
  function Person(name, age, job){
    this.name = name;
    this.job  = job;
    this.age  = age;
    this.sayName = function(){
      alert(this.name);
    };
  }
  
  var person1 = new Person("Nicholas", 19, "Doctor");
  
```

> 使用 `new`操作符调用构造函数来创建对象，发生的过程：

(1) 创建一个新对象： `new Object()`;

(2) 将构造函数的作用域赋给该对象，即函数内的`this`指向该对象；

(3) 执行构造函数内的代码，给该对象添加属性

(4) 将该对象返回。

> 新创建的对象内部都有一个`constructor`属性，该属性最初是用来识别对象的。

> 缺点：属性无法得到复用，比如函数。

4. 原型模式

```javascript
  function Person(){};
  
  Person.prototype.name = "Nicholas";
  Person.prototype.age  = 19;
  Person.prototype.job  = "Doctor";
  Person.prototype.sayName = function(){
    alert(this.name);
  }
```

> `原型`的用途是包含了特定类型的所有实例所共享的属性和方法。

> 缺点：属性被所有实例共享，比如引用类型的属性

5. 组合使用构造函数模式和原型模式

```javascript
  function Person(name, age, job){
    this.name = name;
    this.age  = age;
    this.job  = job;
  }
  
  Person.prototype = {
    constructor : Person,
    sayName = function(){
      alert(this.name);
    }
  };
  
```

> 创建自定义类型最常用的方式：利用构造函数定义实例属性，而使用原型定义共享属性和方法。

6. 动态原型模式

```javascript
  function Person(name, age, job){
    this.name = name;
    this.age  = age;
    this.job  = job;
    
    if(typeof this.sayName != "function"){
      this.sayName = function(){
        alert(this.name);
      }
    }
  }
  
  var person = new Person("Nicholas", 19, "Doctor");
```
7. 寄生构造函数模式

```javascript
  function Person(name, age, job){
    var o = new Object();
    o.name = name;
    o.age  = age;
    o.job  = job;
    o.sayName = function(){
      alert(this.name)
    };
    
    return o;
  }
  
  var person = new Person("Nicholas", 19, "Doctor");
```
>除了需要用`new`来调用外，该模式与工厂模式是一样的。

> 构造函数在不返回值（准确说，应该是在不返回引用类型值）的情况下，默认会返回新对象实例。

> 寄生构造函数模式可以在特殊情况下为用来为对象创建构造函数。比如，假设我们想创建一个具有额外方法的特殊数组，由于不能直接修改Array的构造函数和原型，因此可以使用该模式：

```javascript
  function SpecialArray(){
    var arr = new Array();
    arr.push.apply(arr, arguments);// 这句也可以这么写：arr.push(...arguments)
    
    arr.toPipedString = function(){
      return this.join("|");
    };
    
    return arr;
  }
```

8. 稳妥构造函数模式

```javascript
  function(name, age, job){
    var o = new Object();
    //在这里定义私有变量和函数
    var name = name;
    var age  = age;
    var job  = job;
    
    o.sayName = function(){
      alert(name);
    };
    
    return o;
  }
  
  var person = Person("Nicholas", 19, "Doctor");
```

> 所谓的`稳妥对象`是指，没有公共属性，方法也不引用this对象。稳妥对象最适合在一些安全环境中，或者防止数据被其它应用程序改动时使用。

9. class

```javascript
  class Person {
    constructor(name, age, job){
      this.name = name;
      this.age  = age;
      this.job  = job;
    }
    
    sayName(){
      alert(this.name);
    }
  }

```

> ES5中的构造函数，相当于ES6 Class中的`constructor`




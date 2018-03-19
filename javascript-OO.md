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

> 关于ES6 class 的更多细节，参考[这里](http://es6.ruanyifeng.com/#docs/class)

### 继承

1. 原型链

```javascript
function SuperType(){
  this.property = true;
}

SuperType.prototype.getSuperValue = function(){
  return this.property;
}

function SubType(){
  this.property = false;
}

//继承 SuperType
SubType.prototype = new SuperType();

SubType.prototype.getSubValue = function(){
  return this.property;
}
```

> javascript的继承主要是通过原型链来实现。原型链的构建是通过将一个类型的实例赋值给另一个类型的原型实现的。

> 实例属性名字的解析是沿着原型链进行的，类似于变量沿着作用域链进行标示符解析。

> 缺点：

>> 对象实例共享所有继承的属性和方法，因此，不适宜单独使用；

>> 字面量重写原型会中断继承关系

>> 创建子类型的实例时，不能向超类型的构造函数传递参数。

2. 借用构造函数

```
function SuperType(){
  this.property = true;
}

function SubType(){
  SuperType.call(this); //继承了SuperType
}

```

> 在子类型的构造函数内调用超类型的构造函数

> 缺点：属性无法复用

3. 组合继承

```javascript
  function SuperType(name){
    this.name = name;
  }
  
  function SubType(name, age){
    SuperType.call(this, name);//借用构造函数，实现对实例属性的继承
    this.age = age;
  }
  
  SubType.prototype = new SuperType(); //借用原型链实现对原型属性和方法的继承
  SubType.prototype.constructor = SubType;
  SubType.prototype.sayAge = function(){
    alert(this.age);
  }
```

> 组合继承是最常用的继承方法：使用原型链实现对原型属性和方法的继承，而通过借用构造函数实现对实例属性的继承。

4. 原型式继承

```javascript
  function Object(o){
    function F(){};
    F.prototype = o;
    
    return new F();
  }
    
```

> 基本思想：借助原型基于已有的对象创建新对象，同时还不必创建自定义类型。

> 本质上是对传入的对象`o`执行了一次浅复制

> ES5 定义了`Object.create()`方法来规范化原型式继承

5. 寄生式继承

```javascript
  function createAnother(o){
    var clone = Object(o);
    clone.sayHi = function(){
      alert("HI")
    };
    return clone;
  }
```

> 基本思路与继承构造函数和工厂模式类似，即创建一个函数用于封装继承过程，在函数内部以某种方式来加强对象，最后返回。

> 在主要考虑对象，而不是自定义类型及构造函数的情况下，该模式很有用。

6. 寄生组合式继承

```javascript
function inheritPrototype(subType, superType){
  var prototype = Object.create(superTyep);
  prototype.constructor = subType;
  subType.prototype = prototype;
}

function SuperType(name){
  this.name = name;
}

function SubType(name, age){
  SuperType.call(this, name);
  this.age = age;
}

inheritPrototype(SubType, SuperType);

SubType.prototype.sayAge = function(){
  alert(this.age);
}

```

> 寄生组合继承解决了组合继承中超类型的构造函数调用两次的问题。

> 基本思路：不为子类型的原型调用超类型的构造函数，而仅仅传递超类型原型的一个副本。

7. class 继承

```javascript
  class Rectangle{
    constructor(x, y){
      this.x = x;
      this.y = y;
    }
    
    area(){
      return this.x*this.y
    }
  }
  
  class ColorRectangle extends Rectangle{
    constructor(x, y, color){
      super(x,y);
      this.color = color;
    }
    
    sayColor(){
      alert(this.color);
    }
  }
```

> 关于 class 继承的更多细节参考[这里]（http://es6.ruanyifeng.com/#docs/class-extends）

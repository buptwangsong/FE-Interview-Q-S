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

>> 关于单例，多说两句：

> 这种方式的缺点是，使用同一个接口创建很多对象，会产生大量重复的代码。

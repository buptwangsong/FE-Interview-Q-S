## javascript 的一些常用API

### 对象

1. Object.getPrototypeOf()

* 获取对象的原型

* 判断一个类是否继承了另一个类

2. objectA.isPrototypeOf(objectB)

* 判断 A是否是B的原型对象，如果 objectB的[[prototype]]指向objectA则返回true

3. objectA.hasOwnProperty(attr)

* 检测一个属性是在实例中，还是在原型中

4. attr in objectA

* attr 只要是 objectA 的属性，则返回true

5. Object.keys(obj)

* 返回实例的所有可枚举的属性数组。


***确定原型和实例的关系***

(1) instanceOf

(2) isPrototypeOf

6. Object.create(obj, descriptor)

* 基于已有对象创建新对象，并利用第二个参数对其加强。

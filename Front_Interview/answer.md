## 我的答案

### section one
来源这里[自己写的面试题，自己想的答案](https://segmentfault.com/a/1190000014028922)

1. 面向对象

> 需求：定义`我吃火锅`

1.1 面向过程的变成思想，实现：`动作（我，火锅）`
```javascript
  // 实现上述需求
```

1.2 用面向对象思想，改写上述需求。

```javascript
  //  代码实现
```

2. 预解析

> 要求，根据以下代码。写出结果

*question 1.

```javascript
  alert(a)
  a();
  var a=3;
  function a(){
    alert(10)
  }   
  alert(a)
  a=6;
  a();  
```

*question 2

```javascript
  alert(a)
  a();
  var a=3;
  var a=function(){
      alert(10)
  }   
  alert(a)
  a=6;
  a(); 
```

3. 事件委托

> 要求：一个简单的需求，比如想给ul下面的li加上点击事件，点击哪个li，就显示那个li的innerHTML。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <ul id="ul-test">
            <li>0</li>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li>4</li>
            <li>5</li>
            <li>6</li>
            <li>7</li>
            <li>8</li>
            <li>9</li>
        </ul>
    </body>
</html>

```

4. DOM操作

> 要求:比如有一个需求，往ul里面添加10个li，如下代码

```html
  <!DOCTYPE html>
  <html>
      <head>
          <meta charset="UTF-8">
          <title></title>
      </head>
      <body>
          <ul id="ul-test">

          </ul>
      </body>
  </html>
```

5. 对象深拷贝
> 要求：要求实现一个函数clone
```javascript
  let obj={
      name:'小明',
      age:24
  }
  let obj1=clone(obj);

```
> 修改obj1，不会影响obj.

6. 如果在设计中使用了非标准字体，该如何实现。

7. 在项目开发上，知道哪些优化方法，提升web性能，减少页面加载时间，代码质量和可读性等方面。

8. 列举ES6 常用的一些特性

9. DIV + css排版的时候，从页面渲染和代码可读性角度，应该注意什么？

10. 说下对模块化开发的理解，以及模块化开发的好处？


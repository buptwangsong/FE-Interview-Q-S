## 我的答案

### Section one
来源这里[自己写的面试题，自己想的答案](https://segmentfault.com/a/1190000014028922)

1. 面向对象

> 需求：定义`我吃火锅`

1.1 面向过程的变成思想，实现：`动作（我，火锅）`
```javascript
  const eat = function(name, dishes){
    console.log(`${name} eat ${dishes}`);
  }
```

1.2 用面向对象思想，改写上述需求。

```javascript
  function Person(name){
    this.name = name;
  }
  
  Person.prototype.eat = function(dishes){
    console.log(`${this.name} eat ${dishes}`);
  }
  
```

2. 预解析

> 要求，根据以下代码。写出结果

*question 1.

```javascript
  alert(a)  // function a(){alert(10);}
  a();      // 10
  var a=3;
  function a(){
    alert(10);
  }   
  alert(a) //3
  a=6;
  a();  // Error a is not a function
```

*question 2

```javascript
  alert(a) // undefined
  a(); // Error a is not a function
  var a=3; 
  var a=function(){
      alert(10)
  }   
  alert(a) // function(){alert(10)}
  a=6;
  a(); // Error a is not a function
```
***解析***
> 1. 变量声明提升
> 2. 函数声明优先于变量声明


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
        // 一下是作答部分：
        <scrip>
          
          const eventUtil = {
            addEventHandler: function(element, type, handler){
              if(element.addEventListener){
                  element.addEventListener(type, handler, false);
              } else if(element.attachEvent){
                  element.attachEvent("on"+type, handler);
              } else {
                  element["on"+type] = handler;
              }
            }
  
            removeEventHandler: function(element, type, handler){
                // some code ...
            }
  
            getEvent: function(event){
              return event ? event : window.event;
            }
  
            getTarget: function(event){
              return event.target || event.srcElement;
            }
          }
          
  
  
          let ulElem = document.getElementById("ul-test");
          
          eventUtil.addEventHandler(ulElem, click, handler);
  
          const handler = function(e){
              let event = eventUtil.getEvent(e);
              let target = eventUtil.getTarget(event);
  
              if(target.tagName.toLowCase() === "li"){
                console.log(target.innerHtml);
              }            
    
          }
 
        </script> 
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
  
          // 代码实现如下
          <script>
            let _html = '';
            for(let i = 0; i<10; i++){
              _html += `<li>${i}</li>`;                     
            }
            let ulElem = document.getElementById("ul-test");
            ulElem.innerHtml = _html;
          </script>
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

> 代码实现如下：
```javascript
  const clone = function(obj){
    if(!obj && (typeof obj !== "object")){
      return obj;
    }
    
    let buffer = obj.constructor === "Object" ? {} : [];
    
    for(var key in obj){
      buffer[key] = (obj[key] && typeof obj[key] === "object") ? clone(obj[key]) : obj[key];
    }
    
    return buffer;
  }


```



6. 如果在设计中使用了非标准字体，该如何实现。

> 所谓的`标准字体`是指，一般机器上都会有的，即使没有，也可以用默认字体代替的字体。

**实现方法**
> 用图片代替

> 用`web fonts`在线字库，比如 `font awesome`

> 使用`css3`的@font-face,定义自己喜欢的任意字体。

```css
  @font-face{
    font-family: myFirstFont;
    src: url('Sansation_Bold.ttf'),
         url('Sansation_Bold.eot'); /* IE9+ */
    font-weight: bold;
  }
```

7. 在项目开发上，知道哪些优化方法，提升web性能，减少页面加载时间，代码质量和可读性等方面。

**web性能优化**
> 1. 减少HTTP请求次数：合并文件，使用css sprite.

> 2. 使用CDN，减少http请求的响应时间

> 3. 启用Gzip, 这只 request header： `Accept-Encoding：gzip`

> 4. 启用缓存：`Expires`/`Etag`/`Cache-Control: max-age`

> 5. 减少DNS查询， 配置request header：`Connection: Keep-Alive`

> 6. css文件放在`header`标签内，javascript 文件放在`body`标签底部。

> 7. 避免 css expression

> 8. 尽量使用外联css/js 文件，便于缓存

> 9. 缓存AJAX的请求结果。缓存DOM的查询结果。

**代码层面**

> 1. 尽量避免使用`iframe`

> 2. 尽量避免使用`with`，会延长作用于链

> 3. 尽量避免全局查找。

> 4. 尽量避免使用全局变量。

> 5. 尽量使用`setTimeout`代替`setInterval`，避免页面失去响应。

> 6. 变量命名尽量有意义。

> 7. 适当的注释

> 8. 尽量避免写出巨大的函数

> 9. 尽量避免代码强耦合，比如`swith`

> 10. 尽量模块化


8. 列举ES6 常用的一些特性

> 1. 模板字符串

> 2. let/const 声明变量，引入块级作用域

> 3. 箭头函数

> 4. 函数默认参数，不定参数

> 5. `for...of...`遍历具有`iterator`接口的数据结构的成员

> 6. 将`promise`纳入标准，统一了用法，提供了原生的`promise`对象。

> 7. 引入`symbol`类型，避免命名冲突。

> 8. 引入了`class`（类）概念，作为构建对象的模板，并定义了继承方法。

> 9. 定义了`module`


9. DIV + css排版的时候，从页面渲染和代码可读性角度，应该注意什么？

> 尽量使用语义化的标签。

> 类和id的命名应有意义，且统一规范

> 避免使用`css expression`

> css 避免嵌套层次太深

> 尽量不要使用内嵌样式、行内样式

> 尽量在`head`引入CSS文件

> 不要使用`@import`，它会导致CSS文件无法并行下载。
>> 使用`@import`引用的文件，只有在引用它的那个CSS文件下载、解析后，浏览器才知道还有一个css文件需要下载。


10. 说下对模块化开发的理解，以及模块化开发的好处？


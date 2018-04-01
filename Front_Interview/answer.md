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

// 另一种实现方法：

const clone = function(obj){
  return JSON.parse(JSON.stringify(obj));
}
// 存在的问题，obj中`undefined`和函数将会被忽略，应为，这两种类型不是JSON的合法数据类型。

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
>> 过度的嵌套会使得代码臃肿、沉余、复杂。CSS文件体积过大，造成性能浪费，影响页面的渲染速度。而且过度依赖于HTML的结构。维护起来极度麻烦。

> 尽量不要使用内嵌样式、行内样式

> 图片设置`width`和`height`, 这样保证在网速比较差或者其它原因无法加载图片的时候，页面布局不会乱。

> 图片预加载
>> 将`#preloader`标记的这个元素加入到文档中，就可以通过`css`的`background`属性将图片加载到屏幕之外的地方。只要这些图片的路径保持不变，当他们再web页面的其他地方被调用时，浏览器就会在渲染的过程中使用预加载的图片。

```css
  #preloader{
    background: url(image1.jpg) norepeat, url(image2.jpg) norepeat, url(image3.jpg) norepeat;
    width: 0;
    height: 0;
    visibility: hidden;
  }

```

>> 这里有个问题，预加载的图片会和页面中的其它资源一起加载，增加了页面的首屏事件。因此，需要用js控制。

```javascript
  const preloader = function(urlArr, elem){
    let bgText = '';
    for(let i = 0, len = urlArr.length; i < len; i++){
      bgText += `url(${urlArr[i]}) norepeat`;
    }
    
    elem.style.background = bgText.substring(0, -1);
  }
  
  window.onload = function(){
    preloader(['image1.jpg', 'image2.jpg', 'image3.jpg'], document.getElementById('preloader'));
  }
  
  
```

> 尽量在`head`引入CSS文件
>> 浏览器只有在所有的`stylesheets`下载完成之后，才开始渲染整个页面。如果将css文件放在`body`底部，会导致整个页面在某段时间内无样式。


> 不要使用`@import`，它会导致CSS文件无法并行下载,。
>> 使用`@import`引用的文件，只有在引用它的那个CSS文件下载、解析后，浏览器才知道还有一个css文件需要下载。

> 小图标的处理方案：`css sprite`、`base64`、`字体图标`

> 把常用样式封装成公用样式。

> 给`body`样式设置`min-width: 内容宽度`


10. 说下对模块化开发的理解，以及模块化开发的好处？

> 模块化本质上体现的是一种分治思想，将复杂的系统分解成功能单一、高度解耦且可替换的功能模块，系统中某一部分的变化将如何影响其它部分就变得显而易见，使得系统更容易维护。

> 前端模块化并不仅仅指的是javascript的模块化，因为一个页面功能总是需要javascript、css、template三种语言相互组织才行。

> javascript的模块化方案很多，比如`AMD`、`CMD`、`ES6 Module`，还有服务器端js模块化方案`commonJS`.

> CSS的模块化主要是依赖`LESS`、`SASS`等预编译语言的`import`和`mixin`等特性。

> 除此之外，UI组件也应该实现模块化。

> 最终达到的效果是这样的:

>> 1. 页面中每一个独立可视化/可交互区域视为一个组件

>> 2. 每个组件对应一个工程目录，该组件所需要的所有资源都在该目录下就近维护。

>> 3. 组件具有独立性，因此，组件与组件之间可以自由组合。

>> 4. 页面只不过是组件的容器，负责组合组件形成功能完整的页面。

>> 5. 当不需要或者替换某个组件时，可以将整个目录删除或者替换。

**模块化开发带来的好处**
> 模块之间高度解耦，可以协同开发，提升开发效率。同时也方便了代码维护。

> 每个模块都形成了一个独立的作用域，防止变量命名冲突，及污染全局环境。

> 代码可以复用。





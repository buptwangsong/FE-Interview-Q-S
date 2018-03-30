# Javascript Event

### 1. 事件流

> **事件流**描述的是页面中的元素接收事件的顺序。

1.1 事件冒泡

> 事件开始时由最具体的元素（嵌套层次最深的元素）接收，然后逐级向上传播到较为不具体的元素。

1.2 事件捕获

> 事件开始时应该由最不具体的元素接收，然后向下逐渐传播到较为具体的元素。

1.3 DOM2级 事件流

> 规定事件流分为三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段。


### 2. 事件处理程序（绑定事件的几种方式）

2.1 HTML 事件处理程序

> 某个元素支持的每种事件，都可以用一个与事件处理程序同名的HTML特性来指定。这个特性的值应该是能够执行的js代码。

```html

<input type="button" value="Click me" onclick="alert('ok')" />

<input type="button" value="Click me" onclick="showMessage()">

```

> 函数在元素的作用域内执行，也就是说`this`即为目标元素。

> 事件对象`event`作为函数内的一个局部变量存在。


2.2 DOM0 事件处理程序

> 将函数赋值给元素的一个事件处理程序属性。

```javascript

var btn = document.getElementById("myBtn");
btn.onclick = function(){
  alert("ok");
}

```

> 函数在元素的作用域内执行，也就是说`this`即为目标元素。

> 事件对象`event`在不同浏览器下行为具有不一致性。
>> IE 浏览器下，`event`对象作为`window`对象的一个属性存在。
>> 在非IE浏览器下，`event`对象作为一个参数传入事件处理程序中。

> 如果重复给同一个元素的事件处理程序绑定事件，会覆盖。

2.3 DOM2 事件处理程序

* 非IE浏览器
> 非IE浏览器定义了`addEventListener`、`removeEventListener`用于事件的绑定与删除。

```javascript
  var btn = document.getElementById("btn");
  btn.addEventListener("click", handler, false);
  btn.removeEventListener("click", handler, false);

  function handler(e){
    alert("ok");
  }

```

> 函数在元素的作用域内执行，也就是说`this`即为目标元素
> `event`对象作为函数参数传入事件处理程序中。





* IE浏览器
> IE 浏览器定义了`attachEvent`、`detachEvent`用于事件的绑定和删除

```javascript
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", handler);
btn.detachEvent("onclick", handler);

function handler(e){
  alert("ok");
}

```

> 函数在全局作用域内执行，也就是说`this`即为`window`。
> `event`对象作为函数参数传入事件处理程序中。


### 3. 事件对象

3.1 DOM中的事件对象

> `event.preventDefault()`取消事件的默认行为

> `event.stopPropagation()`取消事件的进一步冒泡或捕获

> `event.target` 触发事件的目标

> `event.currentTarget` 事件处理程序绑定的元素，等于`this`

3.2 IE中的时间对象

> `event.returnValue = false` 取消事件的默认行为

> `event.cancelBubble = true` 取消事件冒泡

> `event.srcElement` 触发事件的目标


### 4. 跨浏览器事件对象的实现

```javascript

  const = EventUtil = {
    
    addHandler: function(element, type, handler){
      if(element.addEventListener){
        element.addEventListener(type, handler, false);
      } else if(element.attachEvent){
        element.attachEvent("on"+type, handler);
      } else {
        element["on"+type] = handler;
      }
    },
    
    removeHandler: function(element, type, handler){
      if(element.removeEventListener){
        element.removeEventListener(type, handler, false);
      } else if(element.detachEvent){
        element.detachEvent("on"+type, handler);
      } else {
        element["on"+type] = null;
      },
      
      getEvent: function(event){
        return event ? event : window.event;
      },
      
      getTarget: function(event){
        return event.target || event.srcElement;
      },
      
      preventDefault: function(event){
        if(event.preventDefault){
          event.preventDefault();
        } else {
          event.returnValue = false;
        } 
      },
      
      stopPropagation: function(event){
        if(event.stopPropagation){
          event.stopPropagation();
        } else {
          event.cancelBubble = true;
        }
      }
    }
      
  }

```


### 4. 事件

4.1 UI事件

> `load`事件：当页面完全加载后在`window`上触发，当所有框架都加载完毕后在框架集上面触发；当图片加载完毕后在`<img>`元素上触发；当嵌入的内容加载完毕后`<object>`元素上面触发。

> `unload`事件： 与上面元素对应。

> `error`事件： 当发生`javascript`错误时在`window`上面触发，当无法加载图像时在`<img>`元素上触发，当无法加载嵌入的内容时在`<object>`元素上触发，当有一个或者多个框架无法加载时在框架集上触发。

> `select`事件：当用户选择文本框（`<input>`、`<textarea>`）中的一个或多个字符时触发。

> `resize`事件：当窗口或框架的大小发生变化时在`window`和框架上触发。

> `scroll`事件：当用户滚动带滚动条的元素中的内容时，在该元素上触发。

4.2 焦点事件

> `blur`事件：当元素失去焦点时触发，该事件**不会冒泡**

> `focus`事件：当元素获得焦点时触发，该事件**不会冒泡**

4.3 鼠标与滚轮事件

> `click`/`dbclick`事件。

> `mousedown`/`mouseup`事件.

> `mouseenter`/`mouseleave`事件：当鼠标光标从元素外/内部，首次移动到元素范围之内/外时触发。该事件不冒泡。

> `mouseout`事件：在鼠标指针位于一个元素上方，然后用户将其移入另一个元素时触发。又移入的另一个元素可能位于前一个元素的外部，也可能是这个元素的子元素。该事件冒泡。

> `mouseover`事件：鼠标指针位于一个元素的外部，然后用户将其首次移入另一个元素内部是触发，又移入的元素可能位于前一个元素的外部，也可能是这个元素的子元素。该事件冒泡。

> 坐标位置

>> 客户区坐标：浏览器视口 `event.clientX`, `event.clientY`
>> 页面坐标： 整个页面 `event.pageX`， `event.pageY`。如果页面没有滚动的话，与客户区坐标相同。
>> 屏幕坐标： 真个屏幕 `event.screenX`, `event.screenY`。


* mouseenter, mouseleave, mouseover, mouseout, mousemove
1. mouseenter:在鼠标光标从元素外部首次移动到元素范围之内时触发，事件不冒泡，而且在光标移动到后代元素上时不会触发
2. mouseleave： 位于元素上方的鼠标光标移动到元素范围之外时触发，事件不冒泡，而且在光标移动到后代元素上时不触发。

3. mouseover: 在鼠标光标位于一个元素外部（可能是其子元素），首次移动到另一个元素边界之内时触发。事件冒泡
4. mouseout： 在鼠标光标位于一个元素上方，然后将其移入另一个元素时触发（可能是其子元素），事件冒泡。

5. mousemove: 当鼠标指针在元素内部移动是重复触发

**mouseover与mouseenter**

> 不论鼠标指针穿过被选元素或其子元素，都会触发 mouseover 事件。

> 只有在鼠标指针穿过被选元素时，才会触发 mouseenter 事件。

**mouseout与mouseleave**

> 不论鼠标指针离开被选元素还是任何子元素，都会触发 mouseout 事件。

> 只有在鼠标指针离开被选元素时，才会触发 mouseleave 事件。

4.4 键盘与文本事件

> `keydown`事件：当用户按下键盘上的任意键时触发，如果按住不放的话，会重复触发此事件。

> `keypress`事件：当用户按下键盘上的任意**字符**键(能够改变文本的键，包括插入删除键)时触发，如果按住不放的话，会重复触发此事件。

> `keyup`事件：当用户释放键盘上的任意键时触发。

>> 当用户按下一个字符键时，会先触发`keydown`，然后触发`keypress`，且这两个事件都是在文本框发生变化之前触发。最后触发`keyup`.


> `textInput`事件：作为`keypress`的补充。当用户在可编辑区域中输入字符时就会触发。
>> 与`keypress`区别之一：任何可以获得焦点的元素都可以触发`keypress`事件，而只有可编辑区才会触发`textInput`事件。
>> 与`keypress`区别之二：`textInput`只在用户按下那些能够输入实际字符的键时才会触发。

4.5 HTML5 新增事件

> `DOMContentLoaded`事件：形成完整的DOM树之后就会触发。

> `hashchange`事件：URL中的参数列表（以及URL中“#”后面的所有字符串）发生变化时触发。

4.6 触摸事件与手势事件

* 触摸事件
> touchstart: 当手指触摸屏幕时触发，即使已经有一个手指放在了屏幕上也会触发

> touchmove: 当手指在屏幕上滑动时连续触发。在这个事件发生期间，调用event.preventDefault()可以阻止滑动。

> touchend: 当手指从屏幕上移开时触发。

触摸事件的对象event，提供了3个用于跟踪触摸的属性：
1. touches: 表示当前跟踪的触摸操作的Touch对象的数组。
2. targetTouchs: 特定于事件目标的Touch对象的数组。
3. changeTouchs: 表示自上次触摸以来发生了什么改变的Touch对象的数组

以上每个`touch`对象，有包含属性：`clientX`、`clientY`、`pageX`、`pageY`、`screenX`、`screenY`、`target`、`identifier`


* 触摸事件: iOS 2.0 Safari浏览器支持。

> `gesturestart`：当一个手指已经按在屏幕上，而另一个手指又接触屏幕时才触发。

> `gesturemove`：当触摸屏幕的任何一个手指位置发生变化时触发。

> `gestureend`：当任何一个手指从屏幕上面移开时触发。



* web页面的内存及性能
1. 事件委托
> 对“事件处理程序过多”问题的解决就是事件委托，事件委托利用了事件冒泡，只在其父元素上指定一个事件处理程序，就可以监控子元素上某一类型的所有事件。
> 优点之一： 方便移除事件处理程序
>> 造成内存泄露的其中一种就是，从文档中移除了带有事件处理程序的元素，这肯能是通过纯粹的DOM操作，利用使用removeChild()和replaceChild(),但更多是使用innerHTML替换页面中的某一部分元素。


---------------

### DOM
* NodeList
> NodeList是一个类数组对象，可以通过方括号语法来访问NodeList的值，而且也具有length属性。比如节点的childNodes属性就是一个NodeList
> NodeList对象的独特之处在于：它实际上基于DOM结构动态执行查询的结构，因此DOM结构的变化能够自动反映在NodeList对象。我们常说，NodeList对象是有生命的有呼吸的，而不是我们第一次访问它们的某个瞬间拍摄下来的一张快照。
*引申*：类数组对象转化为数组
> 常见的类数组对象：函数的arguments, NodeList, HTMLCollection
> 转变为数组的方法：
>> * Array.prototype.slice.call()
>> * Array.from()

* 操作节点
1. appendChild()
2. insertBefore()
3. replaceChild()
4. removeChild()
5. clonNode(bool)

* 实现一个函数提供insertafter

```javascript
  function insertAfter(newElement, targetElement){
    var parentNode = targetElement.parentNode;
    if(parentNode.lastChild == targetElement){
      parentNode.appendChild(newElement);
    } else {
      parentNode.insertBefore(newElement, targetElement.nextSibling);
    }
  }
```

* 查找元素
1. getElementById()
2. getElementsByTagName()
3. getElementsByName()

* 实现getElementsByClass()函数

### 对作用域链的理解

* 作用域链是一个指向`变量对象`的指针列表，它只引用，但不是实际包含`变量对象`

* 而变量对象是和`执行环境`绑定的，执行环境定义了变量和函数有权访问的其他数据，决定了了它们各自的行为。执行环境中定义的所有变量和数据都保存在这个边梁对象中。

> `全局执行环境`被认为是最外围的一个执行环境。根据ECMAScript实现所在的宿主环境的不同，表示全局执行环境的变量对象也不一样，在Node中是一个Gobal对象，而在web浏览器中，这个变量对象被认为是`window`对象，因为所有的全局变量和函数都是作为window的属性和方法创建的。

> 某个执行环境中的代码执行完毕后，该环境就会被销毁，保存在对应变量对象中的变量和函数也会被销毁（全局执行环境直到应用程序退出时，才会被销毁）。

> 每个函数都有自己的执行环境，到执行流进入到一个函数时，该函数的执行环境就会被推入一个环境栈中，而在其执行完毕后，环境栈将其环境推出，将控制权返还给之前的执行环境。

* 作用域链的作用，是保证执行环境有权访问的变量和函数的有序性。作用域链的最前端，始终都是当前执行代码所在的执行环境的变量对象。作用域链的下一个变量对象来自包含环境，再下一个变量对象来自再下一个包含环境，这样一直延续到全局执行环境，全局执行环境的变量对象始终是作用域链的最后一个对象。

* 标识符解析就是沿着作用域链一级一级搜索标示符的过程。

#### 对闭包的理解

* 闭包是有权访问另一个函数作用域中的变量的函数

* 常见的创建闭包的方式，在一个函数的内部创建另一个函数

* 闭包的主要作用是模仿块级作用域和私有变量。

> 闭包模仿块级作用域

```javascript
(function(){
  // 这里是块级作用域
})();
```

> 私有变量

>> 使用构造函数模式、原型模式来实现自定义类型上的特权方法（有权访问私有变量和私有函数的方法）

```javascript
function MyObject(){
  // 私有变量和私有函数
  var privateVariable = 10;
  function privateFunc(){
    return false;
  }
  
  //特权方法
  this.publicMethod = function(){
    privateVariable ++;
    privateFunc();
  };
}
```

***静态私有变量***

```javascript
  (function(){
    //定义私有变量和函数
    var privateVariable = 10;
    function privateFunc(){
      return false;
    }
    
    //构造函数
    MyObject(){};
    
    //公有/特权方法
    MyObject.prototype.publicFunc = function(){
      privateVariable++;
      privateFunc();
    };
  })();
```

>>使用模块模式和增强模块模式实现单例上的特权方法

***模块模式***

```javascript
  var singleton = function(){
    
    //私有变量和私有方法
    var privateVariable = 10;
    
    function privateFunc(){
      return false;
    }
    
    //特权/公有方法和属性
    return {
      publicProperty : true,
      publicMethod : function(){
        privateVariable++;
        privateFunc();
      }
    }
  }();
```

***增强的模块模式***

```javascript
  var singleton = function(){
    
    //定义私有变量和函数
    var privateVariable = 10;
    
    function privateFunc(){
      return false;
    }
    
    var obj = new CustomType();
    
    //添加特权/公有属性和方法
    obj.publicProperty = true;
    
    obj.publicMethod = function(){
      privateVariable++;
      privateFunc();
    };
    
    return obj;
  }();
```

### javascript实现快排序

```javascript
  function quickSort(arr){
    if(arr.length === 1){
      return arr;
    }
    
    var midIndex = Math.floor(arr.length/2);
    var midNum = arr.splice(midIndex,1);
    var leftArr = [];
    var rightArr = [];
    
    for(var i=0; i<arr.length; i++){
      if(arr[i] < midNum){
        leftArr.push(arr[i]);
      } else{
        rightArr.push(arr[i]);
      }
    }
    
    return quickSort(leftArr).concat(midNum, quickSort(rightArr));
  }


```

### 数据类型检测

* 使用`typeof`检测基本数据类型（number、string、boolean、undefined）

> 使用typeof检测`function`时，会返回“function”。 但在 safari 5 和chrome 7之前的版本中， typeof 检测正则表达式也会返回“function”，因为ECMA-262规定，任何内部实现了[[call]]方法的对象在应用了typeof操作符是都应该返回“function”。之后的浏览器都修复了这个问题，typeof应用在正则表达式上时返回object

* 使用 instanceof 检测引用类型

```javascript
A instanceof B
```
> 原理：检测 B.prototype 是否存在于 A的[[prototype]]链上

* Object.prototype.toString.call() 检测所有数据类型

* 检测数组的方法

(1) 方法 instanceof
```javascript
  value instanceof Array
```
> instanceof 操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的Array构造函数。如果你从一个框架向另一个框架传入了一个数组，那么传入的数组与第二个框架原生创建的数据分别具有各自不同的构造函数。

(2) 方法 Array.isArray()

### 用new 来创建一个实例时 发生了什么

* 创建一个新对象

* 将构造函数的作用域赋给新对象（因此，this就指向了这个新对象）

* 执行构造函数内的代码，为这个新对象添加属性

* 返回新对象





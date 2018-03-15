# Javascript Section

### 事件
* 事件流
> 事件冒泡

> 事件捕获

> DOM2级 事件流

* 事件处理程序（绑定事件的几种方式）
> HTML 事件处理程序

> DOM0 事件处理程序

> DOM2 事件处理程序

> IE 事件处理程序

> 跨浏览器事件处理程序的实现

* 事件对象
> DOM中的事件对象

> IE中的时间对象

> 跨浏览器事件对象的实现

* mouseenter, mouseleave, mouseover, mouseleave, mousemove
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

* 触摸事件
1. touchstart: 当手指触摸屏幕时触发，即使已经有一个手指放在了屏幕上也会触发
2. touchmove: 当手指在屏幕上滑动时连续触发。在这个事件发生期间，调用event.preventDefault()可以阻止滑动。
3. touchend: 当手指从屏幕上移开时触发。

触摸事件的对象event，提供了3个用于跟踪触摸的属性：
1. touches: 表示当前跟踪的触摸操作的Touch对象的数组。
2. targetTouchs: 特定于事件目标的Touch对象的数组。
3. changeTouchs: 表示自上次触摸以来发生了什么改变的Touch对象的数组

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

* 查找元素
1. getElementById()
2. getElementsByTagName()
3. getElementsByName()

* 实现getElementsByClass()函数

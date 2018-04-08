## HTML5

### HTML5的新特性

1. 语义化更好的内容标签

> 语义化是指，根据文档的内容结构来选择合适的标签，也即，标签与呈现的内容相关，具有一定的含义，参考[这里](https://www.cnblogs.com/fliu/articles/5244866.html)

> HTML5 新增的语义化标签有：`article`、`header`、`footer`、`section`、`aside`、`nav`

  ![html5vshtml](https://github.com/buptwangsong/FE-Knowledge-collection/blob/master/img/20161015094026098.jpg)
  
 **主题结构元素**
  
 1.1 `article`：表示页面中一块与上下文不相关的独立内容。通常是一篇文章，一个页面，一个独立完整的内容模块。一般带有标题，放在`header`标签中。`article`标签可以相互嵌套，使用频率极高, 强调独立性，多注意与`header`标签的使用。
 
 1.2 `section`：表示页面中的一个内容区块，比如章节。通常由内容和标题组成。
 
 1.3 `nav`： 导航栏
 
 1.4 `aside`: `article`内容之外的信息，辅助信息。
 
 1.5 `time`: 表示时间。
 
 ```html
  <!-- datetime属性中日期与时间之间要用“T” 文字分隔，“T”表示时间 -->
  <time datetime="2013-3-6T20:00">2014年3月6日20:00</time>
 ```

 **非主题结构元素**
 
 1.6 `header`：从语义上看是文档的页眉，一般用法为：一个具有引导和导航作用的元素。通常放置在一个页面或者页面内的一个内容区块的标题，一个页面内可以含有多个`header`标签。

 1.7 `footer`: 从语义上看是文档的注脚，一般用法为：一个内容区块的注脚，通常内容为联系信息、相关阅读、版权信息等。
 
 1.8 `hgroup`: 标题组，对页面中的一个区块，或整个页面的标题进行分组。
 
 1.9 `address`： 地址
 
 ```html
 <address>
  <a href="">作者：张三丰</a>
  <a href="">地址：武当山</a>
  <a href="">联系方式：1247</a>
</address>
 ```
 
 1.10 `figure`：表示媒介内容的分组，以及它们的标题。



2. 新的表单元素及表单特性

2.1 新增的`input`元素类型 

> `email`： 提交表单时自动验证`email`域的值

> `url`： 提交表单时自动验证`url`域的值

> `number`: 用于应该包含数值的输入域，还能够限制接受的数字。显示为有增减箭头的输入框。

> `range`: 应该包含一定范围内数字值的输入域，还能够对显示的数字加以限制。显示为进度条。

> `data pickers`: data/week/month/time/datetime/datetime-local

> `search`

> `color`

```html
<input type="url" name="user-url" />
<input type="email" name="user-email" />
<input type="number" name="points" min="1" max="10">
<input type="range" name="points" min="1" max="10">
<input type="data" name="user_date">

```

2.2 表单特性

（1）`input`元素的`pattern`属性

（2）`a`标签的`download`属性

（3）`datalist`元素

（4）`link`标签`rel`属性的值`dns-prefetch`

（5）`link`标签`rel`属性的值`prefetch`


3. 废除了一些纯表现的元素

4. canvas 

5. SVG

> canvas VS svg

6. `audio`和`vedio`

> 浏览器支持性检测

7. geolocation API

8. communication API

8.1 跨文档消息传递 postMessage

8.2 XMLHttpRequest Level2

9. WebSockets

10. draggable API

11. web workers API

12 web storage API

## HTML5

### Reference

1. [前端开发攻城师绝对不可忽视的五个HTML5新特性 ](https://segmentfault.com/a/1190000003989795)
2. [理解HTML语义化](https://www.cnblogs.com/fliu/articles/5244866.html)
3. [前端面试之htm5新特性](https://segmentfault.com/a/1190000010081812)

### HTML5的新特性

1. 语义化更好的内容标签

> 语义化是指，根据文档的内容结构来选择合适的标签，也即，标签与呈现的内容相关，具有一定的含义。方便开发人员写出更优雅代码的同时，让机器和浏览器的爬虫能够很好的解析。举个例子：`strong`标签的语义表示强调，在外观上表现为加粗效果，用css同样可以模拟呈现的外观，但是却没有强调的语义。

> 语义化的好处：

（1）即使在没有CSS的情况下，页面也能呈现出很好的内容结构和代码结构。

（2）和搜索引擎建立良好的沟通，有利于爬虫抓取更多的有效信息，爬虫是根据标签来确定上下文和各个关键字的权重的。

（3）有利于团队开发和维护，语义化更具有可读性。



> HTML5 新增的语义化标签有：`article`、`header`、`footer`、`section`、`aside`、`nav`

  ![html5vshtml](https://github.com/buptwangsong/FE-Knowledge-collection/blob/master/img/20161015094026098.jpg)
  
  
 1.1 `article`：表示页面中一块与上下文不相关的独立内容。通常是一篇文章，一个页面，一个独立完整的内容模块。一般带有标题，放在`header`标签中。`article`标签可以相互嵌套，使用频率极高, 强调独立性，多注意与`header`标签的使用。
 
 1.2 `section`：表示页面中的一个内容区块，比如章节。通常由内容和标题组成。
 
 1.3 `nav`： 导航栏
 
 1.4 `aside`: `article`内容之外的信息，辅助信息。
 
 1.5 `time`: 表示时间。
 
 ```html
  <!-- datetime属性中日期与时间之间要用“T” 文字分隔，“T”表示时间 -->
  <time datetime="2013-3-6T20:00">2014年3月6日20:00</time>
 ```

 
 1.6 `header`
 
header 元素代表“网页”或“section”的页眉。

通常包含h1-h6元素或hgroup，作为整个页面或者一个内容块的标题。也可以包裹一节的目录部分，一个搜索框，一个nav，或者任何相关logo。

整个页面没有限制header元素的个数，可以拥有多个，可以为每个内容块增加一个header元素

* 使用header时要注意：

> 可以是网页或者section的头部

> 没有个数限制

> 如果`hgroup`或者`h1~h6`自己就能工作的很好，就不要再用`header`

 1.7 `footer`
 
 footer元素代表“网页”或“section”的页脚，通常含有该节的一些基本信息，譬如：作者，相关文档链接，版权资料。如果footer元素包含了整个节，那么它们就代表附录，索引，提拔，许可协议，标签，类别等一些其他类似信息。
 
 * footer使用注意：

> 可以是“网页”或任意“section”的底部部分；
> 没有个数限制，除了包裹的内容不一样，其他跟header类似。

 
 1.8 `hgroup`
 
 hgroup元素代表“网页”或“section”的标题，当元素有多个层级时，该元素可以将h1到h6元素放在其内，譬如文章的主标题和副标题的组合
 
 
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

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
  
  关于新增标签如何使用的细节，参考这里[理解HTML语义化](https://www.cnblogs.com/fliu/articles/5244866.html)
  
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

***************************************************************

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

关于这些特性的细节，参考这里[前端开发攻城师绝对不可忽视的五个HTML5新特性 ](https://segmentfault.com/a/1190000003989795)

（1）`input`元素的`pattern`属性

> 用于检测用户的输入是否符合特定的模式，`pattern`属性接一个正则表达式。

> 所有主流浏览器都支持该属性

>示例如下

```html
<input type="email" pattern="[^ @]*@[^ @]*" value="">
```

> 补充

* 关于正则表达式，参考这里[正则表达式手册](http://tool.oschina.net/uploads/apidocs/jquery/regexp.html)
* 常用的正则表达式

> `email`：`^[\w_-]+@[\w_-]+(\.[\w_-]+)+$`--只允许英文字母、数字、下划线、英文句号、以及中划线组成
> `tel`: `^1[3|4|5|8]\d{9}`

（2）`a`标签的`download`属性

> 不通过后台，直接下载指定的资源，`download`接下载后文件的重命名。
> 兼容性：只有高版本的`Firefox`和`Chrome`才支持。
> 如果需要下载的资源是跨域的（包括跨子域），不同的浏览器表现的很不一致，Chrome可以下载资源，但不能重置文件名，而Firefox直接忽略download属性。

```html
<a href="/images/myw3schoolimage.jpg" download="w3logo">
```

> 补充
* 传统的做法是，后台提供一个下载资源的API，供前端有下载需求时调用，具体调用方式参考这里[HTML无刷新下载文件方法总汇](https://segmentfault.com/a/1190000002923363)

（3）`datalist`元素

> 限定用户的输入为`datalist`中`option`列出的几项。达到的效果是可以自动补齐，

> 所有主流浏览器都支持该元素

>需要配合`input`元素的`list`属性使用，示例代码如下：
```html
<form action="/server" method="post">
    <input list="jslib" name="jslib" >
    <datalist id="jslib">
        <option value="jQuery">
        <option value="Dojo">
        <option value="Prototype">
        <option value="Augular">
    </datalist>
    <input type="submit" value="完成" />
</form>
```

（4）`link`标签`rel`属性的值`dns-prefetch`

> DNS预先加载处理，控制浏览器预先解析指定的域名。

> 前端优化涉及DNS的有两点：一是减少DNS的请求次数（可以设置适当数量的域名，或者设置DNS缓存来减少该项），二是DNS的预解析。

> 浏览器兼容性：目前绝大多数的浏览器都支持该属性值

> 其它一些细节，可以参考这里：[前端优化系列之一：DNS预获取 dns-prefetch 提升页面载入速度](https://www.cnblogs.com/lhm166/articles/6073787.html)

```html
<link rel="dns-prefetch" href="//www.gbtags.com">
<link rel="dns-prefetch" href="//www.gbin1.com">
<link rel="dns-prefetch" href="//m.gbin1.com">
<link rel="dns-prefetch" href="//s.gbin1.com">
```

（5）资源的预先加载`prefetch`

```html
<link rel='prefetch' href='secondary.js'>
```

>`Firefox`浏览器还提供了一种额外的写法

```
<meta http-equiv="link" content="<secondary.js>, rel=prefetch"
```

> 让浏览器预先加载用户访问完当前页面后极有可能访问的其它资源（页面，图片，视频）

> 浏览器的兼容性：支持的浏览器有Chrome(13以后), Firefox, IE 11

(6) `link`元素`rel`属性的`prerender`值

> 预先下载并渲染一个用户极可能访问的页面。

> Prerender是Google的一个发明，致力于减少用户在加载页面时的等待时间, 通过`最相近匹配原则`来加载例如“下一页”的文章, 例如最佳推荐，当用户访问A页面的时候, 用户最可能访问的下一个页面上B 那么就预加载B页面, 以达到提升加载速度的效果。

> 浏览器兼容性：支持的浏览器有Chrome , IE11

> 一些其它细节，可以参考这里[prefetch/prerender](http://www.php.cn/html5-tutorial-361854.html)

```html
<link rel="prerender" href="http://www.gbtags.com/gb/search.htm" />
```
（7）`input`元素的`placeholder`属性

> 当用户还没有输入值的时候，输入性控件可以通过该属性向用户显示描述性信息或提示信息。

```html
<input type="text" name="name" placeholder="First and Last name">
```

* 修改`placeholder`的样式

```css
::-webkit-input-placeholder { /* WebKit, Blink, Edge */
    color:    #909;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
   color:    #909;
}
::-moz-placeholder { /* Mozilla Firefox 19+ */
   color:    #909;
}
:-ms-input-placeholder { /* Internet Explorer 10-11 */
   color:    #909;
}
```

（8）`input`的`autocomplete`属性

> 规定输入字段是否应该启用自动完成功能。

> 自动完成功能允许浏览器预测对字段的输入。当用户开始输入时，浏览器基于之前输入过的值，应该显示出在字段中填写的选项。

> 该属性可用于`form`和下面的`input`

```html
<input type="text" name="name" autocomplete="on">
```

（9）`input`的`autofocus`属性

> autofocus 属性规定当页面加载时 input 元素应该自动获得焦点。
> 一个页面中只允许设置一个该属性，如果设置了多个，相当于为启用该功能

```html
<input type="text" name="fname" autofocus="autofocus" />
```


（10）`input`的`spellcheck`属性

> 对文本域的内容进行拼写检查

```html
<p contenteditable="true" spellcheck="true">这是可编辑的段落。请试着编辑文本。</p>
```

*********************************************

3. 废除了一些元素：纯表现的元素、只有部分浏览器支持的元素、对可用性产生负影响的元素

3.1 纯表现的元素

纯表现的元素是那些完全可以用css来代替的元素，例如`big`、`center`、`u`、`strike`、`tt`、`font`、`basefont`

3.2 对页面产生负影响的元素

主要有`frame`、`frameset`、`noframes`，html5只支持`iframe`元素

3.3 只有部分浏览器支持的元素

对于applet、bgsound、blink、marquee等元素，由于只有部分浏览器支持，特别是bgsound元素以及marquee元素，只被IE支持，所以在html5中被废除。其中applet元素可由embed元素或object元素替代，bgsound元素可由audio元素替代，marquee可以由javascript编程的方式替代。

*****************************************

4. canvas 

>`canvas`元素为页面提供一块画布来展示图形。结合`Canvas API`就可以在这个画布上动态生成和展示图形、图标、图像和动画。
> `canvas`本质上是位图画布，不可缩放，绘制出来的对象不属于页面DOM结构或者任何的命名空间。不需要将每个图元当做对象处理，执行性能非常好。

> 利用`canvas API`绘图，首先要获取`canvas`元素的上下文，然后用该上下文封装好的各种功能绘图。

```javascript
<canvas id="canvas">替代内容</canvas>
<script>
    var canvas = document.getElementById('canvas');
    var context =canvas.getContext("2d"); // 获取上下文
    //设置纯色
    context.fillStyle = "red";
    context.strokeStyle = "blue";
    // 实践表明在不设置fillStyle下的默认fillStyle为black
    context.fillRect(0, 0, 100, 100);
    // 实践表明在不设置strokeStyle下的默认strokeStyle为black
    context.strokeRect(120, 0, 100, 100);
</script>
```

****************************************************

5. SVG

> `svg`是html5的另一项绘图功能，它是一种标准的矢量图形，是一种图像格式，有自己的API
> html5引入了内联的`svg`元素，使`svg`元素可以直接出现在html文档中。

```html
<svg width="100px" height="100px"><circle cx="50px" cy="50px" cr="50px" /></svg>
```

> canvas VS svg

* canvas
（1） canvas 依赖javascript来绘制2D图像，是逐像素进行渲染的。在`canvas`中一旦图像绘制完毕，它就不会再得到浏览器的关注。如果其位置发生了变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

（2）依赖分辨率

（3）不支持事件处理器

（4）弱的文本渲染能力

（5）能够以`.jpg`和`.png`格式保存结果图像

（6）适合图像密集型的游戏，其中很多图像会被频繁的重新绘制

（7）`echart`是基于canvas的

* SVG

（1） `svg`是一种使用xml描述的2D图像语言。`SVG`基于`XML`意味着SVG DOM中的每个对象都是可用的，你可以为某个元素附加上javascript的事件处理器。

（2） 在`svg`中每个被绘制的图像均被视为对象。如果`svg`对象的属性发生了变化，那么浏览器能够自动重现图像。

（3）不依赖分辨率

（4）支持事件处理器

（5）最适合带有大型渲染区域的应用程序（比如，谷歌地图）

（6）复杂度高会减慢渲染速度，任何过度使用DOM的应用都不会快。

（7）不适合游戏应用。

（8）`highchart`和`D3.js`都是基于`svg`的

***************************************

6. `audio`和`vedio`

`audio`和`video`元素的出现为html5的媒体应用提供了新的选择，开发人员不必安装插件就可以播放音频和视频。对这两个元素来说，html5提供了通用、完整、可脚本化控制的API。

html5规范出来之前，在页面中播放视频的典型方式是使用Flash、QuickTime或者Windows Media插件往html中嵌入音频视频，相对这种方式，使用html5的媒体标签有两大好处。

（1）作为浏览器原生支持的功能，新的audio和video元素无需安装。

（2）媒体元素像Web页面提供了通用、集成和可脚本化控制的API。

* audio
```hmtl
// example 1
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
您的浏览器不支持 audio 元素。
</audio>

//example 2
<audio src="/i/horse.ogg" controls="controls">
Your browser does not support the audio element.
</audio>
```

* video
```html
//example 1

<video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
    您的浏览器不支持 video 标签。
</video>

//example 2
<video src="/i/movie.ogg" controls="controls">
your browser does not support the video tag
</video>
```

> 浏览器支持性检测

检测浏览器是否支持某个元素的一般思路是：使用脚本动态的创建该元素，然后检测特定的函数是否存在。
```javascript
let hasVideo = !!(document.createElement("video").canPlayType);
```

*注意：`!!()`是用来进行类型转换为boolean的。


******************************


7. geolocation API

html5的`Geolocation API`(地理定位API)，可以请求用户共享他们的位置。如果用户同意，浏览器就会返回地理位置信息。该定位信息由支持html5地理定位功能的底层设备提供给浏览器。地位信息包括经度、纬度坐标和一些其它元数据。

****************************

8. communication API

8.1 跨文档消息传递 postMessage

> 提供了一种在浏览器窗口、标签页和iframe间安全的进行跨源通信的方式。

> 细节参考这里[浏览器同源策略及规避方法](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)

8.2 XMLHttpRequest Level2

`XMLHttpRequest API`使得AJAX技术成为可能，作为`XMLHttpRequest`的改进版本，`XMLHttpRequest Level2`在功能上有了很大的改进，主要有两个方面：

（1）跨源的`XMLHttpRequest`
（2）进度事件

关于跨域资源共享的细节，参考这里[跨域资源共享](http://www.ruanyifeng.com/blog/2016/04/cors.html)


************************

9. WebSockets

> WebSockets主要解决了http协议的一大缺点：通信只能有客户端发起。

> Websockets属于应用层协议，使用`ws://`（非加密）`wss://`（加密）作为协议的前缀。该协议不实行同源策略，只要服务器支持，就可以用它来进行跨域通信。

> WebSockets提供了双向的、按序到达的数据流。websockets的连接是持久的，它通过在服务器和客户端之间保持双工连接，服务器端的更新可以及时的推送到客户端，而不需要客户端以一定的时间间隔去轮训。

> webSockets协议的主要特点：服务器可以主动向客户端推动信息，客户端也可以主动向服务器推送信息，是真正的双向平等对话，属于服务器推送技术的一种。

> 关于websockets的详细细节参考这里[websockets教程](http://www.ruanyifeng.com/blog/2017/05/websocket.html)


******************

10. draggable API

**********************

11. web workers API

************************

12 web storage API

### 云峰金融的面试题

1. 移动端如何识别左滑、右划

Reference

1.[HTML5 移动端的上下左右滑动问题 ](https://segmentfault.com/q/1010000002585476)

2. 如何实现一个图片的slider效果

3. 跨域

4. jQuery是如何实现promise效果的

Reference
1. [大白话讲解Promise（三）搞懂jquery中的Promise](https://www.cnblogs.com/lvdabao/p/jquery-deferred.html)

5. 如何保证前端源代码代码安全

Reference：

（1）[前端源码安全](https://www.cnblogs.com/lovesong/p/5185543.html)

（2）[前端如何给 JavaScript 加密（不是混淆）？](https://www.zhihu.com/question/47047191)

6. get和post的区别

首先需要明确两组概念：

（1）`语义`和`语法`

（2）`specification`和`implementation`

`语义`和`specification`都属于规范上的概念，也就是协议，具体以RFC的形式存在，而`语法`和`implementation`属于浏览器的具体实现，具体实现可能会和规范
有一定的出人。

这里要讨论的区别，是从规范和协议上讨论的。

RFC7231里定义了HTTP方法的几个性质：

（1）safe - 安全

> 这里的`安全`和通常意义上理解的`安全`不一样。如果一个方法的语义在本质上是`只读`的，那么这个方法就是`安全`。客户端向服务端发起的资源请求如果使用了安全的
方法，就不应该引起服务器端任何状态的变化，因此是无害的。

> RFC协议规定，`GET`、`OPTIONS`、`HEAD`、`TRACE`这几个方法是安全的。

> 引入安全这个概念的目的是为了方便网络爬虫和缓存，以免调用或者缓存某些不安全的方法时引起某些意外的后果。`User Agent`应该在执行安全和不安全的方法时做出区分
对待，并给用户以提示。

> 这个定义只是规范，并不能保证方法的实现也是安全的，服务器端的实现可能会不符合方法的语义，比如，使用`GET`方法修改用户信息的情况。

（2）Idempotent - 幂等

> 幂等的概念是指，同一个请求方法执行一次和执行多次效果是完全一样的。

> RFC协议规定，`DELETE`、`PUT`和安全的方法都是幂等的。

> 引入幂等主要是为了处理同一请求重复发送的情况。比如，在请求响应前失去连接，如果方法是幂等的，就可以放心的重新发送一次。这也是浏览器在后退/刷新时遇到post会给用户提示的原因，post的语义不是幂等的，重复发送可能会带来意想不到的后果。

> 这个定义只是规范，服务器端的实现是否幂等是无法保证的。

（3）cacheable - 缓存

> 一个方法是否可以被缓存

> RFC协议规定，`GET`、`HEAD`和某些情况下的`POST`方法是可缓存的。但绝大多数浏览器的实现里仅仅支持`GET`、`POST`的缓存。

7. web优化

影响一个网络请求的因素有两个：带宽和延时。今天的网络基础设施建设已经使得网络带宽得到极大的提升，大多数情况下都是网络延迟在影响响应速度。

web性能优化的终极目标就是减少用户端的延时，让用户能够尽快的打开前端页面，并进行交互。对客户端而言，就是发送尽可能少的数据给服务器，从服务器下载竟可能少的数据，尽可能的减少round trips time。

（1）减少http请求次数：css sprites、合并css和js文件。

（2）启用缓存，缓存分为两种：客户端缓存和服务器缓存

> 服务器缓存：CDN

> 客户端缓存又分为两种：强缓存和协商缓存

>> 强缓存在response header 中设置`expires`、`cache-control:max-age`
>> 协商缓存通过设置http header中 `last-modified/if-modified-since`、`Etag/if-none-match`

（3）启用压缩

> 设置request header 中`Accept-Encoding: Gzip`来通知服务器。

（4）DNS优化，包括两个方面：减少DNS查询，和DNS预解析

> 减少DNS查询次数

>> 设置request header 中`Connection: Keep-Alive`(`close`关闭)来告诉服务器本次请求结束后不断开TCP连接

>> 使用适当数量的域名

> DNS预解析

<link rel="dns-prefetch" href="www.baidu.com">

（5）使用外联的CSS和javascript文件，将CSS放置在`header`中，将javascript放置在`body`底部，精简css和javascript文件。

（6）避免重定向，通过在URL的末尾添加`/`，可以避免一部分重定向。

（7）移除重复的脚本文件

（8）首屏外资源按需加载，静态资源延迟加载，预加载。

> 图片资源按需加载

```html
<img width="100px" height="100px" data-src="真实的图片地址" src="一张加载中的gif图片">
```

然后监听`scroll`滚动事件，如果图片的位置在可视区内，则将`data-src`属性的值塞进`src`属性中即可。

> 预加载
>> 利用css 的background属性，将图片加载到屏幕之外的地方，只要这些图片的路径保持不变，当他们在`web`页面的其它地方被调用时，浏览器就可以只用之前已经加载缓存的图片了。

>> 利用`link`标签的`rel`属性的`prefetch`，预加载指定的文档资源。

> 其它相信解析，参考这里[前端性能优化之加载技术](https://www.jianshu.com/p/ba9759384ecf)

（9）缓存更新

> 以文件内容的`hash`值为依据生成新文件的非覆盖式发布策略是解决静态资源缓存更新最有效的手段。

（10）图片设置`width`和`height`属性，这样当网速比较差或者其它原因无法加载图片的时候，页面布局不会乱。






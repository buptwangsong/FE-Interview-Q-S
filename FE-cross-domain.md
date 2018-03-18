## 浏览器同源策略及规避方法

### 含义

同源政策最初是由Netscape 公司提出来的，现在所有的浏览器都实行这一政策

同源政策的最初含义是，A网页设置的cookie，B网页不能读取，除非它们同源。而*同源*是指3个相同：

* 协议
* 域名
* 端口号

### 目的

同源策略是浏览器安全的基石，它是为了保护用户信息安全，防止被恶意网站窃取。

### 限制范围

随着互联网的发展，*同源策略*越来越严格，如果是非同源，下列三种行为将受到限制：

* Cookie、localStorage、indexDB将无法读取

* DOM 无法获得

* AJAX 请求不能发送

### 规避策略

#### 设置document.domain 跨次域读取设置cookie

cookie 是服务器写入浏览器的一小段信息，只用同源的网页才能共享。但是，两个网页一级域名相同，二级域名不同时，浏览器允许通过设置document.domain共享cookie

**注意** 这种方法只适用于cookie和iframe窗口，localStorage和indexDB 无法通过这种方法读取

### 片段标示符

片段标示符是URL中#后面的部分，如果只是改变片段标示符，页面是不会刷新的。

父窗口可以把信息写入子窗口的片段标示符，子窗口通过监听hashchange事件得到通知。


### window.name

浏览器窗口有个`name`属性，这个属性的最大特点就是，无论是否同源，前一个页面设置了这个属性，后一个页面可以去读它.


### window.postMessage

###jsonp

动态的插入一个`script`标签，通过这个标签访问一个带参数的url，向服务器请求json数据，服务器接到这个请求后，会将数据放到我们指定的回调函数中返回。

```javascript
  function addScriptTag(url){
    var script = document.createElement('script');
    script.setAttribute('type', 'text/javascript');
    script.src = url;
    document.body.appendChild(script);
  }
  
  
  window.onload = function(e){
    addScriptTag('http://example.com/ip?callback=foo');
  }
  
  function foo(data){
    console.log('You public IP address is:'+ data.ip);
  }
```

### WebSocket

WebSocket 是HTML5提出的一种通信协议。使用 `ws://`(非加密)和`wss://`（加密）作为协议的前缀。该协议不实行同源策略，只要服务器支持，就可以用它进行
跨域通信。

> websocket 是web 应用程序的传输协议，它提供了双向的、按序到达的数据流。websocket的连接是持久的，它通过在客户端和服务器之间保持双工连接，这样服务器的更新可以被即使推送到客户端，而不需要客户端以一定的时间间隔去轮询。

> WebSocket 主要用来解决http协议的一大缺点：通信只能有客户端发起。

> WebSocket 的主要特点：服务器可以主动向客户端推送消息，客户端也可以主动向服务器推送消息，是真正的双向平等对话，属于服务器推送技术的一种。关于websocket的更多细节，[移步这里](http://www.ruanyifeng.com/blog/2017/05/websocket.html)

### CORS

日后总结：
[参考这里](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)





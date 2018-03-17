## ES6 Promise

1. 介绍：

> Promise 是异步编程的一种解决方案，比传统的解决方案——事件和回调函数——更加强大和合理

2. Promise 实现异步加载图片

```javascript
  function loadImageAsync(url){
    return new Promise(function(resolve, reject){
      const image = new Image();
      
      image.onload = function(){
        resolve(image);
      };
      
      image.onerror = function(){
        reject(new Error(`Can't load image at ${url}`));
      }
      
      image.src = url;
      
    });
  }
```

3. Promise 实现Ajax操作

```javascript
const getJSON = function(url){
  const promise = new Promise(function(resolve, reject){
    const handler = function(){
      if(this.readyState !== 4){
        return;
      }
    
      if(this.status === 200){
        resolve(this.response);
      } else {
        reject(new Error(this.statusText))
      }
    }
  
    const client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json"
    client.setRequestHeader("Accept", "application/json");
    client.send();
  });
  
  return promise;
}
```

> 使用
```javascript
  getJSON('/post.json').then(function(json){
    console.log(`Contents: ${json}`);
  }, function(error){
    console.log(`something error: ${error}`);
  });
```

4. Promise 的 API



原文链接[2018面试题总结](https://segmentfault.com/a/1190000013827826)


1. 使用css实现一个持续的动画效果

```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>animation moveon</title>
      <style type="text/css">
        body{
          position: relative;
        }
  
        .box{
          width: 100px;
          height: 100px;
          position: absolute;
          background-color: red;
          animation: moveon 5s infinite;
          -webkit-animation: moveon 5s infinite;
        }
  
        @keyframes moveon{
          from{
            left: 0px;
          }
          to{
            left: 100px;
          }
        }
  
       @-webkit-keyframes moveon{
          from{
            left: 0px;
          }
  
          to{
            left:100px;
          }
  
       }
  
      </style>
    </head>
    <body>
      <div class="box">box</div>
    </body>
  </html>

``

2. 使用js实现一个持续的动画效果

3. 右边宽度固定，左边自适应
```html
  <!DOCTYPE html>
<html>
	<head>
		<title>layout</title>
	</head>
	<body>
		<div class="left">left</div>
		<div class="right">right</div>
	</body>
</html>
```

> 3.1 Flex布局

```css
      body{
		display: flex;  // important
		display: -webkit-flex; //important
	}

	.left{
		width: 200px;
		height: 200px;
		background-color: grey;
	}

	.right{
		height: 200px;
		background-color: yellow;
		flex: 1; //important
	}
```

> 3.2 float + BFC

```css
    .left{
	width: 200px;
	height: 200px;
	background-color: grey;
	float: left;
     }

	.right{
		height: 200px;
		background-color: yellow;
		overflow: hidden;
	}
```

> 3.3 float + margin-left撑开

> 3.4 position + margin-left撑开


4. 水平垂直居中

5. 四种定位的区别

6. 封装一个函数，参数是定时器的时间，.then执行回调函数。

7. 一行代码实现数组去重

8. 怎么判断两个对象相等

9. 重排和重绘

10. 什么情况会触发重排和重绘

11. js bind 实现机制？手写一个 bind 方法？

12. __proto__、prototype、Object.getPrototypeOf()

13. setTimeout 和 setInterval 细谈

14. 判断多图片加载完毕

15. CSS margin重叠问题

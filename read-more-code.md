## 值得反复把玩的代码

1. 尾递归

尾递归的实现，往往需要改写递归函数，确保最后一步只调用自身，做到这一点的方法就是，把所有用到的内部变量改写成函数参数。

> 非尾递归

```javascript
  function factorial(n){
    if(n === 1){
      return 1;
    }
    
    return n*factorial(n-1);
  }
```

> 改成：尾递归

```javascript
  function factorial(n, total){
    if(n === 1){
      return total;
    }
    
    factorial(n-1, n*total);
  }

```

* 另一个例子：Fibonacci

> 非尾递归

```javascript
  function fabonacci(n){
    if(n<=1){
      return 1;
    }
    
    return fabonacci(n-1)+fabonacci(n-2);
  }
```

> 改成尾递归

```javascript
  function fabonacci(n, a=1, b=1){
    if(n<=1){
      return b;
    }
    
    return fabonacci(n-1, b, a+b);
  }

```

2. 函数柯里化

将多参数的函数，转变为单参数函数的形式

```javascript
  function currying(fn, n){
    return function(m){
      fn.call(this,m,n);
    }
  }
```

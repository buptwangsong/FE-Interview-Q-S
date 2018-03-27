## 值得反复把玩的代码

1. 尾递归

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

## 总结javascript的一些小技巧

1. `reduce` 妙用

1.1 使用`reduce`同时实现`map`和`filter`

假设：现在有一个数列，需要更新它的每一项，并且筛选出一部分。如果先用`map`更新，再用`filter`筛选的话，需要遍历数组两次。

例子：将数组中的每一项翻倍，然后筛选出大于50的项

```javascript
  const numbers = [10, 20, 30];
  const doubleOver50 = numbers.reduce(function(prev, cur, index, arr){
    cur = cur * 2;
    if(cur > 50){
      prev.push(cur);
    }
    return prev;
  }, []);
  
  
```

1.2 使用`reduce`匹配圆括号

对于一个含有圆括号的字符串，我们需要知道`（`和`）`的数量是否一致，`（`是否出现在`）`之前。

代码思路如下：声明一个变量`counter`，初始值为`0`，如果遇到`（`则加一，遇到`）`则减一。

```javascript
const isParensBalanced = (str)=>{
  return str.split('').reduce((counter, char) =>{
    if(counter<0){ //match ')'before '('
      return counter;
    } else if(char === ')'){
      counter--;
    } else if(char === '('){
      counter++;
    }
    return counter;
  }, 0);
}
```

1.3 统计数组中相同项的个数

统计数组中重复出现的项的个数，然后用对象表示。

```javascript
const cars = ['BMW','Benz', 'Benz', 'Tesla', 'BMW', 'Toyota'];
const resultObj = cars.reduce((result, name)=>{
  result[name] = result[name] ? ++result[name] : 1;
  
  return resultObj;
},{});
```

2. 函数强制要求传递参数

```javascript
  const required = () => {throw new Error("Missing Parameters")};
  
  const add = (a = required(), b = required())=> a+b
  
 
 3. 对象解构赋值
 
 3.1 删除不需要的属性
 
 有时候你不希望保留某些对象的属性，也许是因为包含敏感信息，或者太大。可以将想要删除属性赋值给变量，而想要保留的属性作为剩余参数就可以了。
 
 下面的代码里，我们希望删除`internal`和`tooBig`参数。我们可以把它们赋值给`internal`和`tooBig`变量，然后在`cleanObject`中存储剩下的属性以备后用。
 
 {internal, toobig, ...cleanObject} = {el1: '1', internal:"secret", tooBig:{}, el2: '2', el3: '3'};
 
```

3.2 在函数参数中解构嵌套对象

在下面的代码中，engine是对象car中嵌套的一个对象。如果我们对engine的vin属性感兴趣，使用解构赋值可以很轻松地得到它。

```javascript
var car = {
  model: 'bmw 2018',
  engine: {
    v6: true,
    turbo: true,
    vin: 12345
  }
}

const modelAndVin = ({model, engine:{vin}}) => {
  console.log(`model: ${model}, vin: ${vin}`);
}
```

4. 扩展运算符 `...`

4.1 合并对象

作用类似与`$.extend`和`$.fn.extend`

```javascript
let object1 = { a:1, b:2,c:3 }
let object2 = { b:30, c:40, d:50}
let merged = {…object1, …object2} //spread and re-add into merged
console.log(merged) // {a:1, b:30, c:40, d:50}
```

4.1 转化为数组

```
  let myset = new Set([1,2,3,3,4,1]);
  const filtered = [...myset].filter(item => item>3);
```

4.2 结合`set`实现数组去重

```javascript
let arr = [1,1,1,1,2,2,3,4,5,3];
let deduped = [...new Set(arr)]
```



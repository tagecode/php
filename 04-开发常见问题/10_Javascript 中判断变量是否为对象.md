### Javascript 中判断变量是否为对象

#### 如果`Object`方法的参数是一个对象，它总是返回该对象，即不用转换。
```javascript
var arr = [];
var obj = Object(arr); // 返回原数组
obj === arr // true

var value = {};
var obj = Object(value) // 返回原对象
obj === value // true

var fn = function () {};
var obj = Object(fn); // 返回原函数
obj === fn // true
```

#### 利用这一点，可以写一个判断变量是否为对象的函数。
```javascript
function isObject(value) {
  return value === Object(value);
}

isObject([]) // true
isObject(true) // false
```
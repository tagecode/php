### Javascript 中计算对象属性个数

#### `JavaScript` 没有提供计算对象属性个数的方法，但是利用`Object` 的静态方法可以代替计算出来。
```javascript
var obj = {
  p1: 123,
  p2: 456
};

Object.keys(obj).length // 2
Object.getOwnPropertyNames(obj).length // 2
```
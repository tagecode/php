### Javascript 中对象的拷贝

#### 有时，我们需要将一个对象的所有属性，拷贝到另一个对象，可以用下面的方法实现。
```javascript
var extend = function (to, from) {
  for (var property in from) {
    if (!from.hasOwnProperty(property)) continue;
    Object.defineProperty(
      to,
      property,
      Object.getOwnPropertyDescriptor(from, property)
    );
  }

  return to;
};

extend({}, { get a(){ return 1 } })
// { get a(){ return 1 } })
```

#### 面代码中，`hasOwnProperty`那一行用来过滤掉继承的属性，否则可能会报错，因为`Object.getOwnPropertyDescriptor`读不到继承属性的属性描述对象。
## defineProperty：
- 特性：
  - configurable, 为 true 时，该属性描述符才能够被改变，也能够被删除。默认为 false。
  - enumerable,  为 true 时，该属性才能够出现在对象的枚举属性中。默认为 false。
  - value, 可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 undefined。
  - writable, 为 true 时，该属性才能被赋值运算符改变。默认为 false。
  - get, 一个给属性提供 getter 的方法，如果没有 getter 则为 undefined。该方法返回值被用作属性值。默认为 undefined。
  - set, 一个给属性提供 setter 的方法，如果没有 setter 则为 undefined。该方法将接受唯一参数，并将该参数的新值分配给该属性。默认为 undefined。
  ```
  Object.defineProperty(obj, 'name', {
    value: 1.
    writable: true,
    enumerable: true,
    configurable: true
  });
  var value = 1;
  Object.defineProperty(obj, 'name', {
    get: function() {
      return value;
    },
    set: function(newValue) {
      value = newValue;
    },
    enumberable: true,
    configurable: true
  });
  ```
- 实现 watch 函数：

## proxy：

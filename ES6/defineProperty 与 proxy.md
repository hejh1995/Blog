## defineProperty：
- 特性：
  - configurable, 为 true 时，该属性描述符才能够被改变，也能够被删除。默认为 false。
  - enumerable,  为 true 时，该属性才能够出现在对象的枚举属性中。默认为 false。
  - value, 可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 undefined。
  - writable, 为 true 时，该属性才能被赋值运算符改变。默认为 false。
  - get, 一个给属性提供 getter 的方法，如果没有 getter 则为 undefined。该方法返回值被用作属性值。默认为 undefined。
  - set, 一个给属性提供 setter 的方法，如果没有 setter 则为 undefined。该方法将接受唯一参数，并将该参数的新值分配给该属性。默认为 undefined。
  - value 和 writable 与 set 和 get 不能同时使用。
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
```
// 监控对象属性值的改变，并且根据属性值的改变，添加回调函数。
function watch(obj, name, func) {
  var value = obj[name];
  Object.defineProperty(obj, name, {
    get: function() {
      return value;
    },
    set: function(newValue) {
      vale = newValue;
      func(value);
    }
  });
  if (value) obj[name] = value
}
```
## proxy：
- 语法： var proxy = new Proxy(target, handler); target 表示要拦截的目标对象，handler 参数也是一个对象，用来定制拦截行为。
- proxy 可以拦截13种操作。比如get， set， has（可以拦截key in obj 的操作。）， apply（拦截函数的调用、call、apply操作）， ownKeys（拦截对象自身属性的读取，可以拦截的操作有：Object.getOwnPropertyNames, Object.getOwnPropertySymbols(), Object.keys()）。
- 
 ```
 var target = {
  _prop: 'foo',
  name: 'aa'
 };
 var handler = {
  get: function(obj, prop) {
    return obj[prop];
  },
  set: function(obj, prop, value) {
    obj[prop] = value;
  },
   // 隐藏 某些 属性，不被 in 运算符 发现。
  has(target, key) {
    if (key[0] === '-') {
      return false;
    }
    return key in target;
  },
  ownKeys(target) {
    return Reflect.ownKeys(target).filter(key => key[0] !== '_');
  }
 };
 var proxy = new Proxy(target, handler);
 propxy.name = 'qq';
 console.log('_prop' in proxy);
 console.log(propxy.name);
 for (let key of Object.keys(proxy)) {
  console.log(target[key]);
}
 ```
 - 实现 watch 函数
 ```
 // 监控对象属性值的改变，并且根据属性值的改变，添加回调函数。
function watch(target,func) {
  var proxy = new Proxy(target, {
    get(target, prop) {
      return target[prop];
    },
    set(target, prop, value) {
      targte[prop] = value;
      func(prop, value);
    }
  });
  return proxy;
}
 ```
 - 使用 defineProperty 和 proxy 的区别，当使用 defineProperty，我们修改原来的 obj 对象就可以触发拦截，而使用 proxy，就必须修改代理对象，即 Proxy 的实例才可以触发拦截。



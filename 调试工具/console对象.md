1. 现实信息的命令：
```
console.log('这是log');
console.info("这是info");
console.debug("这是debug");
console.warn("这是warn");
console.error("这是error");
```
img
2. 占位符：
- console 对象 上面的 5 中方法，都可以使用 prontf 风格的占位符。
- 占位符 的 种类比较少，只有 ‘%s(字符)、%d / %i(整数)、%f（浮点数）、%o（对象）’。
```
console.log("%d年%d月%d日", 2019, 6,2);
console.log("圆周率是%f", 3.1415926);
let dog = {
    name: '大黄',
    color: {
        mouth: 'yellow',
        hair: 'red'
     },
     break() {
         console.log('break');
     }
}
console.log("%o", dog);
console.log(dog);
```
3. 分组 显示：
```
      console.group('第一组信息');
      console.log('1.1');
      console.log('1.2');
      console.groupEnd();
      console.group('第二组信息');
      console.log('2.1');
      console.log('2.2');
      console.groupEnd();
```
4. console.dirxml()  --- 显示网页的某个节点所含的 html/xml 代码。
```
// 感觉和 console.log 没什么区别
```
5. console.assert()  ---- 判断一个表达式或变量是否为真。为真不显示，为否抛出一个异常。
```
      console.assert(a == 'aaaa');
      console.assert(a == 'aa');
```
6. cosole.trace()  ---- 跟踪函数的待用轨迹
```
     function add(a, b) {
        console.trace();
        return a + b;
      }
      function add1(a, b) {
        return add(a, b+1);
      }
      function add2(a, b) {
        return add1(a+1, b);
      }
      let x = add2(1, 2);
```

7. 计时功能：
```
      console.time('计时器1');
      for (let i = 0; i < 100; i++) {}
      console.timeEnd('计时器1');
```

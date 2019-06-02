1. 菜单：
![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-console-1.png)
- 清空 可以使用 快捷键： Ctrl + L / Cmd + K
2. 执行环境
- 除了当前的页面的执行环境，其他的框架、拓展都有其自己的执行环境。
- 会发现默认的执行环境是 "top"，点击下拉框，你会发现还有其他选项。
3. chrome DevTools 自带的 有用的表达式：
- 选择元素：（当页面暴露相同的方法或变量的话，DevTools 自带的会被覆盖）
  - $()： document.querySelector() 的缩写
  - $$()： document.querySelectorAll() 的缩写
  - $x()：通过 XPath 的方式查看元素，注意是 "XPath" 中的 "x"，而不是 +-*/ 中的 *
- $0-4：
  - $0， $1...$4，代表 5 个最近访问过的 DOM 或者堆对象（Heap Object）.
  - $0 是最近访问的。
  - 访问，就是在 Elements 面板被审查或者在 Memory 面板被选择的 DOM 元素或者堆对象。
- $_ 返回上一次表达式执行的结果。
- event：
 - Chrome DevTools 里你可以给 DOM 绑定事件、解绑事件，也能查看 DOM 注册了哪些事件。
 - monitorEvents(DOM_element, event)，如果 event 为空的话，那会给选定的 DOM 元素加上所有事件；如果想监听多个事件的话，event 还可以是 Array 类型的变量
 - unmonitorEvents(DOM_element)，为某个 DOM 元素解绑事件
 - getEventListeners(DOM_element)，查看某个 DOM 元素绑定了哪些事件
![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-console-2.png)
- 其他：
 - debug(function) 与 undebug(function)：在 Console 中调用 debug() 方法，当调用这个方法的时候，就会开启 debug 模式。用 undebug 方法来关闭。
 - monitor(function) 与 unmonitor(function)：当调用某个 function 时，Console 会输出这个 function 的名字和参数。
 - dir(object) 与 dirxml(object)：dir() 与 console.dir() 一样，dirxml() 与 console.dirxml() 一样。dir() 将选中元素以对象的形式输出，而 dirxml() 将元素以 xml 的形式输出。
 - table(object)，与 console.table() 一样。
 - values() 与 keys()，与 ES6 中的用法一样。

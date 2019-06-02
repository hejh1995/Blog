1. 功能：
- 编辑、可视化编辑 HTML 和CSS。
![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-elements-1.png)

2.DOM 数：
- 按键盘的向上向下键可在展开的节点之间进行切换，向左向右键可以收缩和展开节点。
- 双击元素标签，修改 DOM 节点类型，比如将 div 改成 ul
- 双击元素属性，修改 DOM 节点属性，比如修改节点的 id
- 选择一个 DOM 节点，按 enter 键，然后按 tab 键选择想修改的属性或标签
- 选择一个 DOM 节点，并将其拖到目标位置，可以改变页面元素的结构
- 选择一个 DOM 节点，按 delete 键删除
- Ctrl + Z / Cmd + Z，撤回操作
- 多的操作可以通过选中一个 DOM 节点，再右击进行查看：
  - 4 个伪类：选中则表示所选节点处于相应的状态，比如选中 :hover 则表示所选节点当前正处于鼠标悬停的状态。
  - Scroll into View：如果所选的 DOM 节点对应的页面元素不在可视区域内的话，点击这个选项则会将页面滚动到可以显示对应的页面元素的位置。
  - Break on：给 DOM 节点设置断点，主要用来调试 JavaScript 代码，这段代码的作用是用来修改所加断点的 DOM 节点，这一般用在比较复杂的网页应用当中。可以给所选的 DOM 节点添加 3 种类型的断点：
   - subtree modifications：所选节点的子节点被添加、删除、移动的话，则会触发
   - attribute modifications：所选节点的属性被修改的话，则会触发
   - node removal：所选节点被删除的话，则会触发。
3. 样式：
![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-elements-2.png)
- styles：
  - 击属性或者属性值，进行修改：
    - 按 tab 键修改下一个属性或值。
    - 按 tab + shift 修改上一个属性或值。
    - 当值是数字类型时，按上下键可以以 1 为单位递增或递减。
    - 当值是数字类型时，按 alt + 上下键以 0.1 为单位递增或递减。
    - 当值是数字类型时，shift + 上下键以 10 为单位递增或递减。
  - 点击色块可以打开取色器。
  - 将鼠标悬停在一个选择器上时，可以看到这个选择器所影响的所有页面元素（不包括可视区域外的元素）。
  - 每个样式的右侧有三个 . ，可以帮助你通过可视化界面的形式调试 text-shadow、 box-shadow、 color、 background。另外，最后一个 "+" 的符号代表可以添加新的 CSS 规则（在 element.style 中没有）
  ![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-elements-3.png)
  ![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-elements-4.png)
- computed：
  - 所选元素的盒模型
  - 所选元素的 CSS 样式以及值，不仅显示最终所采用的值，也显示被覆盖了的值
  - 每个属性值所在的文件。
  - 鼠标悬停在盒模型上的 margin、border、padding 以及内容区域，可以在网页中看到与之相对应的区域。
  - 你还可以双击盒模型上的数字来修改它。
  - 如果所选元素的 position 属性的值为 absolute 或者 fixed 的话，还可以在 margin 的外围设置 position。
- event listeners：
 - 显示了这个节点注册的所有事件类型，展开一个事件类型，可以看到这个类型下的所有处理函数。
 - ![image](https://github.com/hejh1995/project-img/blob/master/blog/devtool-elements-5.png)
 - 监听器类型：Passive / Blocking / All：Passive Event Listener 是从 Chrome 51 开始添加的一个新特性，主要用来让页面滑动更加流畅。
- DOM Breakpoints：
  - 显示 DOM 的断点。
- properties：
  - 所选 DOM 节点对应的对象以及这个对象的父类，父类的父类...的集合。

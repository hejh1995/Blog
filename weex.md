1. 工作流：
```
   Weex .we 文件 --------------前端(we源码)
   ↓ (转换) -------------------前端(构建过程)
   JS Bundle -----------------前端(JS Bundle代码)
   ↓ (部署) -------------------服务器
   在服务器上的JS bundle -------服务器
   ↓ (编译) -------------------客户端(JS引擎)
   虚拟 DOM 树 ----------------客户端(Weex JS Framework)
   ↓ (渲染) -------------------客户端(渲染引擎)
   Native视图 -----------------客户端(渲染引擎)
```
- Weex JS Framework，运行于客户端的js框架，管理weex实例的运行。它也发送/接受native渲染层产生的系统调用，从而间接的响应用户交互。
 - 在初始化阶段被原生js引擎运行。一旦js bundle 从服务器下载后，它所提供的方法就会执行，define() 函数以注册模块; bootstrap()会编译主要的模块为虚拟DOM，并发送渲染指令给Native .
 - js 和native 沟通的两个关键方法：
  - callNative 是一个由native代码实现的函数, 它被JS代码调用并向native发送指令,例如rendering, networking, authorizing和其他客户端侧的 toast 等API，
  - callJS 是一个由JS实现的函数, 它用于Native向JS发送指令. 目前这些指令由用户交互和Native的回调函数组成.
- native 引擎，在不同的端上，有着不同的实现，ios/andriod/h5，他们有着共同的组件设计，模块api和渲染效果，所以他们能够配合同样的js framework 和 js bundle 工作。
2. weex 渲染过程：
- 虚拟dom。
- 构造树结构。分析虚拟dom，json数据以构造渲染树。
- 添加样式。为渲染树的各个节点添加样式。
- 创建视图。为渲染树的各个节点创建native视图。
- 绑定事件。为native 视图绑定事件。
- css 布局。使用 css-layout 来计算各个视图的布局。
- 更新视窗。采用上一步的计算结果来更新视窗中各个视图的最终布局位置。
- 最终页面呈现。
3. weex 主要包含三大部分：js bridge、render、dom。其中js bridge 和 dom 运行在独立的 handler 线程，render 运行在ui线程。js bridge 主要用来和js 端进行双向通信，比如，js 端的dom结构传递给DOM 线程。com 主要用于负责dom的解析、映射、添加等等操作，最后render 负责在UI线程中对dom 实现渲染，所有的布局元素都会在这一层转化为原生组件。
4. 传统的 HTML DOM 事件是存在捕获和冒泡阶段的， Weex 做了精简，没有支持冒泡或捕获事件 ，只有在 native 层的当前元素触发该事件才会 fireEvent 给 JS。 
5. 页面布局：
- flex 布局是唯一的布局模型，不需要手动为元素添加display: flex；
- 无法使用 float 布局。
- 样式的作用域默认就是scoped。
- 样式不能继承。
- 不支持z-index。
- rem，是rax 中推荐的单位是将页面750等分计算的，同 weex中的px单位。
- 安卓，list 中的cell 无法展示内部超出的元素，可以将外部元素的宽高设置的大一点（比如imageupload组件。）
- web 页面天生可以滚动，native中却不是，所以rax 会提供一些滚动容器。
   - ScrollView：slider，支持垂直和水平滚动。一般情况下需要一个确定的高度来保证 ScrollView 的正常展现。
      - 安卓的list 的原生实现是Android RecyclerView 组件，在 iOS 上则使用的是原生的 UITableView。。
      - Android RecyclerView： 提供了复用机制来减少内存开销、提升滑动效率， weex 中list 也暴露出相应的api支持 cell 复用。
      - iOS UITableView ，一个以行 数据概念实现的列表。为了提高性能，利用有限的结构动态切换其内容来尽可能减少资源占用，以达到cell复用。
      - 
   - RecyclerView：list，可回收的长列表。它可以回收非可视区域的cell，并进行复用。
   - listView： 是 RecyclerView 的上层包装。
   - waterFall：底层实现也是list的一个扩展，在api能力上向listview 靠拢
   - TemplateList 的 Weex 实现是 recycler-list，是一个基于数据与模版的高性能长列表 。
 - 图片：
   - 必须传入宽高。
   - 已经做了优化，不用考虑 图片懒加载。
   - 不能设置背景图，只能使用图片插入到文档中。
   - 
6.事件：
- 不区分事件的捕获阶段和冒泡阶段，相当于DOM 0 级事件。
- 支持的事件类型有限。
7. 内建模块：
- weex 提供了许多内建模块，这部分区别于web的一些功能，直接调用移动端设备能力。
- 

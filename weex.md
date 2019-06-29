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
3. weex 主要包含三大部分：js bridge、render、dom。其中js bridge 和 dom 运行在独立的 handler 线程，render 运行在ui线程。js bridge 主要用来和js 端进行双向通信，比如，js 端的dom结构传递给DOM 线程。com 主要用于负责dom的解析、映射、添加等等操作，最后render 负责在UI线程中对dom 实现渲染。

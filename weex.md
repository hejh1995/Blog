1. 工作流：
Weex .we 文件 --------------前端(we源码)
↓ (转换) -------------------前端(构建过程)
JS Bundle -----------------前端(JS Bundle代码)
↓ (部署) -------------------服务器
在服务器上的JS bundle -------服务器
↓ (编译) -------------------客户端(JS引擎)
虚拟 DOM 树 ----------------客户端(Weex JS Framework)
↓ (渲染) -------------------客户端(渲染引擎)
Native视图 -----------------客户端(渲染引擎)
- Weex JS Framework，运行于客户端的js框架，管理weex实例的运行。它也发送/接受native渲染层产生的系统调用，从而间接的响应用户交互。
 - 在初始化阶段被原生js引擎运行。一旦js bundle 从服务器下载后，它所提供的方法就会执行，define() 函数以注册模块; bootstrap()会编译主要的模块为虚拟DOM，并发送渲染指令给Native .
 - js 和native 沟通的两个关键方法：
  - callNative 是一个由native代码实现的函数, 它被JS代码调用并向native发送指令,例如rendering, networking, authorizing和其他客户端侧的 toast 等API，
  - callJS 是一个由JS实现的函数, 它用于Native向JS发送指令. 目前这些指令由用户交互和Native的回调函数组成.
- native 引擎，在不同的端上，有着不同的实现，ios/andriod/h5，他们有着共同的组件设计，模块api和渲染效果，所以他们能够配合同样的js framework 和 js bundle 工作。

2. 

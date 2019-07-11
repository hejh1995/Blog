1. 概述
- rax是基于react 标准的跨容器解决方案，设计的核心思想是“react 标准”和“跨容器”
- 单向数据流，数据驱动UI渲染，数据变化了，可以直接通知dom更新。在写法上，视图和业务耦合在一起，业务逻辑复杂时，一定要将业务逻辑单独抽取出来。
- rax 是一套基于react 写法的weex 上层 DSL。
- rax 靠拢react native（实现 一次学习，可编写ios 和 andriod两端的代码） 的同时，还做了跨端，让一次学习变成一次编写。
- rax 在 native端的背后实现则是weex，weex是一款轻量级的移动端跨平台动态性技术解决方案。
- 与 React 也有部分区别，如下：
  - 没有 createClass() 方法
  - Rax setState() 是同步的, React setState 是异步的
  - findDOMNode() 方法可以接收字符串类型的 id
  -  PropTypes 只是 React 的接口兼容
2. 核心概念：
- 组件(Components) 
  - 内部提供了如 Text 和 Image 这样的跨容器组件。
  - 用组件来封装界面模块，整个界面就是一个大组件。
  - 开发过程就是不断优化和拆分界面组件、构造整个组件树的过程。
- 属性(Props)
  - 组件很少需要对外公开方法，唯一的交互途径就是 Props。这使得使用组件就像使用函数一样简单，给定一个输入，组件给定一个界面输出。
- 状态(State) 
  - 组件内部维持的状态数据称为 state ，它是组件的当前状态。
  - 可以把组件简单看成一个”状态机”，根据 state 呈现不同的 UI 展示。一旦 state 被更改，组件就会自动调用自身的 render 函数重新渲染 UI，这个更改 state 的动作会通过 this.setState方法来触发：this.setState({ value: 10 })
- 事件(Events) 
  - Rax 中绑定事件的方式和在 HTML 中绑定事件类似，使用驼峰式命名指定要绑定的事件属性为组件定义的一个方法：
  ```<TextInput onInput={ (event) => this.setState({ text: event.value }) } />```
- Flexbox 布局 
  - Rax 使用 flexbox 规则来描述组件。
- 样式 
  - 我们可以使用对象的方式来描述 CSS 中的样式，并传递给组件的 style 属性，唯一的区别是带连词号(-)的属性需要用驼峰写法代替。例如：
  ```<View style={{ width: 100, height: 100, backgroundColor: 'skyblue' }} />```
3. 生命周期
  - 同 react
2. 性能优化
- 将复杂组件合理拆分成小组件：局部更新可以减少更新时的性能损耗。
- 长列表适当分页：减少每次渲染的数据量。
- 子组件适当提供key：尽量保持组件dom结构的稳定。
- 利用钩子优化组件渲染：shouldComponentUpdate将更新的决定权交给开发者，PureComponent在更新触发时会比较props和state，如果没有变化就不更新。StatelessComponent 在组件渲染时不会生成Component实例，能减少一定性能损耗。
- 尽量自己来控制dom 的更新时机：setState 是同步的，要避免频繁调用。（？）
3. 长列表
- web 页面天生可以滚动，native 页面天生不可滚动。需要借助容器的滚动能力。
- 要将滚动容易撑开，下面是比较常用的页面占满全屏的手段。
```
<View style={{ position: 'position', top: 0, bottom: 0, width: 750 }}>
  <RecyclerView />
</View>
```
- 现有的列表：
  - scrollview（水平滚动推荐）：无法做cell 回收，内容过多会有性能问题。
  - recyclerview（最常用高性能推荐方案）：不可水平滚动，性能有很大提升，是可回收的长列表，滚动体验流畅。
  - listview（RN习惯）：recyclerview 的上层包装，对标 RN 的能力 。对性能和列表样式展示有更高要求的推荐使用recyclerview。
  - waterfall（瀑布图场景推荐）：底层实现上也是 list 的一个扩展，在 API 能力上向 ListView 靠拢 
- 长列表的基础能力：[以 recyclerview 为例]
  - onEndReached：weex 中，此时如果cell的个数不变就不会重新加载，这种保护措施让我们避免了重复加载，但也导致如果在切换tab改变同一list的功能时导致不会更新，解决方案就是使用列表的resetScroll 方法充值列表的滚动情况。this.refs.list.resetScroll();
  - refreah： 下拉刷新是通过列表标签内的RefresControl组件实现的。RefresControl 需要放在列表的第一个元素。
  - appear：在元素出现的时候做一些事情。appear 需要绑定在滚动容器内，不然weex上无法生效。实际上是基于onScroll，过多的appear对于滚动性能会稍有影响。appear 是一个滑动过程中可能频繁触发的事件，在这里的 setState 逻辑需要自己把控好 。
  - onScroll：滚动过程中如果要做一些实时的操作会用到onScroll，另外在滚动过程中的动画操作我们推荐使用 BindingX，这个实现方案可以减小通信成本达到性能提升。
  - http://ju.outofmemory.cn/entry/347278

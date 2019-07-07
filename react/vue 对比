# react 与 vue 对比

1. 形式：
- vue ui 和 逻辑分开。
- react 使用 JSX 的形式，ui和逻辑混叠在一起。
2. 数据更新：
- vue ，在初始化的时候，使用Object.defineProperty 为data中的数据添加getter 和setter，实现双向绑定。数据发生变化后，会缓存同一个事件循环中发生的所有数据变化，异步更新DOM。数组的直接赋值和改变长度不会引起重新渲染，对象新添加的属性也不具有响应式。
- vue 具有计算属性，computed 、watch。
- react， 数据的更新必须使用setState，自由度更大，可以合并多个 setState来提高性能。在组件的props 和state 发生变化的时候会引起重新渲染。shouldComponentUpdate，这个钩子函数默认返回true ，如果返回false 不会执行后面的更新操作。
- 重新渲染的时候都采用了diff算法。
- react 重新渲染的时候，会将组件以及该组件的所有后代元素都通过diff算法重新渲染，所以结构应该尽量保持扁平化。vue  不会比较整棵树。
3. 事件处理：
- react 中，不能使用返回 false 的方式阻止默认行为。你必须明确的使用 preventDefault。 e.preventDefault();
- vue 中，提倡方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。所以增加了事件修饰符：`.stop、.prevent、.capture、.self、.once、.passive 等。`
4. refs：
- react 中需要先 创建 React.createRef()，再使用。
5. 组件的区别：
- 父组件向子组件传值方式：
  - props：
    - vue 和react 都有prop，且都可设置 类型、默认值、是否必须。子组件不可修改。
    - react 由于JSX的特性，可以在prop中传递组件。
  - render props： 值为函数的prop，在组件间共享代码的技术。（类似 vue中的slot）
  - context（跨级组件通信）：
    - vue 没有，可以使用vuex。
    - react 中提供的一种在组件之间共享类值得方法，而不必通过组件树的每个层级显式地传递props。context 相当于一个全局变量，是一个大容器，可以把要通信的内容放在这个容易中，想用的时候随意取用。官方不建议大量使用 context，context 作为一个全局变量，会导致走向混乱。
- 子组件向父组件通信：
  - 回调函数
  - 自定义事件
- 组件嵌套：
  - vue 中是 slot。
  - props.children。
  - <br />
- 没有嵌套关系的组件间通信（react）：
  - -监听组件：
    - 在componentDidMount事件中,如果组件挂载完成,再订阅事件（addListener）;
    - 在组件卸载的时候,在componentWillUnmount事件中取消事件的订阅（removeListener）;
  - 触发组件：
    - 使用 emit 方法触发。
- 高阶组件：
  - 接收一个组件作为参数，并返回一个新的组件。
  - vue 中 低版本的方法是mixin。容易污染，也不容易debug。
6. 状态管理：
- redux：
  - 提供 一个全局对象 store， store 中包含 state（用于保存状态） 和 reducer（唯一可修改 state中值的方法）
  - 整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中。
  - 惟一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象。通过 store.dispatch() 将 action 传到 store。action 内必须使用一个字符串类型的 type 字段来表示将要执行的动作，其他字段可以作为改变的值传入。
  - 通过reducer改变state tree，要求reducer是纯函数，即只要传入参数相同，返回计算得到的下一个 state 就一定相同。没有特殊情况、没有副作用，没有 API 请求、没有变量修改，单纯执行计算。注意： 不要修改 state， 在default 情况下返回旧的state。
  - 创建store的时候需要传入reducer，真正能改变store中数据的是store.dispatch API。
  - sore 提供的方法：
    - 提供 getState() 方法获取 state；
    - 提供 dispatch(action) 方法更新 state；
    - 通过 subscribe(listener) 注册监听器;
    - 通过 subscribe(listener) 返回的函数注销监听器。
  - 无法进行异步或辅助操作。
  - 插件middlewares， 提供action 被发起后，到达reducer之前的扩展点，可以用来进行日志记录、创建奔溃报告、调用异步接口或路由。
  - 异步解决方案可以使用 redux-thunk。
- vuex：
  - Vuex 的状态存储是响应式的。
  - <br />
7. React DOM 在渲染之前默认会 过滤 所有传入的值。它可以确保你的应用不会被注入攻击。所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 XSS(跨站脚本) 攻击。
7. 都是单向数据流，组件不可修改props。


1. this.state:React 的一大创新，就是将组件看成是一个状态机，一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染 UI 
1. <br />

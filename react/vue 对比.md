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
  - redux的流程： view——>action——>store——>reducer（返回）——>store——view
- vuex：
  - Vuex 的状态存储是响应式的。
  - vuex是吸收了Redux的经验并且对redux的进行了调整。
  - 用mutations 替换redux中的renducer。
  - 支持getter。
  - 提供 mapstate、mapgetter、mapmutations等方法，用于生成store内部属性对组件内部属性的映射。
  - 将store 传入根实例，使得store 对象在运行时存在于任何vue组件中。
  - 核心：
    - state：存放多个组件共享的状态（数据）
    - mutations：存放更改state里状态的方法，用于变更状态，是唯一一个更改状态的属性
    - getters：将state中某个状态进行过滤，然后获取新的状态，类似于vue中的computed
    - actions：用于调用事件动作，并传递给mutation
    - modules：主要用来拆分state
- 基本概述：
  - redux:
    - 核心对象：store
    - 数据存储：state
    - 状态更新提交接口：==dispatch==
    - 状态更新提交参数：带type和payload的==Action==
    - 状态更新计算：==reducer==
    - 限制：reducer必须是纯函数，不支持异步
    - 特性：支持中间件
  - vuex:
    - 核心对象：store
    - 数据存储：state
    - 状态更新提交接口：==commit==
    - 状态更新提交参数：带type和payload的mutation==提交对象/参数==
    - 状态更新计算：==mutation handler==
    - 限制：mutation handler必须是非异步方法
    - 特性：支持带缓存的getter，用于获取state经过某些计算后的值
 - redux 和 vuex 对比：
  - vuex，状态变更的触发只是一次提交而已。redux，状态变更必须是一次行为触发，action必须是一个对象。
  - vuex 取消action的概念。
  - vuex 中的mutation，根据入参对旧state转变而已。redux中的reducer，根据旧的state和action，规约出新的state。
7. React DOM 在渲染之前默认会 过滤 所有传入的值。它可以确保你的应用不会被注入攻击。所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 XSS(跨站脚本) 攻击。
7. 都是单向数据流，组件不可修改props。


1. this.state:React 的一大创新，就是将组件看成是一个状态机，一开始有一个初始状态，然后用户互动，导致状态变化，从而触发重新渲染 UI 
1. <br />

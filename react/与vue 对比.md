1. 渲染
- react:
  - 一个组件的状态发生变化，会将组件及该组件的所有后代元素 通过diff算法 重新渲染。但是当组件树很大时，仍然需要比较大的开销，react 的解决方案是 shouldComponent
  Update,以这个函数的返回结果判断是否继续执行 后面的 diff、patch、update。
  - 当props或者state改变时，PureComponent将对props和state进行浅比较。Component不会比较当前和下个状态的props和state。
- vue：
  - 响应式使用的Object.defineProperty 实现，在 getter 中收集依赖， setter 中派发更新，所以不会像 react 一样比较整棵树，vue中也有diff 算法，同级比较虚拟dom树。
 - 注意： vue 不需要人为关心更新，react 可以通过 shouldComponentUpdate 实现同样的效果，但是react 中，应该尽量保证结构的扁平化。
2. 状态数据跟改方式：
- react 推荐 ‘函数式编程’
```
// 推荐：
// 修改obj.b
modifyObj = () => {
    this.setState({
        obj: {
            ...this.state.obj,
            b: 3,
        }
    })
}

// 修改arr
modifyArr = () => {
    this.setState({
        arr: [...this.state.arr, 4],
    })
}
// 不推荐：
obj.b = 3；
this.setState({ obj })

pureComponent 中的 shouldComponentUpdate 是浅比较，如果直接修改对象或数组，会导致组件并不会发生更新。
```
- vue，修改状态简单，this.obj.b = 3，就会触发 setter。但是对于数组，虽然可以通过 push， unshift 等方式修改数组，但是类似 arr[index] = value 不会触发重新渲染。（vue3 采用 proxy，可以直接使用 arr[index]）
- 对比： vue 使用 Object.definedProperty，看似方便，但是当状态数据庞大的时候，需要不断的对状态数据执行监听，导致初始消耗更多，白屏事件会更长（据说这个问题也会在 vue3中得到解决）。react 何 redux 推崇 永远用新的值代替旧的值，方便 debug。
3. 关于 逻辑复用
- react 
  - 逻辑复用， 就是把通用的一些逻辑复用到需要这些逻辑的组件上。
  - renderProps，给组件添加一个值为函数的属性，这个函数可以在组件渲染的时候调用，这个函数可以给原有组件‘注入’其他组件的代码。
- vue
  - 注册为一个指令可实现逻辑的复用。https://cn.vuejs.org/v2/guide/custom-directive.html
- 对比：这两个都不常用。
4. 数据的流向：
- 组件之间都是单向数据流，子组件不允许改变props中的值。
- vue 中的 v-model，可以在表单<input>、<textarea>、<select> 元素上创建双向数据绑定，它实质是语法糖，负责监听用户的输入事件以更新数据，或者组件上创建双向数据绑定。
5. 高级组件：
- react： 函数接收的是一个组件，然后返回一个组件。
  ```
  function HOC(wrapperComponent) {
    return class getOrgTree extends React.Component {
        state = { orgTree: [] }
        
        componentDidMount() {
            fetch('xxxxxxx').then(orgTree => this.setState({ orgTree }))
        }
        
        render() {
            return <wrapperComponent orgTree={this.state.orgTree} {...this.props} />
        }
    }
  }
  ```
- vue：只能通过mixin 实现，容易污染，也不容易debug。
- 对比： react 通过面向对象的方式依然达到了一个高扩展性与灵活性，vue 在高阶函数中基本没用发挥余地，vue 是面向配置的。
6. 社区与周边生态：
- react 社区贡献 相当活跃，vue 相对平静很多。
7. 语法：
- react：
  - 需要手动调用 setState 进行重绘，否则页面中的值不会改变。
  - 使用 jsx 的方式进行模板的渲染，可混合使用js 和 html标签。{} 解析 js， （）解析 html。
- vue：
  - 在模板中直接使用data 对象中的数据，利用指令来处理渲染逻辑。
 - 对比： react 需要手动触发更新，虽然麻烦一点，但是自由度更大。
 8. vue 比 react 多了哪些常见属性
 - vue: 
  - computed --- 自动监听变化结果并重新计算、watch --- 指定监听某个状态变化，并获得该属性变化前后的值。
  - 利用指令 封装对 DOM 的操作。
  - slot -- 插槽，组件嵌套。
  - 无状态组件： 在template标签中加上functional，模板渲染后不会对数据进行监听。
 - react：
  - 需要在 componentWillReceiveProps 时自己去判断属性是否发生了变化，或者在 setState 的同时触发变化后的业务逻辑。
  - 本身利用 jsx 操作DOM。
  - React中没有<slot>这种语法，但组件本身可以将标签内的部分以props.children的方式传递给子组件。
  - 无状态组件：只起渲染作用的组件，并不需要状态变化或生命周期监听。可以使用 函数来接收和使用 props。
9. 无状态组件
10. 跨组件通信：
  - 指不通过 props传递获取父组件中定义的数据，这样深层的子组件就可以直接访问顶层的数据。
  - react 提供 context 这样的机制来实现。（写一个 案例~~~~~~~）
    - context 相当于一个全局变量，是一个大容器，可以把要通信的内容放在这个容易中，想用的时候随意取用。
    - 满足的条件：
      - 上级组件要声明自己支持的context，并提供一个函数来返回相应的context对象。
      - 子组件要声明自己需要使用context。
     - 官方不建议大量使用 context，context 作为一个全局变量，会导致走向混乱。
     ```
     
     import ListItem from './ListItem';

      class List extends Component {
          // 父组件声明自己支持context
          static childContextTypes = {
              color: PropTypes.string,
          }
          static propTypes = {
              list: PropTypes.array,
          }
          // 提供一个函数,用来返回相应的context对象
          getChildContext() {
              return {
                  color: 'red',
              };
          }
          render() {
              const { list } = this.props;
              return (
                  <div>
                      <ul>
                          {
                              list.map((entry, index) =>
                                  <ListItem key={`list-${index}`} value={entry.text} />,
                             )
                          }
                      </ul>
                  </div>
              );
          }
      }

      export default List;
      
      import React, { Component } from 'react';
      import PropTypes from 'prop-types';

      class ListItem extends Component {
          // 子组件声明自己要使用context
          static contextTypes = {
              color: PropTypes.string,
          }
          static propTypes = {
              value: PropTypes.string,
          }
          render() {
              const { value } = this.props;
              return (
                  <li style={{ background: this.context.color }}>
                      <span>{value}</span>
                  </li>
              );
          }
      }

      export default ListItem;
      
     ```
11. 没有嵌套关系的组件间通信：
- 监听组件：
  - 在componentDidMount事件中,如果组件挂载完成,再订阅事件（addListener）;
  - 在组件卸载的时候,在componentWillUnmount事件中取消事件的订阅（removeListener）;
- 触发组件：
  - 使用 emit 方法触发。
 12. 组件通信
 - react 组件：
    父组件向子组件通信: props
    子组件向父组件通信: 回调函数/自定义事件
    跨级组件通信: 层层组件传递props/context
    没有嵌套关系组件之间的通信: 自定义事件
    
    当业务逻辑复杂到一定程度,就可以考虑引入Mobx,Redux等状态管理工具
 - vue ： 
   父组件向子组件通信: props
   子组件向父组件通信: 回调函数/自定义事件
13. 高阶组件
- react：
  - 高阶组件就是一个函数，该组件接收一个组件作为参数，并返回一个新的组件。
  - 可以在其他组件中使用装饰器的语法来使用这个高阶组件。（被装饰的组件就相当于传入高级组件内部）
  - 除了在结构上对子组件进行增强外，还可以通过 props 增强子组件的功能，
14. 比较分类：
  - 生命周期
  - vue 比 react 多了哪些常用属性
  - 组件的区别
    - 组件通信
    - 组件嵌套
    - 无状态组件
    - 跨组件通信
    - react 高阶组件
  - 状态管理
    - 对于单页应用来说，web 应用就是一个状态机，视图与状态是一一对应的。
    - redux， 提供 一个全局对象 store， store 中包含 state（用于保存状态） 和 reducer（唯一可修改 state中值的方法）
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


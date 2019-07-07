
1. 要点：
- web 应用是一个状态机，视图与状态是一一对应的。
- 应用中的所有state 都以一个对象树的形式存储在一个单一的store中。唯一改变state的方法是触发action。action 是一个描述发生什么的对象，为了描述action如果改变state树，需要编写reducers。
- state 是只读的，唯一改变state的方法是触发action。
2. 基本做法： 用户发出action，renducer 函数算出新的state，view 重新渲染。     
- 什么使用：
  - 如果你的UI层非常简单，没有很多互动，Redux 就是不必要的，用了反而增加复杂性。
  - Redux 的适用场景：多交互、多数据源。
- 从组件的角度考虑：
  - 某个组件的状态，需要共享。
  - 某个状态需要在任何其他地方拿到。
  - 一个组件需要改变全局状态。
  - 一个组件需要改变另一个组件的状态。
3. 基本概念和API
- store：
  - 保存数据的地方。
  ```
  import { createStore } from 'redux';
  const store = createStore(render); // 该函数的第二个参数表示state的最初状态，这通常是服务器给出的。它会覆盖reducer 函数的默认初始值。
  ```
- state:
- action:
  - 描述当前发生的时间，是改变state的唯一办法，它会运送数据到store。
  ```
  const action = {
    type: 'ADD_TODO',
    payload: 'Learn Redux'
  };
  ```
- action creator：
  - view 要发送多少种消息，就会有多少种action。定义一个函数来生成action，这个函数就是action creator。
  ```
  const ADD_TODO = '添加 TODO';

  function addTodo(text) {  // 就是一个 action creator
    return {
      type: ADD_TODO,
      text
    }
  }

  const action = addTodo('Learn Redux');
  ```
- store.dispatch(): 
  - 是view 发出action的唯一方法。
  - 以后每当store.dispatch发送过来一个新的 Action，就会自动调用 Reducer，得到新的 State。
  - store.dispatch(addTodo('Learn Redux'));
- reducer:
  - Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。
  - 由于reducer 是纯函数，同样的state，必定得到同样的view。也因此，renducer 里面不能修改state，必须返回一个全新的对象。
  ```
    const defaultState = 0;
    const reducer = (state = defaultState, action) => {
      switch (action.type) {
        case 'ADD':
          return state + action.payload;
        default: 
          return state;
      }
    };
    // State 是一个对象
    function reducer(state, action) {
      return Object.assign({}, state, { thingToChange });
      // 或者
      return { ...state, ...newState };
    }

    // State 是一个数组
    function reducer(state, action) {
      return [...state, newItem];
    }
   ```
- store.subscribe()
  - 通过该方法设置监听函数，一旦state发生变化，就会自动执行这个函数。
  - 显然，只要把 View 的更新函数（对于 React 项目，就是组件的render方法或setState方法）放入listen，就会实现 View 的自动渲染。
  - store.subscribe方法返回一个函数，调用这个函数就可以解除监听。
  ```
  let unsubscribe = store.subscribe(() =>
    console.log(store.getState())
  );
  unsubscribe();
 ```
- 中间件的概念：
  - 中间件就是一个函数，对store.dispatch方法进行了改造，在发出action和执行reducer 这两步之间，添加了其他功能。
  - 有些中间件 有次序要求，使用前可查一下文档。
  - applyMiddleware，是 redux 的原生方法，它会将所有中间件组成一个数组，依次执行，最后执行store.dispatch，中间件的内部，可以拿到 getState 和 dispatch 两个方法。
  ```
    import { applyMiddleware, createStore } from 'redux';
    import createLogger from 'redux-logger'; // 这就是一个中间件。
    const logger = createLogger();

    const store = createStore(
      reducer,
      applyMiddleware(logger)
    );
    异步操作的基本思想：
    action的种类不同：同步操作只要发出一种action即可，异步操作可以发出三种action（操作发起时的 action， 操作成功时的 action， 操作失败时的 action）。


    // 写法一：名称相同，参数不同
    { type: 'FETCH_POSTS' }
    { type: 'FETCH_POSTS', status: 'error', error: 'Oops' }
    { type: 'FETCH_POSTS', status: 'success', response: { ... } }

    // 写法二：名称不同
    { type: 'FETCH_POSTS_REQUEST' }
    { type: 'FETCH_POSTS_FAILURE', error: 'Oops' }
    { type: 'FETCH_POSTS_SUCCESS', response: { ... } }
    state：
    let state = {
      // ... 
      isFetching: true, // 是否抓取数据。
      didInvalidate: true, // 数据是否过时。
      lastUpdated: 'xxxxxxx' // 上一次更新时间。
    };
   ```
- 异步操作的思路：
  - 操作开始时，送出一个 action，触发 state 更新为‘正在操作’状态，view 重新渲染。
  - 操作结束后，再送出一个action，触发state更新为‘操作结束’状态，view 再一次重新渲染。
- redux-thunk：
  - 异步的解决方案，就是写一个返回函数 action creator， 然后使用redux-thunk 中间件改造 store.dispatch
  ```
    import { createStore, applyMiddleware } from 'redux';
    import thunk from 'redux-thunk';
    import reducer from './reducers';

    // Note: this API requires redux@>=3.1.0
    const store = createStore(
      reducer,
      applyMiddleware(thunk)
    );

    const fetchPosts = postTitle => (dispatch, getState) => {
      // 先发出一个action，然后进行异步操作。拿到结果后，先将结果转成json格式，然后再发出一个action
      dispatch(requestPosts(postTitle));
      return fetch(`/some/API/${postTitle}.json`)
        .then(response => response.json())
        .then(json => dispatch(receivePosts(postTitle, json)));
      };
    };

    // 使用方法一
    store.dispatch(fetchPosts('reactjs')); // fetchPosts 是 一个 action creator，返回一个函数。
    // 使用方法二
    store.dispatch(fetchPosts('reactjs')).then(() =>
      console.log(store.getState())
    );
  ```
- redux-promise：
  - 可以实现让action creator 返回一个promise对象。
  - http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_two_async_operations.html

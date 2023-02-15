# 一、redux是什么？

### 1、redux概念

它可以用在react，angular,vue等项目中，但基本与react配合使用

作用：集中式管理react应用中多个组件共享状态

### 2、使用redux情况

某个组件的状态，需要让其他组件可以随时拿到（共享）

一个组件需要改变另一个组件的状态（通信）

总体原则：能不用就不用，如果不用比较吃力才考虑使用

# 二、redux的三个核心概念

### 1、action

1. 动作的对象

2. 包括2个属性：

   1. type：标识属性，值为字符串，唯一，必要属性

   2. data：数据属性，值类型任意，可选属性




例子：

```
{type:'ADD_STUDENT',data:{name:'tom',age:18}}
```



### 2、reducer

用于初始化状态、加工状态

加工时，根据旧的state和action，产生新的state的纯函数



### 3、store

(1)将state/action/reducer联系在一起的对象;

(2)如何得到此对象:

```
import {createStore} from 'redux';
import reducer from './reducers'
const store = createStore(reducer)
```


(3)此对象的功能？

getState():得到state;

dispatch(action):分发action,触发reducer调用，产生新的state;

subscribe(listener):注册监听，当产生了新的state时，自动调用的展示，要靠我们自己写。



# 三、案例

### 1、store.js文件

```
//该文件专门用于暴露一个store对象，整个应用只有一个store对象

//引入createStore,，专门用于创建redux中最核心的store对象
import {createStore, applyMiddleware} from 'redux';
//引入为Count组件服务的reducer
import countReducer from './count_reducer'
//引入redux-thunk，用于支持异步action
import thunk from 'redux-thunk'
const store = createStore(countReducer, applyMiddleware(thunk))
//暴露store
export default store
```

### 2、count_reducer.js

2、count_reducer.js

```
/*
1、该文件是用于创建一个Count组件服务的reducer，reducer的本质就是一个函数
2、reducer函数会接到两个参数，分别为：之前的状态（preState）,动作对象（action）
3、reducer被第一次调用时，是store自动触发的，传递的preState是undefined,传递的action是类似于：{
 type: '@@REDUX/INIT_a.2.b.4'
}
*/
const {INCREMENT, DECREMENT} from './constant'
const initState = 0;//初始化状态，推荐写法

export default function countReducer (preState = initState, action) {
//if(preState === undefined) preState = 0
//从action对象中获取：type、data
 const { type, data} = action
 //根据type决定如何加工数据
 switch (type) {
  case INCREMENT://如果是加
    return preState + data;
   case DECREMENT://如果是减
    return preState - data;
   default: 
    return preState
 }
}
```

### 3、count_action.js

```
/*
 该文件专门为Count组件生成action对象
*/

function createIncrementAction(data) {
 return {
  type:'increment',
  data
 }
}

function createDecrementAction(data) {
 return {
  type:'decrement',
  data
 }
}

//改造之后
const {INCREMENT, DECREMENT} from './constant'

//同步action，就是指action的值为Object类型的一般对象
export const createIncrementAction = data => ({type:INCREMENT,data})
export const createDecrementAction = data => ({type:DECREMENT,data})

//异步action，就是指action的值为函数,异步action中一般都会调用同步action，异步action不是必须要用的。
export const createIncrementAsyncAction = (data, time) => {
 return (dispatch) => {
  setTimeout(() => {
   //函数体
   dispatch(createDecrementAction(data));
  }，time)
 }
}
```

### 4、constant.js

```
/*
 该模块是用于定义action对象中type类型的常量值，目的只有一个：便于管理的同时防止在书写单词的时候，出现错误
*/

export const INCREMENT = 'increment'
export const DECREMENT = 'decrement';
```

### 5、在使用的文件中引入

```
//引入store，用于获取redux中保存的状态
import store from '../../redux/store'
//引入actionCreator专门用于创建action对象
import {createIncrementAction,createDecrementAction,createIncrementAsyncAction} from '../../redux/count_action'

//componentDidMount() {
 //监测redux中状态的变化，只要变化，就调用render
 //store.subscribe(() => {
   //this.setState({})
 //})
//}

//加法
increment = () => {
 const { value } = this.selectNumber;
 //store.dispatch({type:'increment', date : value * 1});
 store.dispatch(createIncrementAction(value * 1));
}
//减法
decrement = () => {
 const { value } = this.selectNumber;
 //store.dispatch({type:'decrement', date : value * 1});
 store.dispatch(createDecrementAction(value * 1));
}

//奇数再加
incrementIfOdd = () => {
  const { value } = this.selectNumber;
  const count = store.getState();
  if (count % 2 !== 0) {
   //store.dispatch({type:'increment',data : value * 1})
   store.dispatch(createIncrementAction(value * 1));
  }
}
incrementAsync = () => {
 const { value } = this.selectNumber;
 store.dispatch(createIncrementAsyncAction(value * 1 , 500))
}

render() {
 return (
    <div>
     <h1>当前和为: {store.getState()}</h1>
   </div>
  
 )
}
```

监测redux中状态的改变，如redux的状态发生了变化，那么重新渲染App组件

```
import React from "react";
import ReactDOM from "react-dom";
import App from './App';
import store from './store/store';
ReactDOM.render(<App/>,document.getElementById('root'))
// 在这里需要明确的是：redux只是一个状态的管理机制，它不会自动的触发页面的更新，需要我们自己去写
store.subscribe(() => ReactDOM.render(<App/>,document.getElementById('root')))
```

备注：redux只负责管理状态，至于状态的改变驱动着页面，需要自己去写

# 四、action

两种类型：Object和function

Object:同步action

function:异步action

























































































---
title: cookie
layout : default
---

## redux思路整理

1.最简单的显示静态数据

需要建立基本的 store.js   并注意createStore必须包含Reducer函数，后两者可以选择

```js
import {createStore} from 'redux';

let cmtNum = 0


function Reducer( state , action) {
  return state
}


const defaultState = {
  cmtNum
}
const store = createStore(Reducer,defaultState);

export default store

```
index.js 中引入

```js
import store from './store.js';
```
```js
store.getState()
````
就可以获取相应的值

2.

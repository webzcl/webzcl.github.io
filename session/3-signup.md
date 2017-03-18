---
title: 用户注册
layout : default
---

## 用户注册

这集开始，我们用前后台分离架构，来实现用户登录态管理。


### 基本思路

不要求大家去写后台代码，后台代码会给大家，必要的原理，Peter 会介绍的。我们着重采用 Axios+React+Webpack 这套技术，来实现前端工能。


### 开始第一个任务：把自己的 React 环境准备好

要求：

- 能用 Webpack+Babel 编译 ES6
- 能编译 React 的 JSX 语法


新建项目：

```
mkdir tiger
cd tiger
npm init -y
```

然后，从以前的项目中，拷贝 package.json （ 包含 webpack-react-babel 的各个包），拷贝 .babelrc 文件。

然后，运行

```
npm i
```

开始装包。

然后，就来添加 .gitignore 文件，内容

```
node_modules
bundle.js
```

### 任务：编译 ES6

要求，index.js 中，写几句 ES6 代码。用 webpack-babel 把 index.js 编译成 bundle.js ，并且在浏览器中执行。

代码： [webpack compile es6](https://github.com/happypeter/tiger/commit/608c20412513ce94d691648d2ab338a03804ce1e)


### 任务：代码放到一个 github 上的仓库中

要求：

- 可以自由的进行 push 操作


### 任务：编译 JSX

要求，写一个 React 的 Hello World ，编译执行


代码： [compile React](https://github.com/happypeter/tiger/commit/843889f0fcb871fc5f74e72efc5a286ca91c7bca)

如果遇到这样的浏览器报错：

```
Target container is not a DOM element.
````

翻译：目标容器不是一个 DOM 元素

问题就是处在 ReactDom 中 getElementById 没有真正选中一个 DOM 节点，很可能是 id 名写错了。


### 任务：添加 React-Router

要求：有两个页面一个 /login 还有一个首页

参考：

- [写一个 React Router 的 Hello World](https://happypeter.github.io/digicity/react/3-router-hello.html)
- [官网](https://reacttraining.com/react-router)






### 以下是备忘内容：

https://haoqicat.com/hand-in-hand-react/23-header-state‘’



可以设置一个生命周期函数

```
constructor(){
  this.state(
    currentUser: ''
    )
}

ComponentWillMount(){
  axios.get('/currentUser').then(res => {
    this.setState(currentUser: res.currentUser)
    })
}
```


这样显示登录状态的字符串（需要在同一个组件内，不然就要用 redux ）

```
this.state.currentUser? this.state.currentUser.name:"登录"
```


服务器端对应的代码

```
app.get('/currentUser', function(){
  res.json(req.session.currentUser)
  })
```


这样基本就可以实现登录效果了，刷新页面也不怕。



### 用户注册

https://coding.net/u/newming/p/shopapi/git



```
➜  ~ curl -X POST -H 'Content-Type: application/json' -d '{"username":"peter", "password":"111111"}' http://api.duopingshidai.com/user/signup
{"userId":"58cc967681eaba5480e0890a","username":"peter","msg":"注册成功"}%
```

退出登录

/logout 只是返回一下 msg ，实际什么都不做。客户端直接把 userId 删除即可。

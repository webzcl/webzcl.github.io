---
title: 嵌套 UI ，嵌套路由
layout : default
---

## 嵌套 UI ，嵌套路由

参考： https://github.com/reactjs/react-router-tutorial/tree/master/lessons/04-nested-routes



### 代码调整


```diff
diff --git a/src/components/App.js b/src/components/App.js
index 9ae6a28..1107af4 100644
--- a/src/components/App.js
+++ b/src/components/App.js
@@ -8,6 +8,8 @@ class App extends Component {
       <div>
         <Link to='/hello1'>Hello1</Link>
         <Link to='/hello2'>Hello2</Link>
+        { this.props.children }
+        <div>footer</div>
       </div>
     )
   }
diff --git a/src/routes.js b/src/routes.js
index 227342d..9aeb23d 100644
--- a/src/routes.js
+++ b/src/routes.js
@@ -1,5 +1,5 @@
 import React from 'react';
-import { Router, Route, browserHistory } from 'react-router';
+import { Router, Route, browserHistory, IndexRoute } from 'react-router';
 import Hello1 from './components/Hello1';
 import Hello2 from './components/Hello2';
 import App from './components/App';
@@ -7,9 +7,11 @@ import App from './components/App';

 const renderRoutes = () => (
   <Router history={browserHistory}>
-    <Route path='/' component={App} />
-    <Route path='/hello1' component={Hello1} />
-    <Route path='/hello2' component={Hello2} />
+    <Route path='/' component={App} >
+      <Route path='/hello1' component={Hello1} />
+      <Route path='/hello2' component={Hello2} />
+      <IndexRoute  component={Hello1} />
+    </Route>
   </Router>
 );

```
## 深入理解 react-router 路由系统

在 web 应用开发中，路由系统是不可或缺的一部分。在浏览器当前的 URL 发生变化时，路由系统会做出一些响应，用来保证用户界面与 URL 的同步。随着单页应用时代的到来，为之服务的前端路由系统也相继出现了。有一些独立的第三方路由系统，比如 director，代码库也比较轻量。当然，主流的前端框架也都有自己的路由，比如 Backbone、Ember、Angular、React 等等。那 react-router 相对于其他路由系统又针对 React 做了哪些优化呢？它是如何利用了 React 的 UI 状态机特性呢？又是如何将 JSX 这种声明式的特性用在路由中？

### 一个简单的示例

现在，我们通过一个简易的博客系统示例来解释刚刚遇到的疑问，它包含了查看文章归档、文章详细、登录、退出以及权限校验几个功能，该系统的完整代码托管在 JS Bin（注意，文中示例代码使用了与之对应的 ES6 语法），你可以点击链接查看。此外，该实例全部基于最新的 react-router 1.0 进行编写。下面看一下 react-router 的应用实例：

```
import React from 'react';
import { render, findDOMNode } from 'react-dom';
import { Router, Route, Link, IndexRoute, Redirect } from 'react-router';
import { createHistory, createHashHistory, useBasename } from 'history';

// 此处用于添加根路径
const history = useBasename(createHashHistory)({
  queryKey: '_key',
  basename: '/blog-app',
});

React.render((
  <Router history={history}>
    <Route path="/" component={BlogApp}>
      <IndexRoute component={SignIn}/>
      <Route path="signIn" component={SignIn}/>
      <Route path="signOut" component={SignOut}/>
      <Redirect from="/archives" to="/archives/posts"/>
      <Route onEnter={requireAuth} path="archives" component={Archives}>
        <Route path="posts" components={{
          original: Original,
          reproduce: Reproduce,
        }}/>
      </Route>
      <Route path="article/:id" component={Article}/>
      <Route path="about" component={About}/>
    </Route>
  </Router>
), document.getElementById('example'));
```
如果你以前并没有接触过 react-router，相反只是用过刚才提到的 Backbone 的路由或者是 director，你一定会对这种声明式的写法感到惊讶。不过细想这也是情理之中，毕竟是只服务与 React 类库，引入它的特性也是无可厚非。仔细看一下，你会发现：

- Router 与 Route 一样都是 react 组件 ，它的 history 对象是整个路由系统的核心，它暴漏了很多属性和方法在路由系统中使用；

- Route 的 path 属性表示路由组件所对应的路径，可以是绝对或相对路径，相对路径可继承；

- Redirect 是一个重定向组件，有 from 和 to 两个属性；

- Route 的 onEnter 钩子将用于在渲染对象的组件前做拦截操作，比如验证权限；

- 在 Route 中，可以使用 component 指定单个组件，或者通过 components 指定多个组件集合；

- param 通过 /:param 的方式传递，这种写法与 express 以及 ruby on rails 保持一致，符合 RestFul 规范；

##  关于hashHistory和browserHistory使用的区别

React-router是为react专门构建的一个路由插件，他可以帮助我们实现简单的单页应用效果，学习react的人，避免不了学习react-router的用法。

hashHistory ： 不需要服务器配置，在URL生成一个哈希来跟踪状态，通常在测试环境使用，也可以作为发布环境使用。

```
import { Provider } from 'react-redux'
import { Router, hashHistory} from 'react-router'

ReactDOM.render((
    <Provider store={store}>
        <Router history={hashHistory}>
            <Route>
                //你的route
            </Route>
        </Router>
    </Provider>),
    document.getElementById('root')
);
```
browserHistory ： 需要服务器端做配置，路径是真实的URL，是官方推荐首选。

  客户端配置

```

import { Provider } from 'react-redux'
import { Router, browserHistory } from 'react-router'

ReactDOM.render((
    <Provider store={store}>
        <Router history={browserHistory}>
            <Route>
                //你的route
            </Route>
        </Router>
    </Provider>),
    document.getElementById('root')
);
```
服务器端配置

```

const express = require('express')
const path = require('path')
const port = process.env.PORT || 8080
const app = express()

// 通常用于加载静态资源
app.use(express.static(__dirname + '/public'))

// 在你应用 JavaScript 文件中包含了一个 script 标签
// 的 index.html 中处理任何一个 route
app.get('*', function (request, response){
  response.sendFile(path.resolve(__dirname, 'public', 'index.html'))
})

app.listen(port)
console.log("server started on port " + port)
```
- 解释一下为什么browserHistory需要服务端配置，因为真实URL其实是指向服务器资源，比如我们经常使用的API接口，也是一个真实URL的资源路径，当通过真实URL访问网站的时候，第一次访问的是网站的域名，这个时候可以正常加载我们的网站js等文件，而用户手动刷新网页时，由于路径是指向服务器的真实路径，服务器端没有做路由配置，就会导致资源不存在，用户访问的资源不存在，返回给用户的是404错误。

- 通过hashHistory来生成的URL就不会出现这样的问题，因为他不是指向真实的路由。

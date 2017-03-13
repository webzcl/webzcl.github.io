---
title: 上手 Express 框架
layout: default
---



### 服务器全局工具包，架设服务器（前端安装此包）：

- npm  i -g http-server
- 装包之后直接运行http-server . 即在当前文件夹下架设服务器，选择第一个端口或还是用默认的 localhost：8080 就可以在浏览器就可以访问。
- 但注意：用 http-server 会产生浏览器缓存，在浏览器设置清理即可

### curl

- 用curl测试API,是一个安装在新系统命令个行的工具，可以用来发http请求，用来测API
- curl -X GET 'http://localhost:3000/username' 发送GET请求的时候，-X可以不写

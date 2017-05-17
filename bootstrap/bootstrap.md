---
title: boostrap
layout : default
---

## boostrap



### CSS3-Media Query

1.常见属性：

device-width，device-height-----屏幕宽高（物理）
width，height -----渲染窗口宽高（浏览器）
orientation -----设备方向（横屏、竖屏）
resolution -----设备分辨率

2.基本的语法

外联、内嵌。

001.外联
```css
<link type="text/css" rel="stylesheet" href="link.css" media="only screen and (max-width:480px)"/>

```
 当屏幕的宽度小于等于480px时，使用这个css

002.内嵌

```html
<style>
$media screen and (min-width:480px){
body{background:blue;}
}
</style>

```

 当屏幕的宽度大于480px时，使用这个css


 ### 响应式布局之bootstrap框架：
 
1、是一种移动优先的前端框架；
2、优点：写非常少的代码，即可实现多终端的页面适配；
3、源文件主要有两部分构成，即CSS,JS和font字体；
4、bootstrap的源代码是一些Less文件，不改变源代码的情况下可以直接下载编译后的文件；
5、支持几乎所有浏览器，对于IE8/9需要引入Respond.js文件激活IE8/9对Media Query的支持；
6、最好把respond.js和网站部署在同一个域名下，避免跨域问题

---
layout: post
title:  "探索react技术栈-技术选型"
date:   2017-2-16
author: ihtml5
categories: [deep into react]
---

### 一.前言

  陆陆续续接触react有一年多了，深感[react](http://facebook.github.io/react)的简单优雅，急切地想用react去开发程序。但是热情之后，发现react社区的种种问题。比如在社区打打常常提到的 [angular](https://angular.io/) vs [react](http://facebook.github.io/react)。react作为view层的库，
并没有给我们提供像[angular](https://angular.io/)那样全方位的解决方案。社区很多围绕[react](http://facebook.github.io/react)的解决方案层出不断，尚没有形成一致的最佳实践。那么，在现有的react解决方案下，我们能否提炼出一个行之有效的方案呢，笔者认为可以从以下几方面入手:

1. 技术选型
2. 项目目录划分
3. 应用程序状态管理
4. 前后台交互
5. 测试
6. 迭代式开发

本文作为探索react技术栈第一篇，首先来聊一聊基于react技术栈的技术选型。


### 二.技术选型的意义

1.**View(react)**

   使用react来构造view

2.**状态管理(redux or mobx)**

   [redux](http://www.github.com/reactjs/redux)和[mobx](https://github.com/mobxjs/mobx)是社区两个最著名的状态管理框架。可以选择其中一种，因为redux作者是react核心团队的开发者，基于redux的社区也非常庞大，推荐使用redux

3.**路由(react-router)**

   [react-router](https://github.com/ReactTraining/react-router)是react社区公认的路由框架，但是这个库更新频繁，api变动比较大，笔者推荐使用其较稳定的v2.8.1
  
4.**样式**

   当前围绕react的样式解决方案，有三种即传统class声明，css in js,css module
   
5.**语言(Es6)**

   对浏览器要求不高，即满足ie9+以上的，可以使用es6开发应用，然后通过[babel](http://www.babeljs.io)转码，对于浏览器要求较高的，使用es5来编写，并引入pollify来支持浏览器兼容

6.**fetch**

<<<<<<< HEAD
  [fetch spec](https://fetch.spec.whatwg.org/)使用promise接口来进行后端接口请求，相比ajax来说，使用更加方便，在项目中，
  推荐使用fetch的[官方实现](https://github.com/github/fetch)


7. **构建工具(webpack)**
=======
  [fetch spec](https://fetch.spec.whatwg.org/)使用promise接口来进行后端接口请求，相比ajax来说，使用更加方便，在项目中，推荐使用fetch的[官方实现](https://github.com/github/fetch)
 
7.**构建工具(webpack)**
>>>>>>> f1cfd6be6a447571dd4b11ff2a17f160b48bd46f

   [webpack](http://webpack.js.org)是社区公认的优秀打包工具，和react非常搭。配合[gulp](http://gulpjs.com/)来完成流畅地前端开发。

8.**测试(jest or enzyme)**

  facebook推出的react测试工具[jest](http://facebook.github.io/jest)和airbnb推出的[enzyme](http://airbnb.io/enzyme/)都可以用来测试react

9.**mock(node or json mock server)**

  基于react的开发，几乎都是前后端分离，通过mock后端的接口，可以加快前端的开发效率。构建mock接口，一可以通过node来自己编写mock server或者可以通过现有的json mock server比如[jsonyeah](http://www.jsonohyeah.com/)

10.**异步数据流处理**

  对于简单的异步数据处理我们可以使用[redux-thunk](https://github.com/gaearon/redux-thunk)或者[redux-promise](https://github.com/acdlite/redux-promise),对于复杂的异步交互，可以使用[redux-observable](http://www.github.com/redux-observable/redux-observable)和[redux-sagas](https://github.com/redux-saga/redux-saga)



### 相关链接

1. [react howto](https://github.com/petehunt/react-howto)
  
2. [React + Redux 最佳实践](https://github.com/sorrycc/blog/issues/1)

---

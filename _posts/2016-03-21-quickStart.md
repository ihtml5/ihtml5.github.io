---
layout: post
title:  "快速搭建react的开发环境"
date:   2016-03-21
author: ihtml5
categories: [react]
cover: /assets/instacode.png
description: 'react框架因其简洁的api设计,生命式语法，组件化设计，单向数据流等特点日益受到广大开发者的关注。这篇文章就简要概述下如何快速搭建react的开发环境。包括webpack,babel简单介绍，前后端联调等'
---

&nbsp;&nbsp;&nbsp;&nbsp;[react](http://facebook.github.io/react)是facebook 2013年推出的开源框架库,react专注于web开发的View层,2015年随着[react native](http://facebook.github.io/react-native)的推出，react得到了进一步发展，成为2015年前端社区最活跃的框架，国内外诸多公司投入react社区具体可以[这里](https://github.com/facebook/react/wiki/Sites-Using-React)

  **webpack**

 &nbsp;&nbsp;&nbsp;&nbsp;[webpack](https://github.com/webpackWebpack)是德国开发者 Tobias Koppers 开发的模块加载器,Instagram 工程师认为这个方案很棒,在webpack里js, css, 图片等资源都可以当成模块来处理。因此, 在Webpack当中 js 可以引用 css, css 中可以嵌入图片 dataUrl,对应各种不同文件类型的资源, Webpack 有对应的模块 loader,比如 React jsx语法解析用的是 babel-loader,其他还有很多loader:http://webpack.github.io/docs/list-of-loaders.html。loader一般配置在根目录下的webpack.config.js文件中</br>

  **jsx**
  
  &nbsp;&nbsp;&nbsp;&nbsp;[jsx](http://facebook.github.io/jsx/),是facebook发明的适用于react的模板语法，在jsx中你可以编写js,声明css，生成react的虚拟dom。通过jsx语法，开发者可以快速构建开发组件。</br>

  **babel**
  
  &nbsp;&nbsp;&nbsp;&nbsp;[babel](http://www.http://babeljs.io/)是一个javascript编译器,在react项目中babel主要起到两个作用：1.解析jsx语法 2.将编写react组件的es2015语法转化为现阶段浏览器都兼容的es5语法

### 开始开发
  &nbsp;&nbsp;**开发前准备工作**<br>
    &nbsp;&nbsp;&nbsp;&nbsp;1. 整个开发所有的编译打包工具都依赖于node.js，开发前首先需要安装下[node.js](http://www.nodejs.org)
    &nbsp;&nbsp;&nbsp;&nbsp;2. 直接到svn里面checkout最新的前端代码示例。            

  &nbsp;&nbsp;**代码示例解读**
  
&nbsp;&nbsp;&nbsp;&nbsp;代码目录中assets存放源文件包括css,js,fonts,本地模拟数据等,dest文件夹下是打包后的bundle.js文件,webpack.config.js是webpack配置文件,告诉webpack如何加载和解析资源,详细使用可以参考[react和webpack小人书](https://www.gitbook.com/book/yimity/react-webpack-cookbook/details)这本电子书 package.json文件是告诉node.js，本项目依赖于哪些npm包</br>

  &nbsp;&nbsp;**快速开发**<br>
  &nbsp;&nbsp;&nbsp;&nbsp;利用现有的示例代码，只需要简单几个命令，就可以快速开发。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.在下载的前端项目根目录下运行 npm i，这个命令的目的是：检查项目所需要的依赖是否安装完全
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. 继续在项目根目录下运行webpack -p,这个命令主要是生成线上可用的bundle.js文件
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3. 打开另外一个命令行，同样是进入根目录，运行npm start,会启动webpack-dev-server命令，这个命令的作用是：<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(1)开启一个localhost:8080的代理服务 
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(2)开发时若有文件修改，webpack-dev-server就会自动刷新页面
&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;4. 有时候webpack-dev-server命令并不能实时更新生成bundle.js 我们还需要在根目录下运行webpack -w命令。

**通过以上几步我们就可以跑起来react应用啦。**


### 前后端联调

  &nbsp;&nbsp; **前后端通信方式**

  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;前后端通过api进行通信，通信格式为json

  &nbsp;&nbsp;**前后端联调**<br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;按照上面“快速开发”步骤中部署好前端环境后，然后将前端项目中的index.html文件放到java项目相应位置，并修改index.html中js，css资源，比如之前页面中引入的资源地址：
```javascript
    <link href="assets/css/amazeui.min.css"/>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css">  
    <link href="assets/css/app.css"/>
    <script src="dest/bundle.js" charset="utf-8"></script>
```
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;现在需要将所有css,js资源更改为
```javascript
    <link href="http://localhost:8080/assets/css/amazeui.min.css"/>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css">  
    <link href=="http://localhost:8080/assets/css/app.css"/>
    <script src="http://localhost:8080/dest/bundle.js" charset="utf-8"></script>
```
完成以上步骤后，开启java服务器环境，就可以进行页面调试了。


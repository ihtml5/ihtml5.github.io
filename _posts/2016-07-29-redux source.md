---
layout: post
title:  "redux源码解读"
date:   2016-08-21
author: ihtml5
categories: [react]
cover: /assets/instacode.png
tags: redux
description: 'redux源码短小精悍。本文尝试从源码角度解读redux,以便更深刻地理解redux。'
---


### **一.目录分析**

#### 1.src

  > 项目的源代码,包括以下几个文件：
  
  + **index.js**
  
  > 整个redux框架的入口文件
  > **作用**: 导出redux的几大函数包括createStore,bindActionCreators,combineReducers,compose,applyMiddleware
  
  + **createStore.js**
  
  > 创建应用唯一的state树
  
  + **bindActionCreators.js**
  
  > 工具类函数
  > **作用**: 方便开发者将dispatch和actioncreator当props绑定到组件中
  
  + **combineReducers.js**
  
  > 将多个reducer,合并成一个reducer,传入到createStore函数中
  
  + **compose.js**
  
  > 将多个函数组合执行
  
  + **applyMiddleware**
  
  > 工具类函数 
  > **作用:** 将中间件如[redux-thunk](https://github.com/gaearon/redux-thunk)应用到createStore函数上
  
  + **util/warning.js**
  
  > 自定义的错误信息提示函数

#### 2.docs

  > redux的文档.
  > 官方网站:[www.redux.js.org](http://www.redux.js.org)
  > 中文翻译:[cn.redux.js.org](http://cn.redux.js.org)

#### 3.build

  > 构建redux所需要的一些文件

#### 4.examples

  > redux的使用案例,从简单的原生counter到复杂到真实场景的应用,都提供了案例参考

#### 5.test

  > 测试文件目录

#### 6.node_modules

  > redux源码所依赖的node包

***

### **源码分析**

#### **1.src/index.js**

+ **关键词**

>  源代码使用了es6语法,使用import从文件中导出es6模块
> [import用法](http://es6.ruanyifeng.com/#docs/module#import命令)

+ **源码解读**

    1.导出redux的各个主要模块导出redux的各个主要模块

  {% highlight javascript %}
       // 绑定reducer和state的关系
       import createStore from './createStore'
       // 导出警告函数
       import warning from './utils/warning'
       // 导出自动绑定函数 自动绑定函数，主要生成dispatch(actionCreator(action));
       import bindActionCreators from './bindActionCreators'
       // 导出应用中间件函数,中间件主要作用是将发往reducer的action进行多次修改
       import applyMiddleware from './applyMiddleware'
       /* 合并多个reducer,这样方便每个reducer只处理store的某一个部分数据，最后通过
       * combineReducers函数合并
       */
       import combineReducers from './combineReducers'
       // 将多个函数合并在一起
       import compose from './compose'
  {% endhighlight %}  

  2.在开发环境下使用压缩版本给予警告
   
    {% highlight javascript %}
      function isCrushed() {}
       if (process.env.NODE_ENV !== 'production' && typeof isCrushed.name === 'string' 
        && isCrushed.name !=='isCrushed') {
           warning(
            'You are currently using minified code outside of NODE_ENV === \'production\'. ' +
            'This means that you are running a slower development build of Redux. ' +
            'You can use loose-envify (https://github.com/zertosh/loose-envify) for browserify ' +
            'or DefinePlugin for webpack (http://stackoverflow.com/questions/30030031) ' +
            'to ensure you have the correct code for your production build.'
            )
       }
    {% endhighlight %}
   
  3.导出多个对象
   
    {% highlight javascript %}
      export {
          createStore,
          compose,
          warning,
          combineReducers,
          bindActionCreators
      }
    {% endhighlight %}

#### **2.src/utils/warning.js**

+ **关键词**

> 1. [export default](https://defed.github.io/%E6%A8%A1%E5%9D%97/) 
> 2. [javascript中异常处理](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)
> 3. [javascript中错误处理](https://davidwalsh.name/fix-javascript-errors)
> 4. [阮一峰谈javascript错误处理](http://javascript.ruanyifeng.com/grammar/error.html#toc5)

+ **源码解读**

   1.判定console.error是否存在且可用
  
  {% highlight javascript %}
    // 导出warning函数
    export default function warning(message) {
        // 判断console.error函数是否存在且可用
        if (typeof console !== 'undefined' && typeof console.error == 'function') {
            console.error(message);
        }

    }
  {% endhighlight %}
    
  2.捕获异常并处理
    
   {% highlight javascript %}
    try {
        // 抛出异常
        throw new Error(Message)
    } catch(e) {
        // 捕获异常
    }
    {% endhighlight %}

### redux从入门到进阶

#### **初学者**
> 学习步骤：1. 阅读redux的官方文档 2.通过一些小例子熟悉redux的思想 3.复杂案例应用 4.熟悉redux的源码 5.熟悉业界关于redux的最佳实践

1. [redux offical site](http://www.reduxjs.org)
2. [Redux系列01：从一个简单例子了解action、store、reducer](https://yq.aliyun.com/articles/36261?spm=5176.100240.searchblog.32.2LIXzh)
3. [Redux系列02：一个炒鸡简单的react+redux例子](https://yq.aliyun.com/articles/36265?spm=5176.100240.searchblog.21.lItKnE)



### **Pratice**
> 关于redux的实战经验 

1. [Redux 在实践中的一些问题及思考](https://undefinedblog.com/some-thoughts-in-redux/)
2. [React和Redux的连接react-redux](https://leozdgao.me/reacthe-reduxde-qiao-jie-react-redux/)
3. [对Redux实践中数据请求的一些想法](https://leozdgao.me/reduxshi-jian-zhong-de-xie-xiang-fa/)
4. [Redux系列x：源码解析](https://yq.aliyun.com/articles/36263?spm=5176.100240.searchblog.26.NAsBoE)




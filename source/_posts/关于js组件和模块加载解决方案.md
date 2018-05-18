---
title: 关于js组件模块加载解决方案
date: 2017-08-26 18:53:01
categories: 				# 文章分类
- js
tags: 						# 文章标签
- AMD CMD CommonJS
- 模块加载
---

> #### 1、**AMD**（Asynchromous Module Definition - 异步模块定义）

AMD是RequireJS在推广过程中对模块定义的规范化产出，AMD是异步加载模块，推崇依赖前置。
```
	define('module1', ['jquery'], ($) => {
	  //do something...
	});
```
> #### 2、**CMD**（Common Module Definition - 公共模块定义）

CMD是SeaJS在推广过程中对模块定义的规范化产出，对于模块的依赖，CMD是延迟执行，推崇依赖就近。
```
	define((require, exports, module) => {
		  module.exports = {
	    fun1: () => {
	       var $ = require('jquery');
	       return $('#test');
	    } 
	  };
	});
```	
* CommonJS：CommonJS是服务端模块的规范，由于Node.js被广泛认知。根据CommonJS规范，一个单独的文件就是一个模块。加载模块使用require方法，该方法读取一个文件并执行，最后返回文件内部的module.exports对象。CommonJS 加载模块是同步的，所以只有加载完成才能执行后面的操作。



> #### 3、**UMD**（Universal Module Definition - 通用模块定义）

UMD是AMD和CommonJS的一个糅合。AMD是浏览器优先，异步加载；CommonJS是服务器优先，同步加载。

既然要通用，怎么办呢？那就先判断是否支持node.js的模块，存在就使用node.js；再判断是否支持AMD（define是否存在），存在则使用AMD的方式加载。这就是所谓的UMD。

> #### 4、ES6 风格：

通过import--export对管理依赖模块，可以选择性加载单个变量、函数等。


## 关于模块管理工具：


Gulp / Grunt 是一种工具，能够优化前端工作流程。比如自动刷新页面、combo、压缩css、js、编译less等等。简单来说，就是使用Gulp/Grunt，然后配置你需要的插件，就可以把以前需要手工做的事情让它帮你做了。

browserify / webpack ，那还要说到 seajs / requirejs 。这四个都是JS模块化的方案。其中seajs / require 是一种类型，browserify / webpack 是另一种类型。

seajs / require : 是一种在线"编译" 模块的方案，相当于在页面上加载一个 CMD/AMD 解释器。这样浏览器就认识了 define、exports、module 这些东西。也就实现了模块化。
browserify / webpack : 是一个预编译模块的方案，相比于上面 ，这个方案更加智能。没用过browserify，这里以webpack为例。首先，它是预编译的，不需要在浏览器中加载解释器。另外，你在本地直接写JS，不管是 AMD / CMD / ES6 风格的模块化，它都能认识，并且编译成浏览器认识的JS。
这样就知道，Gulp是一个工具，而webpack等等是模块化方案。Gulp也可以配置seajs、requirejs甚至webpack的插件。

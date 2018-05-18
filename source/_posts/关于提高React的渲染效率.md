---
title: 关于提高React的渲染效率
date: 2017-11-26 22:47:37
categories:         # 文章分类
- js
tags:             # 文章标签
- React
- 渲染
- 性能优化
---

> react组件是如何渲染的？
> 怎样提高其渲染效率呢？

### 一、React的render机制：
react的组件的渲染分为初始化渲染（initial）和更新渲染（update）;
初始化渲染调用的过程：
- getDefaultProps
- getInitialState
- componentWillMount [渲染前最后可以改变state的地方]；
- render [构建虚拟Dom]
- componentDidMount [真实DOM构建完毕，可以操作组件的真实DOM，如绑定事件等]

组件在初始化的时候会调用根组件下的所有组件的render方法。
但是当我们要更新某个自组建的时候，我们的理想状态是只调用关键路径上组件的render函数。但是react的默认做法是调用所有组件的render，再对生成的虚拟DOM经行对比，如果不变则不进行更新，这样有些没有改变的组件的虚拟DOM的对比将是额外的开销。react会以变化的组件对比虚拟DOM（props和state变化），并且re-render该组件下的所有子组件，这就导致了组件没必要的重新渲染。

我们应该清楚：
- 拆分组件有利于复用和组件优化；
- 成成的虚拟DOM并进行Diff对比是发生在render()函数之后的，而非之前；


### 二、 shouldComponentUpdate()实现不必要的渲染；
在大量的数据的时候，有很多不必要的渲染，react团队给定制优化的生命周期钩子函数。
- componentWillReceiveProps(nextProps):当挂载的组件接收到新的props时被调用，父组件的状态改变（setState）怎样传递到自组件中？该函数在子组件中调用，比较this.props和nextProps然后再this.setState()执行子组件的状态变换，这样父组件的状态改变就更新到子组件了。
- shouldComponentUpdate(nextProps, nextState): boolean (返回布尔值，后面简单记为SCU)： 当组件决定任何状态改变时是否更新DOM，re-render以及后续操作，返回false时跳过重新渲染
- componentWillUpdate(nextProps, nextState)更新前调用，此时不能setSate()
- componentDidUpdate(prevProps, prevState): 更新后调用；

### 三、重新渲染的流程
+ 根据shouldComponentUpdate（SCU）函数的返回值决定是否要更新，默认返回true，
+ 如果要更新则调用组件的render方法生成新虚拟DOM；
+ 新的虚拟DOM与旧的虚拟DOM对比，根据Diff算法最小粒度的去改变更新真实DOM节点；
+ 如果SCU返回false则该组件以及子组件都保持不变

### 四、 提高react渲染效率的几个方案：
1. 给组件添加shouldComponentUpdate逻辑判断：
```js
shouldComponentUpdate(nextProps, nextState) {
	return nextProps.value !=== this.props.value
}

```
当然也可以使用facebook 开发react的孪生姐妹三方件immutable.js更方便地比较状态树；
2. 对于遍历组件，给组件添加唯一的key属性，提高Diff算法效率；
3. 不要乱用{...this.props}经行解构，只传递组件需要的props, 传得太多传得太深都会加重shouldComponentUpdate数据的比较的负担；
在用react-redux时，在容器组件上使用*connect([mapStateToProps(state, ownProps)], [mapDispatchToProps], [mergeProps],[options])*函数；
4. 将方法绑定置于constructor(props)函数中，如果直接在render函数中绑定，每次调用都会执行bind函数创建一个新的函数。
等等。。。【未完待续】
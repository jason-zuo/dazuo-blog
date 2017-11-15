---
title: react-touch-loader组件学习
date: 2017-11-15 16:09:58
tags: [ react, 组件学习 ]
author:
  nick: 大左
subtitle: 针对项目中的需求对react-touch-loader进行学习，以及简单的封装...
cover: 

---

#### react touch loader学习


###### 由于移动端项目中有下拉滚动加载更多，所以需要对该npm包进行简单的再封装，再次记录下来，作为学习记录
该npm包下载地址 : https://github.com/Broltes/react-touch-loader


感谢该组件的作者封装出来这么好用的组件，膜拜


---

一、首先定义一个STAS对象，在该对象中定义了几种加载状态

init | ''          (为空)
---|---
pulling | pulling  (下拉)
enough | pulling enough (下拉到一定程度)
refreshing | refreshing (恢复中)
refreshed | refreshed (回复之前)
reset | reset  (复位)
loading | loading  (加载)

之后定义了一个Tloader类并且定义了

1、loaderState:STATS.init

2、pullHeight : 0 

3、progressed ： 0   ( 头部加载条的进度 )

几种初始状态

---

在componentWillReceiveProps的生命周期中
定义了如果
```
nextprops.initializing < 2
```
 的话设置progessed的状态为0
> 注释为reset progress animation state( 重置进度动画状态 )


---
render函数中定义了

```
const { className, hasMore, initializing } = this.props;
```

上级传过来的class名字、以及是否还有更多、头部进度条的状态


```
 const { loaderState, pullHeight, progressed } = this.state;
```
当前组件的状态

一个footer的组件定义的是如果还有更多则渲染一个底部加载动画，加载的div上绑定了一个点击事件
```
onClick = { e => this.loadMore(e)}
```
如此引出loadMore事件


```
loadMore() {
    this.setState({ loaderState: STATS.loading });
    this.props.onLoadMore(() => {
      // resolve
      this.setState({ loaderState: STATS.init });
    });
  }
```

该事件将默认的loaderState定义为loading状态，并且引用了引用该Tloader方法的上层组件方法onLoadMore如果resolve说明加载完成并将loaderState设置为默认空


---

并且所渲染的dom绑定了三个事件分别为onScroll、touchStart、touchMove、touchEnd第一个事件对应实现滚动移动距离之后加载更多，剩下三个事件对应下拉回弹并且刷新当前页面。


---

### 项目中遇到的问题

1、由于滚动条加在了最外层的div上所以，无法给Tloader加scroll的监听事件

2、如何在现在基础上封装出新的需求代码


（下拉到一定程度之后自动加载数据，**可以根据滑动速度加载更多）

---
### 解决方法
组件滚动条要加tloader组件上



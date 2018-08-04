学习 React 的第一篇笔记

拜读了 阮老师的 [React 入门实例教程](http://www.ruanyifeng.com/blog/2015/03/react.html)

接着读了一遍[菜鸟教程](http://www.runoob.com/react/react-tutorial.html)上的 React 教程

将笔记整理了下

也有些与 Vue 的对比

2018年4月

#### 1.ReactDOM.render()

这个可以说就像 外加载 vue 中的 new Vue({ }) 一样重要了;

第一个参数是模板，第二个参数是要插入的节点对象

最简单的 React 程序

```
ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
```



#### 2.JSX语法 

可以把html和js混写 

遇见<就开始当html标签处理，js的可以放{}里面



#### 3.使用注意

就像上面的 h1 里面 如果写入 {} 里面放个数组的时候

react 会自动展开，（不管你是标签组成的数组还是字符串数组）

效果有点像 vue 的 v-for



#### 4.React.createClass 

可以生产一个组件，但是 es6 现在都流行这么写了：

```
import React, { Component } from 'react';
class App extends Component{
    render(){
        return
    }
}
```



#### 5.prop

 可以实现父子通讯，而且可以传递函数等

this.props是调用组件时候传进来的，但this.props.children是表示组件所有子节点

`React.Children.map` 来遍历子节点

（ 很好理解， Vue 也可以添加 prop 向子组件传值）



#### 6.propTypes 

prop内容较多但好理解，有点模糊了就翻

[React Props --菜鸟教程](http://www.runoob.com/react/react-props.html)

用来检验传入的值是否合格，不合格会报错（和render写在同一层级）



#### 7.getDefaultProps

```
getDefaultProps : function () {
return {      
	title : 'Hello World'    
	};  
},
```

用来指定默认值 （也r在同一层级）



#### 8.ref

> 组件并不是真实的 DOM 节点，而是存在于内存之中的一种数据结构，叫做虚拟 DOM （virtual DOM）。。只有当它插入文档以后，才会变成真实的 DOM 。根据 React 的设计，所有的 DOM 变动，都先在虚拟 DOM 上发生，然后再将实际发生变动的部分，反映在真实 DOM上，这种算法叫做 [DOM diff](http://calendar.perfplanet.com/2013/diff/)，它可以极大提高网页的性能表现。

所以需要获取元素需要添加 ref  然后 `this.refs.[refName]` 

可以使用原生 DOM 的API

vue 那个 ref 也很像的



#### 9.getInitialState 

由名字读出来就是初始的时候

可以定义些状态的函数

```
 getInitialState: function() {
    return {liked: false};
  },
```

通过 this.state 读取  this.setState() 设置



> 由于 `this.props` 和 `this.state` 都用于描述组件的特性，可能会产生混淆。一个简单的区分方法是，`this.props` 表示那些一旦定义，就不再改变的特性，而 `this.state` 是会随着用户互动而产生变化的特性。



#### 10.注意点 标签写属性的时候

```
style={{opacity: this.state.opacity}}
```

因为 [React 组件样式](https://facebook.github.io/react/tips/inline-styles.html)是一个对象，所以第一重大括号表示这是 JavaScript 语法，第二重大括号表示样式对象。



#### 11.生命周期

暂时感觉状态比 vue 的少好多 ， 也许是还没深入吧



- Mounting：已插入真实 DOM
- Updating：正在被重新渲染
- Unmounting：已移出真实 DOM
  - componentWillMount()
  - componentDidMount()
  - componentWillUpdate(object nextProps, object nextState)
  - componentDidUpdate(object prevProps, object prevState)
  - componentWillUnmount()


- componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
- shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用

#### 12.ajax

获取数据就可以在didmount里面弄，弄了setState进去



## 4月2日

##### 1.无状态的，不需要生命周期的组件可以这样写

```
const BasicExample = () => (
	<div></div>
)
```



## 4月3日

#### 正确地使用状态

关于 `setState()` 这里有三件事情需要知道

##### 1.不要直接更新状态 应当使用 `setState({user: 'boen'})`:

##### 2.状态更新可能是异步的 React 

   可以将多个`setState()` 调用合并成一个调用来提高性能。

因为 `this.props` 和 `this.state` 可能是异步更新的，你不应该依靠它们的值来计算下一个状态。

请使用第二种形式的 `setState()` 来接受一个函数而不是一个对象。 该函数将接收先前的状态作为第一个参数，将此次更新被应用时的props做为第二个参数：

```
// Correct
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));

```

##### 3.状态更新合并

setState() 是浅合并 之前的都在
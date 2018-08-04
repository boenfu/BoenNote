----图书馆的书 React开发实战



1.html写在组件的 render函数里

2.state定义在constructor里

3.props传给子组件时 直接写在子组件标签上

4.onClick这类绑定函数时需要bind(this)把this传进去

5.onClick这类并不是原始事件 只是做的很像

6.行内不能if 但是可以三元运算符

7.注释就是js的注释 但是要写在标签里时 要用{}

8.使用表单 input 绑在value上 要改变 onChange

9.textarea 也是value ，select 标签 value设什么 选中的就是对应的value的option

10.只是设初始值用 defaultValue

11.45页虚拟dom的处理方法介绍

12.指定key可以避免渲染瓶颈 方便react工作的

13. ref 类里用this.refs 访问真实dom

    2018年5月16日20:33:20







14.在组件类定义外设置属性 .propTypes 设置prop的类型，设置默认值 defaultProps 要是用ts就不需要这两个了

15.自定义propTypes 验证器 可用参数有 props propName 和组件名

16.有状态的组件能少就少

17.子组件调用 this.props.回调函数名 与父组件通讯

18. 生命周期

    ​	加载

    ​	constructor -> componentWillMount -> render -> componentDidMount

    ​	卸载

    ​	componentWillUnmount

    ​	props更改

    ​	componentWillReceiveProps -> shouldComponentUpdate ->componentWillUpdate 

    ​	-> render -> compoentDidUpdate

    ​	state 更改

    ​	shouldComponentUpdate ->componentWillUpdate -> render -> compoentDidUpdate

19. 获取数据最佳在componentDidMount 另外 可以创建一个容器组件来取值用props传递

20. React提供了不变性助手 --就是用来解决Object.assign浅复制影响React的问题

    2018年5月17日09:51:39

    ​

    ​

    ​

    #### 第四章 复杂交互

21. react 组件过度效果

    ​

    react-addons-css-transition-group

    定义各阶段css 类名

    ```
    import Rctg from 'react-addons-css-transition-group'
    <Rctg transitionName="example" 
              transitionAppear={true} //初始化是加载额外过渡效果 默认关闭
              transitionAppearTimeout={4000}
              transitionEnterTimeout={2000}
              transitionLeaveTimeout={2000}>
                {lists}
              </Rctg>
    // css
    .example-enter{
      opacity: 0;
      background-color: #009960;
    }
    .example-appear{
      opacity: 0;
      background-color: #db366d;
    }
    .example-enter.example-enter-active,
    .example-leave{
      opacity: 1;
      background-color: #fff;
      transition: all 2s;
    }
    .example-appear.example-appear-active{
      opacity: 1;
      background-color: #fff;
      transition: all 4s;
    }
    .example-leave.example-leave-active{
      opacity: 1;
      background-color: #f7da37c2;
    }
              
    ```

    ​



dnd

拖拽 见代码注释



#### 第五六章为 路由与flux 

​	路由参考代码

​	flux 简略跳过 看redux了

![](https://img.mukewang.com/5aee7f43000140ad12800720.jpg)



#### 第七章

子级校正

​	setState后不是立即生效 而是 标记为 ‘脏’ 数据 轮询结束后 一齐重绘

​		有一个 shouldComponentUpdate 的生命周期	 

​		默认返回的 true 重写并返回 false 就能跳过该组件及子组件重绘

React Perf 

​	分析工具 可以对应用整体性能进行概要分析（了解一下就行）



2018年5月19日14:10:28

#### 第八章

同构（服务端渲染？）
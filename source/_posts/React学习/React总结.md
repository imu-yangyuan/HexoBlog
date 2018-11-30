---
title: React总结
date: 2018-11-08 11:44:59
tags: react
---
#### React特点：

- 虚拟dom
    - 简单的UI开发逻辑
    - 组件化
 - 一个组件应该具有的特征：
    - 可组合
    - 可重用
    - 可维护
#### Jsx语法：在html中直接写Js代码，不加任何引号，允许html和js混写

- 组件的生命周期：
    - Mounting：已插入真实 DOM
    - Updating：正在被重新渲染
    - Unmounting：已移出真实 DOM

 和组件生命周期相关的几个方法：
```
getDefaultProps //创建组建
getInitialState  //实例化状态
componentWillMount  //挂载前
componentDidMount //挂载后
componentWillReceiveProps //属性被改变时
shouldComponentUpdate //是否更新
componentWillUpdate //更新前
componentDidUpdate //更新后
componentWillUnmount //销毁前
```

- 1、ReactJs是基于组件化的开发，所以最终的页面应该是由若干个小组件组成的大组件。
- 2、可以通过属性，将值传递到组件内部，同理也可以通过属性将内部的结果传递到父级组件(留给大家研究)；要对某些值的变化做DOM操作的，要把这些值放到state中。
- 3、为组件添加外部`css`样式时，类名应该写成`className`而不是`class`;
`for`是`htmlFor`，添加内部样式时，应该是style=&#123;&#123;opacity: this.state.opacity&#125;&#125;
而不是```style="opacity:{this.state.opacity};"```。
- 4、组件名称首字母必须大写。
- 5、变量名用`{}`包裹，且不能加双引号。
#### ReactJS优缺点：
- 优点：
    - React速度很快
    - 浏览器兼容 兼容到IE8
    - 模块化（1、 模块化组件 2、 对于每个组件方便独立进行开发和测试，提高了代码可维护性）
    - 单向数据流
- 缺点：
    - React只是MVC中V，并不是一个完整的框架
#### React创建组件：

- 1.创建组件两种方式：
    - 无状态组件
    - 类组件（ES6的class）
- 2.原则：遵守单一职责的原则
- 3.一个类组件包含：
    - 属性：`props`
    - 内部状态
    - 处理逻辑
    - 事件处理
    - 渲染：`render`
    - 生命周期函数
- 4.组件创建技巧
    - 尽可能无状态化
    - 减少冗余
    - 创建多个只负责渲染数据的无状态组件，在他们的上层创建一个有状态的组件并把状态通过props传递给子级
    - 有状态组件封装了所有用户的交互逻辑，无状态组件只负责声明式渲染



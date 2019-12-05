---
title: React 生命周期
date: 2018-08-30
author: ChenEnjun
category: React
tags:
- React
---

# React 生命周期
### 公式抽象
> #### **UI=render(data)**
1. 用户看到片的界面（UI），应该是一个纯函数（render）的执行结果,只接受数据（data）作为参数。
2. 存函数的输出完全依赖于输入的函数，两次函数条用如果输入相同，得到的结果也绝对相同。
<!--more--> 
## prop
> prop为property的简写，意为属性
1. prop是组件的对外接口，state是组件的内部状态，对外用prop，内部用state。
1. 一个React组件通过定义自己能够接受的prop就定义了自己的对外公共接口。
1. 每个React组件都是独自存在的模块，组件之外的一切都是外部世界，外部世界就是通过prop来和组件对话。

```
<SampleButton id="sample" borderWidth={2} onClick={onButtonClick} style={{color:"red"}} />
```
1. HTML组件的属性都是字符串类型，而React组件的prop能支持任何一种js语言数据类型，比如数字，函数，对象。
2. 当prop的类型不是字符串类型的时候在JSX中必须用花括号{}把prop值包住。
3. 父组件可以通过prop给子组件传递数据，同样子组件也可以通过prop给父组件**反馈数据**，因为prop不限制存数据，也可以是函数，函数类型的prop等于让父组件交给了子组件一个**回调函数**，子组件调用此prop的时候，可以带上必要的参数，这样就可以反馈数据给父组件。
```
constructor(props) {
    super(props);
    this.state = {
        count: props.initValue || 0
    }
}
```
4. propTypes 、defaultProps ( prop-types v16.0, babel-react-optimize 线上环境)
```
// propTypes
import PropTypes from 'prop-types';

、
SampleButton.propTypes = {
    id: PropTypes.string.isRequired,
    borderWidth: PropTypes.number
}

SampleButton.defaultProps={
    borderWidth: 0
}
例子
```

## prop和state的对比
- [ ] prop用于定义外部接口，state用于记录内部状态；
- [ ] prop的赋值再外部世界实用组件时，state的赋值再组件内部；
- [ ] 组件不应该改变prop的值，而state存在的目的就是让组件来改变的；

## 组件的生命周期
#### 装载过程
当组件第一次被渲染的时候，一次调用这些函数。
##### constructor
组件自己的构造函数，可用于初始化state，绑定this环境等

##### getInitialState & getDefaultProps
只有React.createClass创造的组件会有，用于初始化state和给props初始值

##### componentWillMount
在调用render函数之前调用，这里的所有事情都可以提前到constructor中做
##### render
一个React组件可以忽略其他所有函数都不实现，但是一定要实现render函数，因为所有React组件的父类React.Component类对其他生命周期函数都有默认实现。
- [ ] render 函数并不做实际的渲染动作，它只是返回一个JSX描述的结果，最终由React 来操作渲染过程。
##### componentDidMount
在调用render函数之后调用，注意点：
- [ ] render函数调用完后，**不会立刻调用**componentDidMount，它的触发点在render已经**引发了渲染**，组件已经被装载到DOM数上后。
- 例子
- [ ] 不同于componentWillMount可以在服务器和浏览器端被调用，componentDidMount**只能在浏览器端**被调用。这点在同构的时候会用到，同时也提供给开发者一个很好的位置去做只有浏览器才做的逻辑，比如通过ALAX获取数据用来填充组件内容。
- [ ] 有时候React需要和其他UI库配合使用，比如jQuery,比如d3.js等，因为DOM已经存在，事件函数已设置好，所以可以在这一步进行调用。
#### 更新过程
##### componentWillReceiveProps
- [ ] 只要是父组件的render函数被调用，不管传递的porps有没有改变，都会触发子组件的componentWillReceiveProps。
- [ ] 注意子组件内部的this.setState方法不会触发这个函数，因为这个函数是根据新的props（也就是参数nextProps）来计算是不是要更新state。
- 例子

##### shouldComponentUpdata（nextProps,nextState）
- [ ] 此函数决定了一个组件什么时候**不需要渲染**，shouldComponentUpdata返回一个布尔值，告诉React库这个组件在这次更新中是否要继续。
- [ ] 恰当的使用shouldComponentUpdata能够大大提高React组件的**性能**。
- [ ] 如果不写，会继承React.Component中的默认实现方式，也就是简单的返回true。
- 例子
扩展：React.PureComponent
React.PureComponent通过浅的prop和状态比较来实现shouldComponentUpdate()
- [ ] 在将来，React会将shouldComponentUpdate()视为提示而不是严格的指令，并且返回false仍然可能导致组件的重新呈现。
##### componentWillUpdate
##### render
##### componentDidUpdate
- [ ] 如果组件的shouldComponentUpdata返回true，接下来就会依次调用这三个函数。
- [ ] 与装载不同的是，这一对函数的Did函数（componentDidUpdate）并不是只在浏览器端执行。
- [ ] 在React组件更新时，原有内容被重制，所以用到的UI库（比如jQuery）需要在componentDidUpdate后再次调用jQuery代码。

#### 卸载过程
##### componentWillUnmount
当React组件需要从DOM树上删掉之前，对应的componentWillUnmount函数会被调用，移除多余的DOM元素，避免内存泄漏。

### React v16.3新生命周期

开启异步渲染
新引入的两个生命周期函数 getDerivedStateFromProps，getSnapshotBeforeUpdate 以及在未来 v17.0 版本中即将被移除的三个生命周期函数 componentWillMount，componentWillReceiveProps，componentWillUpdate .
#### 装载
- [ ] constructor()
- [ ] static getDerivedStateFromProps()
- [ ] render()
- [ ] componentDidMount()
- [ ] 移除 componentWillMount()
#### 更新
- [ ] static getDerivedStateFromProps()
- [ ] shouldComponentUpdate()
- [ ] render()
- [ ] getSnapshotBeforeUpdate()
- [ ] componentDidUpdate()
- [ ] 移除 componentWillUpdate() componentWillReceiveProps()
##### getDerivedStateFromProps(nextProps, prevState)
getDerivedStateFromProps在调用render方法之前调用，无论是在初始安装还是后续更新。它应该返回一个更新状态的对象，或者返回null以不更新任何状态。

##### getSnapshotBeforeUpdate(prevProps, prevState)
getSnapshotBeforeUpdate()在最近呈现的输出被提交到例如DOM之前调用。它使您的组件可以在可能更改之前从DOM捕获一些信息（例如滚动位置）。此生命周期返回的任何值都将作为参数传递给componentDidUpdate()。
```
可能出现在需要以特殊方式处理滚动位置的聊天线程等UI中。比如jtalk

class ScrollingList extends React.Component {
  constructor(props) {
    super(props);
    this.listRef = React.createRef();
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // 我们是否在列表中添加新项目?
    // 捕获滚动位置，以便我们稍后调整滚动.
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // 如果snapshot有返回值，我们就是添加了新项目.
    // 调整滚动，以便这些新项目不会将旧项目推出视图.
    // (这里的snapshot是从getSnapshotBeforeUpdate中返回的值)
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  render() {
    return (
      <div ref={this.listRef}>{/* ...contents... */}</div>
    );
  }
}
```
在上面的例子中，重要的是读取scrollHeight属性，getSnapshotBeforeUpdate因为“渲染”阶段生命周期（如render）和“提交”阶段生命周期（如getSnapshotBeforeUpdate和componentDidUpdate）之间可能存在延迟。

#### 错误处理
##### componentDidCatch(error, info)
错误边界是React组件，**它们在其子组件树中的任何位置捕获JavaScript错误，记录这些错误，并显示回退UI**而不是崩溃的组件树。错误边界在渲染期间，生命周期方法以及它们下面的整个树的构造函数中捕获错误。

```
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  componentDidCatch(error, info) {
    // Display fallback UI
    this.setState({ hasError: true });
    // You can also log the error to an error reporting service
    logErrorToMyService(error, info);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}
```

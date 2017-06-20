不用 Redux 如何实现组件间通信呢？

答案简单来说就一句话：

> 通过子组件，修改父组件的 state ，然后把父组件的 state 作为所有子组件的 props 值传入各个子组件

这样就实现了各个兄弟组件间通信。

```js
import React from 'react'

class Child extends React.Component {
  render() {
    return(
      <button onClick={() => this.props.changeParentState('yellow')}>Child Button</button>
    )
  }
}

class App extends React.Component {
  constructor() {
    super()
    this.changeBgc = this.changeBgc.bind(this)
  }

  state = {
    color: 'red'
  }

  changeBgc(color) {
    this.setState({
      color: color
    })
  }
  render() {
    return(
      <div style={{'color': this.state.color}}>
        <div>App</div>
        <Child  changeParentState={this.changeBgc} />
      </div>
    )
  }
}

export default App
```


### redux-hello 项目中

实现评论效果：

- [go without redux](https://github.com/happypeter/redux-hello/commit/f9ab32451cfba2e0e6c5f25dead99dcb5214d932)


### 参考资料

- [You May Not Need Redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)

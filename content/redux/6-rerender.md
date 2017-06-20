先给出结论，下面再具体写小例子验证。

> 组件的 **state** 和 **props** 变化都会触发 render() 函数的再次执行。


### 验证一下

state 变化，render() 重新被执行，这个是很明显的，不验证了。下面验证一下 props 。

任务：写一个组件，点一下按钮，就能够改变它的子组件的 prop ，同时展示一下此刻子组件的 render 函数有没有被再次执行。这个任务的目的是要验证一个观点：

> 组件的 props 变化，会导致组件重新 render 。

官方文档在[这里](https://facebook.github.io/react/docs/react-component.html#updating)

>An update can be caused by changes to props or state.

### 案例1

App.js

```
import React, { Component } from 'react';
import Son from './Son';

class App extends Component {
  constructor() {
    super();
    this.state = {
      data: 1
    }
  }
  handleClick(e){
    e.preventDefault();
    this.setState({
      data: this.state.data + 1
    })
  }
  render(){
    return(
      <div>
        <Son num={this.state.data} />
        <button onClick={this.handleClick.bind(this)}>Click</button>
      </div>
    )
  }
}

export default App;
```

Son.js

```js
import React, { Component } from 'react';
import store from '../store';


class Son extends Component {
  render(){
    console.log('Son rendering....')
    return(
      <h1 >
          { this.props.num }
      </h1>
    )
  }
}

export default Son;
```

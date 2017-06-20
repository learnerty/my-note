这一集不涉及 Redux ，我们只是使用每个组件自己的 State 来达成基本评论框效果。

要求：不需要使用后台。直接把假数据设置到 state 变量里面。

### 任务一： 显示两条死的评论在页面上。

这里的体现出 React 的特点，就是所有的组件显示出来的动态数据，都要存放到 state 值之中。

但是数据到底要存储成何种数据类型呢？也即是数据的存储格式要怎么样？

```
this.state = {
  comment1: "hello1",
  comment2: "hello2"，
}
```

这样写，如果只是展示两条死数据，完全没有问题。但是如果有一百条评论，就得有一百个 state 值。但是 React 组件其实一旦写成，它里面的 state 变量名的数量是固定的。代码运行过程中，一般不能添加新的 state 变量进来。只能修改已有的 state 变量值。

数据结构的采用，完全根据实际需要来选择。首先要设置一个 state 变量，就叫 comments 。
同时这个变量里面，可以有多个元素，可以任意增加或者减少元素数量。

```
this.state = {
  comments: [
    "hello1",
    "hello2"
  ]
}
```

代码： [two comments](https://github.com/happypeter/redux-hello/commit/20db7800a8d08cf3c9f0bc40f3dfc35277c795a2)

注意：用数组的 Index 值做 key 是非常不好的习惯，一般用每条数据的 id 来做即可。

### 任务二：添加 form

代码： [form styling](https://github.com/happypeter/redux-hello/commit/af4a6c86e81e00a59088226e67774702206ba225)


### 任务三：发布评论

发布评论的过程：

- 点一下 submit 这个按钮，浏览器发成的 event （事件）就是 “表单提交（ form submit ）”
- 事件触发之后，我们如何来写对应的”事件处理函数“一般会叫 handleXXX ，意思是”处理XXX事件“
- 如何把”事件处理函数“跟事件本身绑定起来呢？纯 html 中用 action 属性来处理。但是有了 React 就不用 action 。用 onSubmit （ on 的意思就是”当发生“ ) 。参考 [官方文档](https://facebook.github.io/react/docs/forms.html)

```
  <form onSubmit={this.handleSubmit}
```

- 现在的问题是，每次提交，页面都会刷新，而我们写的是”单页面应用“，所以页面不允许刷新

```
e.preventDefault()
```

- 下一步就需要拿到用户填写的评论内容了，这个我们就不用 [refs](https://facebook.github.io/react/docs/refs-and-the-dom.html) 了。而[改用箭头函数](https://zhenyong.github.io/react/docs/more-about-refs.html)。

```
<input ref={(value) => { this.textInput = value} }
```

- 现在，报错如下：

```
'textInput' of null
```

意思是在 handleSubmit() 中 this 的值是 null （空）。

- 这个的绑定形式是

```
constructor() {
  super()
  this.handleSubmit = this.handleSubmit.bind(this)
}
```


代码:

- 老的 refs 方式已经过时：[submit comment](https://github.com/happypeter/redux-hello/commit/23b7e9aa518f596e961c72362638b019e9d7d441)

- [with spread and new refs](https://github.com/happypeter/redux-hello/commit/599262380567ad201d2c7318dcd3196accc2f02c)


注意，不能直接使用下面的代码：

```js
handleSubmit(e) {
  e.preventDefault()
  let content = this.refs.content.value
  let comments =   this.state.comments // 需要添加 .slice()
  comments.push(content)
  this.setState({ comments })
}
```

因为这样会直接修改 state 值。可行的方式是用 slice() 或者用数组展开运算符。


参考：

- [为何不能直接修改 State](https://facebook.github.io/react/tutorial/tutorial.html#why-immutability-is-important)

- [中文](https://beijiyang.github.io/react-tutorial-translation/chapter3/content2.html)

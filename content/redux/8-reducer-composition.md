这一节来看看 redux 如何处理多类数据。

### 添加点赞功能

目前 PostBody 组件中只显示评论，现在我们在添加一个点赞的按钮进来。

- [add like button](https://github.com/happypeter/redux-hello/commit/e77624e16b89a08bb4d0783d7fb1d5122913b37f)

### 显示“0赞”

这个就要来修改一下 store 中的数据初始值的内容了

```
comments = ['hello1', 'hello2']
```

要改为

```
defaultState = {
  comments: ['hello1', 'hello2'],
  likes: 0
}
```

对应的 reducer 的命名也要改一下了。

```
commentReducer => rootReducer
```

- [state tree with more data](https://github.com/happypeter/redux-hello/commit/79c5e8c367f40262dc2a1335ba21ecbfa780a639)

有了上面的代码，读取 store 中的 defaultState 没有问题了，但是 reducer 本身却失效了。


### 修改 reducer 的 ADD_COMMENTS 部分


从 [中文官方文档的 reducer 部分](不要修改 state) 可以看到

>不要修改 state

意思是，reducer 函数中，只能修改 state 的拷贝，state 本身不能变。


这里涉及到你先要对 defaultState 做一个拷贝再改，如果是数组的拷贝通常用 slice() 还有 ...spread 。我们这里 defaultState 是一个对象，用 Object.assign 还有 ...spread 。

- [add comments works](https://github.com/happypeter/redux-hello/commit/f4c5fd6a60cb3fde7bd58bcf6248e8ea851b6b82) 这里采用的是”对象展开运算符“的方式。

- [INCREMENT_LIKES](https://github.com/happypeter/redux-hello/commit/730893d5ff90f698a9b33919cbf306c403656066)

参考文档： [redux 中文](http://cn.redux.js.org/docs/recipes/UsingObjectSpreadOperator.html)

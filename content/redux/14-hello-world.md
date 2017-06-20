现在来给出一个 redux-thunk 的极简案例，就显示一个评论数。最终代码在：https://github.com/happypeter/thunk-hello

### 搭建一个 react hello world 程序

```
create-react-app thunk-hello
```

删除一些不用的文件和代码，

- 代码： **react hello world**


### 页面显示“0 评论”

现在走 redux 的全套思想，让页面上显示一个 store 中存储的初始值 0 。

首先要安包：

```
npm i --save redux
```

然后创建 store.js/commentReducer

代码：**read 0 from store**

### 使用 react-redux 动态订阅 store 数据

先装包：

```
npm install --save react-redux
```

- 代码：**connect with react-redux**

### 后台 API

```
curl http://redux-hello.haoduoshipin.com/comments
```

curl 是最常用的 API 测试工具。上面的命令的输出是一系列的服务器端提供的评论。

```
{"msg":"获取评论成功","comments":[{"_id":"58f605d217deb3614c290704","commentBody":"hi","postId":"1","__v":0},{"_id":"58f605da17deb3614c290705","commentBody":"hi again","postId":"1","__v":0},{"_id":"58f605f317deb3614c290706","commentBody":"hello baby","postId":"2","__v":0}]}%
```

### 使用 Redux 加载初始化数据的一个流程

我们先抛开 thunk ，只要我用 redux ，那么事情的起点就是：浏览器的一个事件。事件触发 dispatch(action) 。

所以用了 thunk 之后，思路也是相同的。就是在页面加载这个事件中触发 dispatch 操作。具体来说就是，在 componentWillMount() 中，去呼叫 Action Creator ，然后，Action Creator 中首先发起网络请求，请求拿到数据之后，去 dispatch 。接下来触发 reducer ，修改 state ... 这些都和 redux 的普通思路相符了。

### 发起 API 请求

代码：

- **thunk works**


### 备注

如果不用 thunk ，直接在 componentWillMount() 中写成这样：

```
componentWillMount() {
  axios.get('http://api.example.com/api').then(res => {
    this.props.dispatch({ type: xxx, comments: res.data.comments })
    })
}
```

达成的效果是跟使用 thunk 一样的。但是如果 action 复杂了，不把数据整理代码移动到 action creator 里面，都写入 componentWillMount ，代码就会比较乱。


### 结语

到这里，我们的 redux-thunk 的 hello world 就写完了。

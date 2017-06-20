本节把整个应用做的完善一些：

- 添加 React-Router 进来，让首页显示多篇文章
- 每篇文章拥有自己的点赞和评论

### 添加 React-Router

区分出两个页面来。

- [two pages](https://github.com/happypeter/redux-hello/commit/99da8c6b5289dfde5d165316a6c8ffc7cb0dea20)

### 添加另一组评论，每篇 post 显示自己的评论

- [show comments for each post](https://github.com/happypeter/redux-hello/commit/bb38c8dda47bc0c779438f6a8b94251e729289f4)

- [fix PostBody](https://github.com/happypeter/redux-hello/commit/d1e8167cd8170886b5524c6ff962b6e0674226c4)

### 点赞功能

重新规划一下数据，把点赞功能也实现了

- [INCREMENT_LIKES for each post](https://github.com/happypeter/redux-hello/commit/20a6ca3e15346523e461dfeab93fcccfca7bae96)

### 首页

添加首页

- [Home](https://github.com/happypeter/redux-hello/commit/d6e687649f46e151240775d0e21347bc3b7d7714)

- [rm warning](https://github.com/happypeter/redux-hello/commit/8edd0d470ad73e4b4d86f48519428a9a6385da13)



### 总结

目前 redux 的知识，除了做 ajax 请求需要的 redux-thunk 之外，基本都讲完了。redux-thunk 咱们下下节再讲。下面我们做一个 todo 的作业，来巩固一下前面的知识。

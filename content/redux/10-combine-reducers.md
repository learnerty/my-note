如果我们整个项目只用一个 reducer ，随着状态树变大，reducer 就会变得很复杂。那么如何进行 reducer 的拆分呢？这就涉及到 rootReducer/combineReducers 这些技巧了。


拆分后，要达成两个目标：

- 每个 reducer 负责一类数据，所以每个 reducer 都不会很大
- 每个 reducer 修改的 state 值，都**不是**整个状态树


### 创建 reducers/index.js 文件

创建一下 redux/reducers/index.js 文件，把 reducer 的代码拷贝进去。

- [create reducers](https://github.com/happypeter/redux-hello/commit/637492a945ae6827df8d2f66e041e73976fe28d8)

### 拆出两个 reducer

每个 reducer 的 state 默认值都只是自己对应的那一部分数据。

- [combineReducers](https://github.com/happypeter/redux-hello/commit/b77874d7e3364cd3e2db0ae0857086584f0ac9a3)

注意： combine 的意思是“合并”

```
const rootReducer = combineReducers({
  comments: commentReducer,
  likes: likeReducer
})
```

上面的参数中，`comments` 是需要被更新的 state ，commentReducer 是负责更新它的 reducer ，同理 likes 和 likeReducer 也是这样的关系。最终的整个 App 的状态树，就是

```
{
  comments,
  likes
}
```

后续在各个组件的 mapStateToProps(state) 函数中的 state 就是上面的这个值。


### 参考资料

- [官方的 combineReducers()文档](http://cn.redux.js.org/docs/recipes/reducers/UsingCombineReducers.html)
提出了很多值得注意的点，还是应该看一下的。

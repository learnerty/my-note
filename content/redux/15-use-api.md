# redux-hello 项目联通后台 API


这节来把 redux 代码中的前台假数据都删除，然后从后台 [API](http://redux-hello.haoduoshipin.com/comments) 中把评论读取并显示到前台。

### load comments 读取所有评论

从后台 API 读取评论

- 代码： [load comments](https://github.com/happypeter/redux-hello/commit/eb9ad97fe3ec59cf523116069e6dfaaa34588a59)

其中一个任务就是数据的整理：

要把服务器返回的

```
{"_id":"58d88a4d6281635fbed182bd","postId":"1","commentBody":"hello1","__v":0},{"_id":"58d88b8b17deb3614c29065f","postId":"2","commentBody":"hello2","__v":0}
```

整理成下面的格式：

```
let comments = {
  1: ['nice course', 'help me a lot'],
  2: ['really good', 'save me lots of time']
}
```


解决方案如下：

```
let cc = [
  { _id: '58d88a4d6281635fbed182bd',
    postId: '1',
    commentBody: 'hello1',
    __v: 0 },
  { _id: '58d88b8b17deb3614c29065f',
    postId: '2',
    commentBody: 'hello2',
    __v: 0 },
  { _id: '98d88a4d6281635fbed182bd',
    postId: '1',
    commentBody: 'hello11',
    __v: 0 },
  { _id: '58d8bf1317deb3614c290660',
    postId: '2',
    commentBody: 'hello22',
    __v: 0 }
]

let post1Com  = cc.filter(value => value.postId != '2' ).map(item => {
  return item.commentBody;
})

let post2Com = cc.filter(value => value.postId != '1' ).map(item => {
  return item.commentBody;
});
console.log(post1Com, post2Com);
// [ 'hello1', 'hello11' ] [ 'hello2', 'hello22' ]
```


### 提交评论

写代码之前，先拿 curl 测一下 API 是否还活着：

```
curl -X POST -H 'Content-Type: application/json' -d '{"postId": "2", "commentBody": "curl-test-xxx"}' http://redux-hello.haoduoshipin.com/comment
{"msg":"添加成功","comment":{"__v":0,"postId":"2","commentBody":"curl-test-xxx","_id":"593112e817deb3614c29070e"}}%
```

测试无误之后，开始写代码。

- [ADD_COMMENT](https://github.com/happypeter/redux-hello/commit/3635b5bf767e9235134f0ba8ec77554d207d04f6)

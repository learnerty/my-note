### 全局安装express
`npm install -g express-generator`
### 创建express项目
`express -e 项目名`
### 安装实时监听
`npm i -g supervisor`
### 开启监听
`supervisor bin/www`

### 安装express
项目文件夹的名称不能和包名相同
`npm install --save express`

### 创建一个index.js文件
```js
const express =  require('express')   //导入express
const app = express()

app.listen(3000 ,() => console.log('running on port 3000...'))   //启动一个3000端口服务器,成功打印run...
```
#### 在app.listen上写
```js
app.get('/', function(req, res){    //get请求，访问http://localhost:3000/  后端向前端浏览器返回字符串，req是请求，res是响应
  res.send('Hello World');
})
```
### 安装nodemon
能够持续监听，如果后台发生变化，会自动重启，启动命令`nodemon 文件名`   
`npm install -g nodemon`

## Express 操作 MongoDB
### 安装 Mongoose 包
通过 mongoose npm 包，让 Express 应用和 MongoDB 建立连接   
`npm install --save mongoose`
### 导入mongoose
`const mongoose = require('mongoose')`
### 链接MongoDB
localhost:27017是mongodb启动时默认的端口号，express-kiss-api是项目数据库的名称`mongoose.connect('mongodb://localhost:27017/express-kiss-api')`
### 判断是否链接成功
```js
const db = mongoose.connection;  //获取链接存到db
db.on('error', console.log);   //失败打印错误
db.once('open', function() {   //成功执行...
  console.log('success!')
});
```
### 创建数据模型文件
####　新建文件 models/post.js
```js
const mongoose = require('mongoose');   //导入 mongoose 功能模块
const Schema = mongoose.Schema;    //调用它提供的 Schema() 接口创建一个新的 schema
const PostSchema = new Schema(    //创建了一个名为 PostSchema 的 schema,包含三个字段category,title,content
  {
    category: { type: String },
    title: { type: String, required: true },    //title数据不能为空
    content: { type: String }
  },
  { timestamps: true }  //选项 timestamps 的值设置为 true，则自动给所映射集合添加 createdAt 和 updatedAt 两个字段
);
module.exports = mongoose.model('Post', PostSchema);  //通过 Mongoose 的 model() 方法把一个 schema 编译成一个 model，一个 model 实例会对应映射集合中的一条记录，这个 model() 方法的第一个参数 Post 则是映射集合名字的单数形式，所以 PostSchema 映射集合的名字是 posts。上述代码还把构建成的 Post Model 导出供外部其它文件使用。
```
#### 打开index.js
```js
const Post = require('./models/post')   //导入post数据模型文件

db.once('open', function() {
  let post = new Post({title: 'mongoose usage'})  //实例化对象，填入title
  post.save(function(err){    //保存到数据库
    if(err) console.log(err)
  })
  console.log('success!')
})
```
### 构建一套 RESTful API
#### 查询所有文章
```js
app.get('/posts', (req, res) => {   //发送get请求到服务器地址/posts
  Post.find().sort({'createdAt': -1}).exec(function(err, posts) {  //Post为上面导入的数据模型文件，查寻所有数据逆序排序，执行完调用函数
    if (err) return res.status(500).json({error: err.message})
    res.json({ posts })
  })
})
```
#### 查找一篇文章
```js
app.get('/post/:id', (req, res) => {
  Post.find({_id: req.params.id}).exec(function(err, post) {   //req.params.id接收前台发来的请求id
    if (err) return res.status(500).json({error: err.message})
    res.json({ post })
  })
})
```
#### 添加一篇文章
首先要装一个包   
`npm i --save body-parser`   
然后添加
```js
var bodyParser = require('body-parser')   //导入body-parser包
app.use(bodyParser.json())   //添加中间键

app.post('/post', (req, res) => {   //发送post请求
  var post = new Post(req.body);   //实例化post对象，传入请求(req)的body的内容
  post.save(function(err){    //向数据库添加数据
    if(err) console.log(err)
  })
} )
```
#### 修改文章内容
```js
app.put('/post/:id', function(req, res) {   //发送put请求
    if (req.body.title === '') return res.status(400).json({error: '文章标题不能为空！'})   //如果请求的标题为空，返回状态码400，json字符串：文章标题不能为空！
    Post.findById({_id: req.params.id}, function(err, post) {  //在数据库中查找id等于请求修改的文章id
      if (err) return res.status(500).json({error:  err.message})
      for (prop in req.body) {   //遍历请求的body内容
        post[prop] = req.body[prop]   //把遍历到的要修改的内容替换到实例化的post对象中
      }
      post.save(function(err) {   //保存修改后的内容
        if (err) return res.status(500).json({error: err.message})
        res.json({
          message: '文章更新成功了！'
        })
      })
    })
  })
```
#### 删除文章
```js
app.delete('/post/:id', function(req, res) {   //发送delete请求
  Post.findById({_id: req.params.id}, function(err, post) {   //查找id相同的
    if (err) return res.status(500).json({error: err.message})
    post.remove(function(err){    //删除找到的数据
      if (err) return res.status(500).json({error: err.message})
      res.json({ message: '文章已经删除了！' })
    })
  })
})
```

### 解决跨域请求的问题
在服务器中处理，先安装包   
`npm i  --save cors`   
然后在index.js文件中添加
```js
const cors = require('cors')
app.use(cors())
```
就可以了

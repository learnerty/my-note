## mongodb
#### 安装mongodb
[MongoDB 中文社区 安装地址](http://docs.mongoing.com/manual-zh/tutorial/install-mongodb-on-ubuntu.html)
1. `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`
2. `echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list`
3. `sudo apt-get update`
4. `sudo apt-get install -y mongodb-org`

#### 查看版本
`mongod --version`

### 创建data文件夹
`mkdir data`
#### 启动服务端
`mongod --dbpath=./data`

#### 启动客户端连接服务器
`mongo --host=127.0.0.1` 或者 `mongo` 按回车键   --host后的值表示服务器的ip地址

#### 查看有哪些数据库
`show dbs`

#### 新建或切换数据库
`use test`  test是数据库的名称

#### 查看当前使用的数据库
`db` 或 `db.getName()`

#### 删除数据库
`db.dropDatabase()` 切换到要删的数据库执行

#### 查看有那些集合(数据库表)
`show tables` 或  `show collections`

### 创建集合
`db.createCollection('users')`   创建users集合

#### 插入集合数据
`db.users.insert({name:'tian',age:23})`  users是集合的名称

#### 查询集合内容
`db.users.find({name:'tian'})` 查询users集合内的内容，find内传入查询条件，不传默认查找全部   
`db.users.find({name:'tian'}).explain()` 查询name为tian的详细信息   
`db.users.ensureIndex({"name": 1})` 给name创建一个索引,1是升序,-1是降序   
1. ensureIndex()创建索引
2. getIndexes()查看索引
3. dropIndex删除索引
**使用索引是也是有代价的：对于添加的每一条索引，每次写操作（插入、更新、删除）都将耗费更多的时间。这是因为，当数据发生变化时，不仅要更新文档，还要更新级集合上的所有索引。因此，mongodb限制每个集合最多有64个索引。通常，在一个特定的集合上，不应该拥有两个以上的索引。**
#### 删除集合数据
`db.users.remove({name:'tian'})` 传入一个{}空条件删除所有

#### 更新数据
`db.users.update({name:'tian'},{$set:{age:22}})` 更新name为tian的age为22,也可以增加不存在的属性

#### save()属性
不传id，插入新文档，传入id，把id符合的覆盖掉
`db.users.save({_id:ObjectId("592e78c76266fab949e54500"),name:'hahaha'})`

#### 返回集合所有数量
`db.users.find().count()`

#### 跳过 skip
`db.users.find().skip(2)`  跳过两条  
`db.users.find().skip(1).limit(1)`  跳过一条查一条

#### 删除集合
`db.users.drop()`

#### 条件操作符
```
$or　　　　或关系
$nor　　　 或关系取反
$gt　　　　大于
$gte　　　 大于等于
$lt　　　　 小于
$lte　　　  小于等于
$ne            不等于
$in             在多个值范围内
$nin           不在多个值范围内
$all            匹配数组中多个值
$regex　　正则，用于模糊查询
$size　　　匹配数组大小
$maxDistance　　范围查询，距离（基于LBS）
$mod　　   取模运算
$near　　　邻域查询，查询附近的位置（基于LBS）
$exists　　  字段是否存在
$elemMatch　　匹配内数组内的元素
$within　　范围查询（基于LBS）
$box　　　 范围查询，矩形范围（基于LBS）
$center       范围醒询，圆形范围（基于LBS）
$centerSphere　　范围查询，球形范围（基于LBS）
$slice　　　　查询字段集合中的元素（比如从第几个之后，第N到第M个元素）
```

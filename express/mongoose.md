## Mongoose是在node.js异步环境下对mongodb进行便捷操作的对象模型工具

###　名词解释
```
Schema：一种以文件形式存储的数据库模型骨架，不具备数据库的操作能力
Model ：由Schema发布生成的模型，具有抽象属性和行为的数据库操作对
Entity：由Model创建的实体，他的操作也会影响数据库
```
### mongoose安装
`npm install mongoose`  
安装成功后，就可以通过 require('mongoose') 来使用！
### 常用数据库操作
```
插入　
Model.save([fn])
更新 　
Model.update(conditions, update, [options], [callback])
Model.findByIdAndUpdate(id, [update], [options], [callback])　根据id更新
Model.findOneAndUpdate([conditions], [update], [options], [callback])　　找到一条记录并更新
删除
Model.remove(conditions, [callback])
Model.findByIdAndRemove(id, [options], [callback])　　　　根据id删除
Model.findOneAndRemove(conditions, [options], [callback])　　找到一条记录并删除
条件查询
Model.find(conditions, [fields], [options], [callback])
User.find({userage: {$gte: 21, $lte: 65}}, callback);    表示查询年龄大于等21而且小于等于65岁
数量查询
Model.count(conditions, [callback])
根据_id查询
Model.findById(id, [fields], [options], [callback])

其它常用方法
去重
Model.distinct(field, [conditions], [callback])
查找一条记录　　　　　　　　　　　　
Model.findOne(conditions, [fields], [options], [callback])
```

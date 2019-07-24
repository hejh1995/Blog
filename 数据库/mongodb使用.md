#### 1. 连接：
- 
#### 2. 创建数据库
- use database_name :  数据库不存在则创建，否则切换到指定数据库。
- show dbs: 查看所有的数据库。
- db.databse_name.insert({"name","名字"})：向数据库插入一些数据。
#### 3. 删除数据库
- db.dropDatabase()
- db.collection.drop(): 删除集合。
  ```
    > use runoob
    switched to db runoob
    > db.createCollection("runoob")     # 先创建集合，类似数据库中的表
    > show tables
    runoob
    > db.runoob.drop()
    true
    > show tables
    > 
  ```
#### 4. 创建集合
- 不需要创建集合，当插入一些文档时，会自动创建集合。
- db.createCollection("mycol", { capped : true, autoIndexId : true, size : 6142800, max : 10000 } )
#### 5. 删除集合
- db.collection_name.drop()
#### 6. 插入文档
- 文档的数据结构和 JSON 基本一样。
- 存储在集合总数据都是BSON格式。
- db.COLLECTION_NAME.insert(document)
- 插入文档你也可以使用 db.col.save(document) 命令。如果不指定 _id 字段 save() 方法类似于 insert() 方法。如果指定 _id 字段，则会更新该 _id 的数据。
- db.collection.insertOne():向指定集合中插入一条文档数据
- db.collection.insertMany():向指定集合中插入多条文档数据
```
// 可以将数据定义为一个变量
> document=({title: 'MongoDB 教程', 
    description: 'MongoDB 是一个 Nosql 数据库',
    by: '菜鸟教程',
    url: 'http://www.runoob.com',
    tags: ['mongodb', 'database', 'NoSQL'],
    likes: 100
});
// 插入
> db.db_name.insert(document)
WriteResult({ "nInserted" : 1 })


> db.db1.insertOne({"a":"2"})
{
	"acknowledged" : true,
	"insertedId" : ObjectId("5d380b2db68670d330ba9cf6")
}

> db.db1.insertMany([{"a":"2"}, {"c":"3"}])
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("5d380d9bb68670d330ba9cf9"),
		ObjectId("5d380d9bb68670d330ba9cfa")
	]
}
```
- 一次插入多条数据：
```
var arr = [];
for (let i = 0; i <= 2000; i++) {
  arr.push({num: i});
};
db.numbers.inert(arr);
```
#### 7. 更新文档
- update() 方法：
- db.col_name.update(查询条件，update的对象和一些更新的操作符等，{upsert:false【如果update的记录不存在，是否插入】, multi:false【只更新找到的第一条记录】,writeConcern:})
#### 8. 删除文档
#### 9.查询文档
#### 10.条件操作符
#### 11. $type 操作符
#### 12. limit 与 skip 方法
#### 13. 排序
#### 14. 索引
#### 15. 聚合
#### 16. 复制（副本集）
#### 17. 分片
#### 18. 备份与恢复
#### 19. 监控

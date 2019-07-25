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
- db.col_name.update(查询条件，update的对象和一些更新的操作符等，{upsert:false【如果update的记录不存在，是否插入】, multi:false【只更新找到的第一条记录】,writeConcern:【抛出异常的级别】})
- 如果要修改多条相同的文档，需要将 multi 设置为 true。
db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}},{multi:true})
```
只更新第一条记录：

db.col.update( { "count" : { $gt : 1 } } , { $set : { "test2" : "OK"} } );
全部更新：

db.col.update( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true );
只添加第一条：

db.col.update( { "count" : { $gt : 4 } } , { $set : { "test5" : "OK"} },true,false );
全部添加进去:

db.col.update( { "count" : { $gt : 5 } } , { $set : { "test5" : "OK"} },true,true );
全部更新：

db.col.update( { "count" : { $gt : 15 } } , { $inc : { "count" : 1} },false,true );
只更新第一条记录：

db.col.update( { "count" : { $gt : 10 } } , { $inc : { "count" : 1} },false,false );
```
- save（）方法：通过传入的文档来替换已有文档。
```
db.collection.save(
   <document>, // 文档数据。
   {
     writeConcern: <document>  // 抛出异常的级别。
   }
)
// 可以通过 find() 来查看替换后的数据
db.col.find().pretty()
```
#### 8. 删除文档
- remove(): 
```
db.collection.remove(
   <query>, // 删除的文档的条件
   {
     justOne: <boolean>, // 默认为false。为true/1时，只删除一个文档。
     writeConcern: <document> // 抛出异常的级别
   }
)
/////////////
> db.db1.remove({'a': '2'}) // 删除所有满足条件的数据
> db.db1.remove({'c':'3'}, 1) // 只删除第一条找到的记录
> db.col.remove({})  // 删除所有数据
```
- remove 并不会真正的释放空间，需要继续执行 db.repairDatabase() 来回收磁盘空间。
- remove() 方法已经过时了，现在官方推荐使用 deleteOne() 和 deleteMany() 方法。
```
如删除集合下全部文档：

db.inventory.deleteMany({})
删除 status 等于 A 的全部文档：

db.inventory.deleteMany({ status : "A" })
删除 status 等于 D 的一个文档：

db.inventory.deleteOne( { status: "D" } )
```
#### 9.查询文档
- find()
```
// and
db.col.find({key1:value1, key2:value2}).pretty()
// or
>db.col.find({$or:[{"by":"菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
// and 和 or 一起
>db.col.find({"likes": {$gt:50}, $or: [{"by": "菜鸟教程"},{"title": "MongoDB 教程"}]}).pretty()
// 其他
```
- 
	操作|格式|范例|RDBMS中的类似语句
	--|:--:|:--:|--:
	等于|{<key>:<value>}|db.col.find({"by":"菜鸟教程"}).pretty()|where by = '菜鸟教程'
	小于|{<key>:{$lt:<value>}}|db.col.find({"likes":{$lt:50}}).pretty()|where likes < 50
	小于或等于|{<key>:{$lte:<value>}}|db.col.find({"likes":{$lte:50}}).pretty()|where likes <= 50
	大于|{<key>:{$gt:<value>}}|db.col.find({"likes":{$gt:50}}).pretty()|where likes > 50
	大于或等于|{<key>:{$gte:<value>}}|db.col.find({"likes":{$gte:50}}).pretty()|where likes >= 50
	不等于|{<key>:{$ne:<value>}}|db.col.find({"likes":{$ne:50}}).pretty()|where likes != 50
	
#### 10.条件操作符
```
$gt -------- greater than  >

$gte --------- gt equal  >=

$lt -------- less than  <

$lte --------- lt equal  <=

$ne ----------- not equal  !=

$eq  --------  equal  =

/////////// 模糊查询
查询 title 包含"教"字的文档：

db.col.find({title:/教/})
查询 title 字段以"教"字开头的文档：

db.col.find({title:/^教/})
查询 titl e字段以"教"字结尾的文档：

db.col.find({title:/教$/})
```
#### 11. $type 操作符
- db.col.find({"title" : {$type : 'string'}}) // 查找col 中 title 为string的数据
- 后面是 可选择的类型
db.col.find({title:/教/})
db.col.find({title:/教/})
db.col.find({title:/教/})
#### 12. limit 与 skip 方法
- limit 读取指定数量的数据，skip 跳过指定数量的数据。
```
limit:
> db.col.find({},{"title":1,_id:0}).limit(2) // 显示查询文档中的两条记录
skip:
>db.col.find({},{"title":1,_id:0}).limit(1).skip(1) // 此时只会显示第二条文档数据
```
#### 13. 排序
- sort（）可以 根据 参数指定排序的字段。1表示升序，-1表示降序。
```
>db.col.find({},{"title":1,_id:0}).sort({"likes":-1})
// skip(), limilt(), sort()三个放在一起执行的时候，执行的顺序是先 sort(), 然后是 skip()，最后是显示的 limit()。
```
#### 14. 索引
- 通常能极大的提高查询的效率
- 可以使用 createIndex 来创建索引。
- 没太懂。。。。
#### 15. 聚合
- 主要用于处理数据，并返回计算后的数据结果。
```
// 以 by_user 为区分，统计个数，显示在 num_tutorial 中，$sum 统计方法，初始值为1
> db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
{
   "result" : [
      {
         "_id" : "runoob.com",
         "num_tutorial" : 2
      },
      {
         "_id" : "Neo4j",
         "num_tutorial" : 1
      }
   ],
   "ok" : 1
}

```
- 可以进行的计算：
	- $sum【求和】
	- $avg【平均值】
	- $max【最大值】
	- $min【最小值】
	- $push【在结果文档中插入值到一个数组中】
	- $addToSet【在结果文档中插入值到一个数组中， 但不创建副本】
	- $first【根据资源文档的排序获取第一个文档数据】
	- $last【根据资源文档的排序获取最后一个文档数据】
#### 16. 复制（副本集）
- 是将数据同步到多个服务器的过程。
- 
#### 17. 分片
#### 18. 备份与恢复
#### 19. 监控
#### 20. 关系
- 关系：
	1:1 (1对1)
	1: N (1对多)
	N: 1 (多对1)
	N: N (多对多)
- 有嵌入关系和引用关系，一般用的比较多的是引用关系。
```
{
   "_id":ObjectId("52ffc33cd85242f436000001"),
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin",
   "address_ids": [
      ObjectId("52ffc4a5d85242602e000000"),
      ObjectId("52ffc4a5d85242602e000001")
   ]
}

//////// 查找

>var result = db.users.findOne({"name":"Tom Benzamin"},{"address_ids":1})
>var addresses = db.address.find({"_id":{"$in":result["address_ids"]}})
// 这里第一句 得用 findOne，它返回的数据类型是 对象。find 返回的数据类型是 数组。
```
#### 21. 数据库引用
- 引用的分类：
	- 手动引用
	- DBRefs
- DBRefs：
	- $ref: 集合名称
	- $id: 引用的id
	- $db: 数据库名称，可选参数
```
{
   "_id":ObjectId("53402597d852426020000002"),
   "address": {
	   "$ref": "address_home",
	   "$id": ObjectId("534009e4d852427820000002"),
	   "$db": "runoob"
	   },
   "contact": "987654321",
   "dob": "01-01-1991",
   "name": "Tom Benzamin"
}

>var user = db.users.findOne({"name":"Tom Benzamin"})
>var dbRef = user.address
// 通过指定 $ref 参数（address_home 集合）来查找集合中指定id的用户地址信息：
>db[dbRef.$ref].findOne({"_id":ObjectId(dbRef.$id)})
```	
- 

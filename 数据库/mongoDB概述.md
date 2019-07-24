#### 1.简介：
- 基于分布式文件存储的数据库。
- 介于关系数据库和非关系数据库之间的产品，属于非关系型数据库。
#### 2. noSQL：
- noSQL：not only SQL【不仅仅是SQL】
  - 非关系型数据库。
  - 可用于超大规模数据的存储，这些类型的数据存储不需要固定的模式，无需多余操作就可以横向扩展。
  - 没有声明性查询语言。
  - 没有预定义的模式
  - 健-值 对 存储，列存储，文档存储，图形数据库
  - 非结构化和不可预知的数据
  - 最终一致性，非ACID
  - CAP 定理
- 关系型数据库遵循的ACID 规则：
  - 原子性：事务种的所以操作要么全部做完，要嘛都不做。【0 和 1】
  - 一致性：
  - 独立性：并发的事务之间不会互相影响。
  - 持久性：修改的数据会被永久保存。
- CAP 定理：
  - 对于分布式系统，不能同时满足一下三点：
    - 一致性：所有数据在同一时间具有相同的数据
    - 可用性：保证每个请求不管成功或者失败都有响应。
    - 分割容忍：系统中任意信息的丢失或失败都不会影响系统的继续运行。
  - 因此将 NoSQL 数据库 分为满足 CA原则、CP 原则、AP 原则
    - CA：单点集群，满足一致性，可用性。可扩展性不太强。
    - CP：满足一致性，分隔容忍性。性能不是特别高。
    - AP：满足可用性，分隔容忍性。对一致性要求低一些。
- 分布式系统：
  - 由多台计算机和通信软件组成，通过计算机网络连接组成。
  - 可以应用在不同的平台上。
- 分布式计算的优点：
  - 可靠性：一台服务器奔溃，不会影响其余服务器。
  - 可扩展性：可根据需要增加更多机器。
  - 资源共享：如银行、预定系统就必须有这种功能。
  - 灵活性：容易安装，实施和调试新的服务。
  - 更快的速度：因为有多台计算机的计算能力，所以有更快的处理速度。
  - 开放系统：本地或者远程都可以访问到该服务。
  - 更高的性能：相较于 集中式 计算机网络集群 可以提供更高的 性能 及 更好的性价比。
- 分布式计算的缺点：
  - 故障排除：
  - 软件：能支持的软件更少。
  - 网络：包括，传输问题、高负载、信息丢失等。
  - 安全性：因为开放性，所以存在数据、共享的安全性。
- NoSQL 的优点：
  - 高可扩展性
  - 分布式计算
  - 低成本
  - 架构的灵活性，半结构化数据
  - 没有复杂的关系
- NoSQL 的缺点：
  - 没有标准化
  - 有限的查询功能
  - 最终一致是不直观的程序
- BASE：
  - 是NoSQL 数据库通常对可用性及一致性的弱要求原则。
  - BA：basically availble，基本可用。
  - S：soft-state，软状态，可以理解为‘无连接’的。
  - E：eventual consistency，最终一致性。
- MongoDB：
  - 属于 文档存储的 NoSQL 数据库。
  - 文档存储，一般用类似 json 的格式存储，存储的内容是文档型的。这样也就有机会对某些字段建立索引，实现关系数据库的某些功能。
  - 
#### 3. MongoDB 简介
- 基础：
  - 由 c++ 语言编写的，是一个 基于分布式文件存储 的 开源 数据库系统
  - 在高负载的情况下，添加更多的节点，可以保证服务器的性能。
- 主要特点：
  - 面向 文档存储 的数据库， 操作简单。
  - 可以在MongoDB记录中设置任何属性的索引 (如：FirstName="Sameer",Address="8 Gandhi Road")来实现更快的排序。
  - 更强的扩展性。可以通过本地或者网络创建数据镜像。
  - 可分片。将增加的负载分布在计算机网络中的其他节点上。
  - 支持丰富的查询表达式。
  - 使用update()命令可以实现替换完成的文档（数据）或者一些指定的数据字段 。
  - Map/reduce主要是用来对数据进行批量处理和聚合操作。
  - Map和Reduce。Map函数调用emit(key,value)遍历集合中所有的记录，将key与value传给Reduce函数进行处理。
  - Map函数和Reduce函数是使用Javascript编写的，并可以通过db.runCommand或mapreduce命令来执行MapReduce操作。
  - GridFS是MongoDB中的一个内置功能，可以用于存放大量小文件。
  - MongoDB允许在服务端执行脚本，可以用Javascript编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。
  - MongoDB支持各种编程语言:RUBY，PYTHON，JAVA，C++，PHP，C#等多种语言。
  - MongoDB安装简单。
- 安装：
  - mac 下
    - 下载安装包：https://www.mongodb.com/download-center/community
    - 解压安装包【打开即解压】
    - 配置环境变量：直接在terminal 里面输入 ‘export PATH=/usr/local/mongodb/bin:$PATH’【记得用pwd 查看文件的地址】
    - 查看效果：
      - 首先创建一个数据库存储目录：sudo mkdir -p /data/db
      - 启动 mongodb，sudo mongodb。默认数据库目录即为 /data/db
      - 再打开一个新的终端：
        ```
          $ cd /usr/local/mongodb/bin 
          $ ./mongo
          MongoDB shell version v4.0.9
          connecting to: mongodb://127.0.0.1:27017/?gssapiServiceName=mongodb
          Implicit session: session { "id" : UUID("3c12bf4f-695c-48b2-b160-8420110ccdcf") }
          MongoDB server version: 4.0.9
          ……
          > 1 + 1
          2
          > 
        ```
        - 此时，数据库的目录还不是 /data/db，可以通过 --dbpath 来指定。sudo mongod --dbpath=/data/db 
#### 4. 概念解析
- 与SQL术语的对比：

SQL 术语|MongoDB 术语|解释说明
--|:--:|--:
database|database|数据库
table|collection|数据库表/集合
row|document|数据记录行/文档
column|field|数据字段/域
index|index|索引
table joins| |表连接，mongodb 不支持
primary key|primary key|主键，MongoDB 自动将_id 字段设置为主键

- 数据库
  - 一个 mongodb 可以建立多个数据库
  - 单个实例 可以容纳多个独立的数据库，每个都有自己的集合和权限，不同的数据库也放在不同的文件中部。
  - 数据库名字要求： 不能是空格，不能含有 ' '（空格)、.、$、/、\和\0 (空字符)，应该全部是小写，最多 64字节。
  - 有些数据库名是保留的，可以直接访问这些有特殊作用的数据库。
    - admin：‘root’数据库，将用户添加到这个数据库，这个用户自动继承所有数据库的权限。
    - local：永远不会被复制。可以用来存储本地单个服务器的任意集合。
    - config：保存分片的相关信息。
  - 简单命令：
  ```
  show dbs // 显示所有数据的列表。
  db // 显示当前数据库对象或集合。
  use 数据库名字 // 连接一个指定的数据库
  
  ```
- 集合
  - 就是文档组 的意思。
  - 可以插入不同格式和类型的数据，但是通常情况下，我们插入的数据都会有一定的关联性。
  - 当都一个文档被插入时，集合就被创建了。
  - 命名：
    - 集合名不能是空字符串""。
    - 集合名不能含有\0字符（空字符)，这个字符表示集合名的结尾。
    - 集合名不能以"system."开头，这是为系统集合保留的前缀。
    - 用户创建的集合名字不能含有保留字符。有些驱动程序的确支持在集合名里面包含，这是因为某些系统生成的集合中包含该字符。除非你要访问这种系统创建的集合，否则千万不要在名字里出现$。　
  - capped collections：
    - 固定大小的 collection
    - 高性能、自动的 维护对象的插入顺序
    - 适合类似记录日志。
    - 必须显示创建，并指定大小（单位是字节，指定的存储大小包含数据库的头信息）
    - MongoDB 的操作日志文件 oplog.rs 就是利用 Capped Collection 来实现的。
    - db.createCollection("mycoll", {capped:true, size:100000})
    - 可以添加新的对象。更新时不能增加存储空间。不能删除文档，只能使用drop（） 删除 collection 中所有的行。
- 文档
  - 当都一个文档被插入时，集合就被创建了。 
  - 文档是一组 键值对（key-value）。不需要设置相同饿字段，并且相同的字段也不需要 相同的 数据类型。
  - 文档中的 key-value 是有序的。
  - key 是字符串。value，可以是字符串，也可以是 其他几种数据类型。
  - 区分 类型 和 大小写。
  - 不能有 重复的key。
  - key命名：
    - 不能含有\0 (空字符)。这个字符用来表示键的结尾。
    - .和$有特别的意义，只有在特定环境下才能使用。
    - 以下划线"_"开头的键是保留的(不是严格要求的)。
- 元信息：
  - 存储数据库的信息。
  - dnname.system.*
    - namespaces: 列出所有名字空间。
    - indexes: 列出所有索引。在{{system.indexes}}插入数据，可以创建索引。
    - profile: 包含数据库概要信息。 {{system.profile}}是可删除的。
    - users: 列出所有可访问数据库的用户。{{system.users}}是可修改的。
    - sources: 包含复制对端（slave）的服务器信息和状态。
 - 数据类型：
  - 字符串【string】：都是 UTF-8编码的。
  - 整型数值【integer】
  - 布尔值【boolean】
  - 双精度浮点值【double】
  - min/max keys
  - 数组【array】
  - 时间戳【timestamp】：
    - 64 位的值。前32位是一个time_t 值（与Unix新纪元相差的秒数）。后32位是在某秒中操作的一个递增的序数。
    - 在单个 mongod 实例中，时间戳值通常是唯一的。
    - BSON 时间戳类型主要用于 MongoDB 内部使用
  - 用于内嵌文档【object】
  - 用于创建空值【null】
  - 符号【symbol】
  - 日期时间【date】
    - 表示当前距离 Unix新纪元（1970年1月1日）的毫秒数。
    - 简单使用：
    ```
    > var mydate1 = new Date()     //格林尼治时间
    > mydate1
    ISODate("2018-03-04T14:58:51.233Z")
    > typeof mydate1
    object
    > var mydate2 = ISODate() //格林尼治时间
    > mydate2
    ISODate("2018-03-04T15:00:45.479Z")
    > typeof mydate2
    object
    > var mydate1str = mydate1.toString()
    > mydate1str
    Sun Mar 04 2018 14:58:51 GMT+0000 (UTC) 
    > typeof mydate1str
    string
    > Date()
    Sun Mar 04 2018 15:02:59 GMT+0000 (UTC)   
    ```
  - 对象ID【object ID】：
    - 包含12 bytes，[0-3]--- 时间戳，[4-6]--- 机器标识码，[7-8]--- 进程id组成的PID，[9-11]--- 随机数。
    - MongoDB 中存储的文档必须有一个 _id 键。这个键的值可以是任何类型的，默认是个 ObjectId 对象
    - 简单使用：
    ```
    > var newObject = ObjectId()
    > newObject.getTimestamp()  // 获取文件的创建时间
    ISODate("2017-11-25T07:21:10Z")
    
    > newObject.str // Objectid 转为 字符串
    5a1919e63df83ce79df8b38f
    ```
  - 二进制数据【binary data】
  - 代码类型【code】
  - 正则表达式类型【regular expression】
  

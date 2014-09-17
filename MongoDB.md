###MongoDB 学习笔记
1. 对于拥有数组的文档，对于多条件匹配查找，不需要数组中有同时满足所有条件的元素；可以每个元素只满足个别条件，只要所有条件都有某个元素满足，就视为匹配上。

2. update方法中使用unset，因为unset对应的value可以为任意常量或者已定义的变量。所以unset的元素为第一个参数中的元素（即查找条件）。

3. 对于find，第二个参数用来表示用来显示或者不显示哪些field，但是不能同时设置显示的field和不显示的field，即不能同时包含field:0和field:1。

4. 数据库备份

* mongodump -d 数据库名 -o 保存文件夹 -h 连接主机（默认localhost）。
* mongorestore -d 数据库名 保存文件夹/* --drop（用来删除原有同名数据库）。
* mongoexport 可以导出数据库中的表，而不能导出数据库。对应的mongoimport有同样的使用范围。

5. 如何开启认证机制

* 创建一个用户管理员（localhost默认用户拥有最高权限，可以通过设置取消该机制）。
在配置文件设置auth为true。
重启mongod。

6. 锁

* MongoDB 的锁是 readers-writer 锁，多个读操作可以同时进行，会阻塞写；一个写操作会阻塞其它所有操作。当一个读操作和一个写操作同时申请锁时，系统优先满足写操作。

* 2.2之前的锁都是针对 mongod 实例的，如果一个 mongod 上有5个 db，则对其中任意一个 db 发起写操作，会使得其他4个 db 同样无法访问。2.2开始引入 db-level 的锁，但是同时保留 global lock，对于一些操作（如复制数据库或者做日志等操作）仍然会锁住整个 mongod 实例。

7. index

* MongoDB 使用 B-tree 来存储索引。

* index 的意义在于是的引擎每次查询操作只需查询部分 documents 来匹配结果，而不是遍历整个 collection。

* 使用 index 的好处之一是 index 的存储默认按升序排列，引擎可以直接按升序或降序遍历索引，而不需要一个额外的排序过程。

* 索引类型

+ Mongo 为每个 collection 的 _id 域自动创建索引。

+ Single filed Index，即根据一个域创建索引。

+ Compound Index，使用一个索引列表，指明多个域，多个域之间有主次关系。如 { userid: 1, score: -1 } 表示索引先按 userid 域的升序排序，然后针对每个 userid，再按 score 的降序排序。

+ Mutikey Index，针对一个 value 是数组类型的域建立的索引，有系统决定是否建立该类型索引。

+ Geospatial Index

+ Text Indexes，匹配一个值是 string 或 string 数组的域，多个单词用空格隔开，表示 OR 关系。如果用 \" 括住，则表示 AND 关系，使用 - 前导符表示非。

+ Hashed Indexes

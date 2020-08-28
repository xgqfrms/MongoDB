# mongodb commands

```sh
# mongodb server
# start mongod
$ mongod --dbpath /System/Volumes/Data/data/db
# macOS 10.15.x 🚀升级bug

$ mongod --dbpath /data/db
# macOS 10.14.x

# stop mongod
$ mongod --shutdown
# Ctrl + C
# kill <mongod process ID>
# Shut down the mongod from the mongo shell using the db.shutdownServer() method as follows:
> use admin
> db.shutdownServer()
# kill -9

```
https://docs.mongodb.com/manual/tutorial/manage-mongodb-processes/#stop-mongod-processes

```sh
# mongodb client
$ mongo

# 查看所有数据库
> show databases;
> show dbs;
> show dbs

# 切换到指定数据库，如果数据库不存在，则创建数据库
> use test

# 插入数据到集合/表，如果集合/表不存在，则先创建集合/表，再插入数据
> db.test_table.insert({"name": "xgqfrms"})
# WriteResult({ "nInserted" : 1 })

# 创建集合，类似SQL数据库中的表
> db.createCollection("test_table")

# 查看集合(表)
> show collections

# 查看表(集合)
> show tables


## 查询文档 find
# > db.collection_name.find(query, projection)
> db.test_table.find().pretty()
# { "_id" : ObjectId("5f492c2d5c778acee17db436"), "name" : "xgqfrms" }
> db.test_table.find().projection()
# { "_id" : ObjectId("5f492c2d5c778acee17db436"), "name" : "xgqfrms" }

# 插入文档
# db.collection_name.insert(document)
# 或
# db.collection_name.save(document)
db.test_table.insert({
  name: "website",
  url: "https://www.xgqfrms.xyz",
});
# db.test_table.insert({
#   "name": "website",
#   "url": "https://www.xgqfrms.xyz",
# });
db.test_table.insert({
  "name": "cdn",
  "url": "https://cdnxgqfrms.xyz",
});

# 更新文档
# update() 和 save()
# db.collection_name.update(
#   <query>,
#   <update>,
# )
db.test_table.update(
  {name: "website"},
  {
    $set: {year: 2020},
  },
)
# db.test_table.update(
#   {"name": "website"},
#   {
#     $set: {"year": 2020},
#   },
# )

# 删除文档
# db.collection_name.remove(
#   <query>,
#   {
#     justOne: <boolean>,
#     writeConcern: <document>
#   }
# )
db.test_table.remove(
  {name: "website"},
)
# db.test_table.remove(
#   {"name": "website"},
# )

# 删除所有数据，(类似常规 SQL 的 truncate 命令)
> db.test_table.remove({})


# 删除集合
# > db.collection_name.drop()
> db.test_table.drop()

# 删除当前数据库
> db.dropDatabase()

```


## 查询 find

```sh
# MongoDB 查询文档数据的语法格式

db.collection_name.find(query, projection)

# query ：可选，使用查询操作符指定查询条件
# projection ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）


# pretty() 方法以格式化的方式来显示所有文档
```

## 插入文档

```sh

db.collection_name.insert(document)
# 或
db.collection_name.save(document)

```

## 更新文档

```sh
# update() 和 save()
db.collection_name.update(
  <query>,
  <update>,
  {
    upsert: <boolean>,
    multi: <boolean>,
    writeConcern: <document>
  }
)

# query: update的查询条件，类似 sql update 查询内where后面的

# update: update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的

# upsert: 可选，这个参数的意思是，如果不存在update的记录，是否插入 objNew, true为插入，默认是false，不插入

# multi: 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新

# writeConcern: 可选，抛出异常的级别。

```

## 删除文档

```sh

db.collection_name.remove(
  <query>,
  {
    justOne: <boolean>,
    writeConcern: <document>
  }
)

```

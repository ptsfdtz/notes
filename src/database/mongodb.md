# mongodb

MongoDB 是文档型数据库，数据以 BSON 文档形式保存，适合字段结构变化较多或以文档整体读取的场景。

## 安装和连接

Windows 可使用 Docker 快速启动：

```powershell
docker run -d --name mongodb -p 27017:27017 -v mongo-data:/data/db mongo:8
docker exec -it mongodb mongosh
```

## 常用操作

```javascript
use app

db.users.insertOne({ name: 'alice', email: 'alice@example.com', createdAt: new Date() })
db.users.find({ name: 'alice' })
db.users.updateOne({ email: 'alice@example.com' }, { $set: { name: 'Alice' } })
db.users.deleteOne({ email: 'alice@example.com' })
```

## 索引

```javascript
db.users.createIndex({ email: 1 }, { unique: true })
db.users.getIndexes()
db.users.find({ email: 'alice@example.com' }).explain('executionStats')
```

## 经验总结

1. 根据查询方式设计文档结构，不要直接把关系型表结构逐表搬到 MongoDB。
2. 高频查询字段要建立索引，同时避免没有查询需求的冗余索引。
3. 生产环境启用认证、备份和副本集；不要将 27017 端口直接暴露到公网。

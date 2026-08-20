# redis

Redis 是内存型键值数据库，常用于缓存、会话、限流和消息队列。缓存数据必须设定合适的过期时间，并处理缓存未命中的回源逻辑。

```bash
redis-cli
SET greeting hello EX 60
GET greeting
INCR page_views
TTL greeting
```

生产环境应启用认证、限制网络访问，并设置内存上限和淘汰策略。不要把 Redis 当作唯一的关键业务数据存储，除非已配置并验证持久化与恢复方案。

## 常用数据结构

```bash
HSET user:1 name alice age 20
HGETALL user:1
LPUSH tasks task-1
RPOP tasks
SADD tags go redis
SMEMBERS tags
```

## 常用排查

```bash
redis-cli INFO memory
redis-cli SLOWLOG GET 10
redis-cli --scan --pattern 'user:*'
```

## 经验总结

1. 访问缓存时设置合理 TTL，防止缓存雪崩和内存无限增长。
2. 大 key 会影响网络和阻塞操作，使用 `SCAN` 代替生产环境中的 `KEYS *`。
3. 缓存更新应考虑一致性；常见做法是先更新数据库，再删除缓存。

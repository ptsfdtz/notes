# postgresql

## 连接与基础操作

```bash
psql -U postgres
CREATE DATABASE app;
CREATE USER app_user WITH PASSWORD 'replace-with-a-secret';
GRANT ALL PRIVILEGES ON DATABASE app TO app_user;
```

## 常用命令

```sql
\l
\c app
\dt
\d users
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'user@example.com';
```

PostgreSQL 建议通过迁移管理表结构。对 JSON、全文检索或高频过滤字段选择匹配的索引类型，并定期关注慢查询和连接数。

## 数据表例子

```sql
CREATE TABLE users (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    email TEXT NOT NULL UNIQUE,
    name TEXT NOT NULL,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_users_created_at ON users (created_at DESC);
```

## 备份与恢复

```bash
pg_dump -U postgres -Fc app > app.dump
createdb -U postgres app_restore
pg_restore -U postgres -d app_restore app.dump
```

## 经验总结

1. `TIMESTAMPTZ` 适合记录业务时间点，应用层统一使用 UTC。
2. SQL 标识符默认转为小写，避免混用带引号的大小写表名。
3. 长事务会阻碍 VACUUM 回收空间，排查时关注空闲事务。

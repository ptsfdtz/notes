# mysql

## 连接与基础操作

```bash
mysql -u root -p
CREATE DATABASE app CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
CREATE USER 'app_user'@'%' IDENTIFIED BY 'replace-with-a-secret';
GRANT SELECT, INSERT, UPDATE, DELETE ON app.* TO 'app_user'@'%';
```

## 常用排查

```sql
SHOW DATABASES;
SHOW TABLES;
DESCRIBE users;
SHOW PROCESSLIST;
EXPLAIN SELECT * FROM users WHERE email = 'user@example.com';
```

为高频筛选和关联列建立索引，并使用 `EXPLAIN` 验证执行计划。定期演练备份恢复，不要只验证备份文件是否存在。

## 数据表例子

```sql
USE app;
CREATE TABLE users (
    id BIGINT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(255) NOT NULL,
    name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    UNIQUE KEY uk_users_email (email)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

## 备份与恢复

```bash
mysqldump -u root -p --single-transaction app > app.sql
mysql -u root -p app < app.sql
```

## 经验总结

1. 业务表优先使用 InnoDB，支持事务和行级锁。
2. 字符集使用 `utf8mb4`，避免表情等字符写入失败。
3. 不要对线上大表直接执行无条件 `UPDATE` 或 `DELETE`；先用 `SELECT` 确认范围。

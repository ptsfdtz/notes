# ci_cd

CI 用于在每次提交时自动构建、测试和检查代码；CD 用于将已验证的构建产物发布到目标环境。

## 最小流程

1. 拉取代码并安装锁定版本的依赖。
2. 执行格式检查、静态检查和测试。
3. 构建不可变产物，例如 Docker 镜像，并以提交 SHA 标记。
4. 发布前执行健康检查；失败时停止推广或回滚。

令牌、部署密钥等敏感信息仅放在 CI 的 Secret 中。缓存依赖时，缓存键应包含锁文件的哈希。

## GitHub Actions 例子

```yaml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run lint
      - run: npm test
      - run: npm run build
```

## 经验总结

1. 安装依赖优先使用 `npm ci`、`pnpm install --frozen-lockfile` 等锁文件模式。
2. 部署步骤应只运行在受保护分支或经审批的环境中。
3. 构建产物和测试报告可作为 artifact 保存，便于排查失败任务。

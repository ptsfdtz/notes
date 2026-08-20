# vite

Vite 提供快速的本地开发服务器和生产构建。

```powershell
pnpm create vite
cd <项目名>
pnpm install
pnpm dev
pnpm build
pnpm preview
```

客户端可读取的环境变量必须以 `VITE_` 开头。不要在前端环境变量中放置私钥或服务端令牌，构建后的值对用户可见。

## 环境变量

创建 `.env.local`：

```text
VITE_API_BASE_URL=http://localhost:8080
```

在代码中读取：

```ts
const apiBaseUrl = import.meta.env.VITE_API_BASE_URL
```

## 常用配置

```ts
import { defineConfig } from 'vite'

export default defineConfig({
  server: { port: 5173 },
})
```

## 经验总结

1. 修改 `.env` 后需要重启开发服务器。
2. 静态资源放在 `public` 时会原样复制，需由构建工具处理的资源放在 `src`。
3. 发布前执行 `pnpm build`，不要只依赖开发服务器中的表现。

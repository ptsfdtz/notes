# typescript

## 创建项目

Vite 创建 React + TypeScript 项目：

```bash
pnpm create vite my-app --template react-ts
cd my-app
pnpm install
pnpm dev
```

已有 JavaScript 项目安装 TypeScript：

```bash
pnpm add -D typescript @types/node
npx tsc --init
```

## 常用类型

```ts
type User = {
  id: string
  name: string
  email?: string
}

function getUserName(user: User): string {
  return user.name
}
```

接口返回数据可先定义类型：

```ts
type ApiResponse<T> = {
  data: T
  message: string
}

const response: ApiResponse<User> = await fetch('/api/user').then((r) => r.json())
```

## 常用命令

```bash
npx tsc --noEmit
npx tsc --init
```

## 经验总结

1. `strict` 建议保持开启，避免 `null`、`undefined` 和隐式 `any` 问题进入运行时。
2. API 数据不能只依赖 TypeScript 类型，外部输入仍需在运行时校验。
3. 优先使用明确的对象类型和联合类型，不要为了省事大量使用 `any`。

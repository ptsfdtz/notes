# nextjs

## pnpm 创建

```bash
pnpm create next-app my-nextjs-app
cd my-nextjs-app
pnpm install
pnpm run dev
```

## 静态导出（GitHub Pages 部署前提）

GitHub Pages 只能托管静态文件，Next.js 需要开启静态导出。在 `next.config.ts` 中设置 `output: 'export'`，否则 `pnpm build` 不会生成 `out/` 目录，workflow 会因找不到发布目录而失败。

```ts
// next.config.ts
import type { NextConfig } from 'next'

const nextConfig: NextConfig = {
  output: 'export',
  basePath: '/<仓库名>',      // 部署到 https://<用户名>.github.io/<仓库名>/ 时填写
  assetPrefix: '/<仓库名>/',  // 与 basePath 保持一致
}

export default nextConfig
```

`basePath` / `assetPrefix` 应与 workflow 中的 `NEXT_PUBLIC_BASE_PATH` 保持一致；仅部署在用户主页（`https://<用户名>.github.io/`）时可以不设置。

## github workflow

```yaml
name: Deploy Next.js 16 to GitHub Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup pnpm
        uses: pnpm/action-setup@v4
        with:
          version: latest

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "20"
          cache: "pnpm"

      - name: Install dependencies
        run: pnpm install

      - name: Build (Next.js static export)
        run: pnpm build
        env:
          NEXT_PUBLIC_BASE_PATH: /${{ github.event.repository.name }}

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./out
          user_name: "github-actions[bot]"
          user_email: "github-actions[bot]@users.noreply.github.com"
```

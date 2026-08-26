# react

## pnpm 和 vite 创建

```bash
pnpm create vite my-react-app --template react
cd my-react-app
pnpm install
pnpm run dev
```

## GitHub Pages 部署的 base 配置

GitHub Pages 子路径部署时，Vite 默认的 `/` 根路径会导致静态资源 404。需要在 `vite.config.ts` 中设置 `base`，与 workflow 中的 `BASE_URL` 保持一致：

```ts
import { defineConfig } from 'vite'

export default defineConfig({
  base: '/<仓库名>/',
})
```

仅部署到用户主页（`https://<用户名>.github.io/`）时使用默认 `base: '/'` 即可。注意 workflow 中设置的 `BASE_URL` 环境变量不会自动改变 Vite 的 `base`，必须显式配置。

## github workflow

```yaml
name: Deploy to GitHub Pages

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

      - name: Build
        run: pnpm build
        env:
          BASE_URL: /${{ github.event.repository.name }}/

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          user_name: "github-actions[bot]"
          user_email: "github-actions[bot]@users.noreply.github.com"
```

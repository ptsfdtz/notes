# svelte

## 创建项目

```powershell
npx sv create my-app
cd my-app
npm install
npm run dev
```

Svelte 组件将状态、模板和样式放在同一文件中。派生值应保持可计算，异步请求应处理加载、空数据和失败状态；路由项目可使用 SvelteKit 的 `load` 函数在页面层获取数据。

## 组件例子

> `sv create` 生成的是 Svelte 5 项目，事件使用 `onclick` 属性；Svelte 4 的 `on:click` 语法在新项目中已弃用。

```svelte
<script>
  let count = 0;
</script>

<button onclick={() => count += 1}>
  count: {count}
</button>
```

## 常用命令

```bash
npm run dev
npm run check
npm run build
npm run preview
```

## 经验总结

1. 页面级数据获取优先放在路由层，组件更容易复用和测试。
2. 表单提交时禁用重复提交，并把服务端校验错误显示给用户。
3. 发布前运行 `npm run check`，可发现类型和 Svelte 模板问题。

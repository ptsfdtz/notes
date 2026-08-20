# vue

## 创建项目

```powershell
pnpm create vue@latest
cd <项目名>
pnpm install
pnpm dev
```

单文件组件使用 `<script setup>`、`<template>` 和 `<style>` 组织。将可复用逻辑提取为 composable，跨页面状态使用 Pinia 等状态库，而不是在组件间层层传递。

## 组件例子

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">count: {{ count }}</button>
</template>
```

## 常用命令

```bash
pnpm dev
pnpm build
pnpm lint
pnpm add vue-router pinia
```

## 经验总结

1. 模板中不要写复杂业务计算，使用 `computed` 保持模板可读。
2. 列表渲染必须提供稳定的 `:key`，不要直接使用会变化的数组下标。
3. API 请求要处理加载、失败和空数据状态。

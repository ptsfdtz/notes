# tailwindcss

Tailwind CSS 通过原子类组合样式。优先复用项目的颜色、间距和字体 token，避免同类元素散落大量不一致的任意值。

```html
<button class="rounded bg-blue-600 px-4 py-2 text-white hover:bg-blue-700">
  保存
</button>
```

复杂组件可抽取为框架组件或使用 `@apply` 定义少量语义化样式；响应式前缀如 `md:` 应基于内容布局需求使用，而不是设备品牌。

## 常用写法

```html
<div class="mx-auto grid max-w-6xl gap-4 p-4 md:grid-cols-2">
  <input class="w-full border border-slate-300 px-3 py-2 focus:outline-none focus:ring-2" />
</div>
```

## 状态和响应式前缀

```html
<button class="bg-slate-900 text-white hover:bg-slate-700 disabled:opacity-50 md:px-6">
  提交
</button>
```

## 经验总结

1. 颜色和间距保持使用同一组 token，页面观感更统一。
2. 类名过长时先抽组件；不要为了缩短类名过度使用 `@apply`。
3. 使用 Prettier 的 Tailwind 插件自动排序类名，减少无意义的 diff。

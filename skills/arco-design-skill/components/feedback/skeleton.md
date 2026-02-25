---
name: arco-skeleton
description: Arco Skeleton 骨架屏组件用法与 API。当需要在数据加载期间展示占位骨架动画时使用。
user-invocable: false
---

# Skeleton 骨架屏

```tsx
import { Skeleton } from '@arco-design/web-react';

<Skeleton loading={loading} animation>
  <div>实际内容</div>
</Skeleton>

// 自定义组合
<Skeleton loading={loading} animation text={{ rows: 3 }} image />

// 细粒度控制
<Skeleton>
  <Skeleton.Image style={{ width: 200, height: 200 }} />
  <Skeleton.Line rows={3} />
</Skeleton>
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `loading` | `boolean` | `true` | 是否显示骨架 |
| `animation` | `boolean` | — | 动画效果 |
| `image` | `boolean \| SkeletonImageProps` | — | 图片占位 |
| `text` | `boolean \| { rows, width }` | `true` | 文字占位 |

## 最佳实践

- **用于首屏加载**，给出内容布局预期
- **配合 `animation`** 提供更好的加载体验
- **组合使用 Skeleton.Image + Skeleton.Line** 模拟具体布局

## 常用模式

```tsx
// 文本骨架
<Skeleton loading={loading} text={{ rows: 3, width: ['100%', '80%', '60%'] }}>
  <div>实际内容</div>
</Skeleton>

// 图片 + 文本
<Skeleton loading={loading} image text={{ rows: 2 }}>
  <Card>实际卡片内容</Card>
</Skeleton>

// 自定义动画
<Skeleton animation loading={loading} text={{ rows: 5 }}>
  <Article />
</Skeleton>

// 列表骨架
{loading
  ? Array.from({ length: 5 }).map((_, i) => (
      <Skeleton key={i} text={{ rows: 2 }} image={{ size: 40, shape: 'circle' }} style={{ marginBottom: 16 }} />
    ))
  : list.map(item => <ListItem key={item.id} {...item} />)
}
```

## 最佳实践

1. **loading 属性控制显隐** —— 直接包裹实际内容，loading=true 时显示骨架
2. **width 模拟真实文本宽度** —— 不同行设置不同宽度更真实
3. **animation 增强感知** —— 动画骨架让用户感觉在加载中
4. **列表页用循环生成** —— 生成 N 个骨架项匹配预期列表长度

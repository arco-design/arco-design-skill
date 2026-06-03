---
name: arco-card
description: "Arco Design Card component API. Use for card containers, cover cards, card grids (Card.Grid), card actions, and Card.Meta."
user-invocable: false
---

# Card 卡片

通用卡片容器。

```tsx
import { Card } from '@arco-design/web-react';

<Card title="卡片标题" extra={<Link>更多</Link>} style={{ width: 360 }}>
  卡片内容
</Card>

// 带封面
<Card cover={<img src="/cover.jpg" />}>
  <Card.Meta title="标题" description="描述文字" />
</Card>

// 栅格卡片
<Card.Grid hoverable style={{ width: '25%' }}>
  内容
</Card.Grid>
```

### CardProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `title` | `ReactNode` | — | 标题 |
| `extra` | `ReactNode` | — | 右上角操作区 |
| `cover` | `ReactNode` | — | 封面 |
| `actions` | `ReactNode[]` | — | 底部操作列表 |
| `bordered` | `boolean` | `true` | 边框 |
| `loading` | `boolean` | — | 加载状态 |
| `hoverable` | `boolean` | — | 可悬停 |
| `size` | `'default' \| 'small'` | — | 尺寸 |
| `headerStyle` | `CSSProperties` | — | 头部样式 |
| `bodyStyle` | `CSSProperties` | — | 内容样式 |

### Card.Meta Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `avatar` | `ReactNode` | 头像 |
| `title` | `ReactNode` | 标题 |
| `description` | `ReactNode` | 描述 |

### Card.Grid Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `hoverable` | `boolean` | `true` | 悬停效果 |
| `style` | `CSSProperties` | — | 自定义样式（常用于 `width: '25%'` 等栅格分割） |
| `className` | `string \| string[]` | — | class |
| `onClick` | `(e) => void` | — | 点击回调 |


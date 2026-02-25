---
name: arco-card
description: Arco Card 卡片组件用法与 API。当需要卡片容器、带封面卡片、卡片网格或可操作卡片时使用。
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



---
name: arco-space
description: Arco Space 间距组件用法与 API。当需要给组件之间设置统一的水平或垂直间距时使用。
user-invocable: false
---

# Space 间距

设置组件之间的间距，替代手动设置 margin。

## 基本用法

```tsx
import { Space, Button } from '@arco-design/web-react';

<Space>
  <Button>按钮1</Button>
  <Button>按钮2</Button>
  <Button>按钮3</Button>
</Space>

// 垂直排列
<Space direction="vertical" size="large">
  <Input placeholder="输入框1" />
  <Input placeholder="输入框2" />
</Space>
```

## API

### SpaceProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `direction` | `'vertical' \| 'horizontal'` | `'horizontal'` | 排列方向 |
| `size` | `'mini' \| 'small' \| 'medium' \| 'large' \| number` | `'small'` | 间距大小 |
| `align` | `'start' \| 'end' \| 'center' \| 'baseline'` | — | 对齐方式 |
| `wrap` | `boolean` | `false` | 是否自动换行 |
| `split` | `ReactNode` | — | 分隔符 |

## 常用模式

```tsx
// 自动换行
<Space wrap size={16}>
  {tags.map(tag => <Tag key={tag}>{tag}</Tag>)}
</Space>

// 自定义间距大小
<Space size={24}>
  <Card>卡片1</Card>
  <Card>卡片2</Card>
</Space>

// 带分隔符
<Space split={<Divider type="vertical" />}>
  <Link>链接1</Link>
  <Link>链接2</Link>
  <Link>链接3</Link>
</Space>

// 对齐方式
<Space align="center">
  <Button size="large">大</Button>
  <Button size="small">小</Button>
</Space>
```

## 最佳实践

1. **替代手动 margin**，保持间距一致性
2. **使用 `wrap` 处理动态数量的元素**（如标签列表）
3. **`split` 用于面包屑式的分隔布局**

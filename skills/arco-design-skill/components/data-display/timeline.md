---
name: arco-timeline
description: Arco Timeline 时间线组件用法与 API。当需要展示时间轴、流程步骤或变更记录时使用。
user-invocable: false
---

# Timeline 时间线

```tsx
import { Timeline } from '@arco-design/web-react';

<Timeline>
  <Timeline.Item label="2024-01-01">事件一</Timeline.Item>
  <Timeline.Item label="2024-02-01" dotColor="red">事件二</Timeline.Item>
  <Timeline.Item label="2024-03-01">事件三</Timeline.Item>
</Timeline>

// 水平方向
<Timeline direction="horizontal" mode="alternate">
  <Timeline.Item>步骤1</Timeline.Item>
  <Timeline.Item>步骤2</Timeline.Item>
</Timeline>
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `direction` | `'horizontal' \| 'vertical'` | `'vertical'` | 方向 |
| `mode` | `'left' \| 'right' \| 'alternate'` | `'left'` | 显示模式 |
| `reverse` | `boolean` | — | 逆序 |
| `pending` | `boolean \| ReactNode` | — | 加载中 |
| `labelPosition` | `'relative' \| 'same'` | — | 标签位置 |

### Timeline.Item

| 属性 | 类型 | 说明 |
|------|------|------|
| `label` | `ReactNode` | 标签 |
| `dot` | `ReactNode` | 自定义节点 |
| `dotColor` | `string` | 节点颜色 |
| `dotType` | `'default' \| 'hollow'` | 节点类型 |
| `lineType` | `'solid' \| 'dashed' \| 'dotted'` | 连线类型 |
| `lineColor` | `string` | 连线颜色 |

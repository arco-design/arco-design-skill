---
name: arco-badge
description: Arco Badge 徽标组件用法与 API。当需要在元素上显示数字或状态小红点时使用。
user-invocable: false
---

# Badge 徽标

```tsx
import { Badge, Avatar } from '@arco-design/web-react';

<Badge count={5}><Avatar shape="square">头像</Avatar></Badge>
<Badge count={100} maxCount={99}><Avatar shape="square">头像</Avatar></Badge>
<Badge dot><Avatar shape="square">头像</Avatar></Badge>
<Badge status="processing" text="进行中" />
<Badge color="#165DFF" text="自定义颜色" />
```

## BadgeProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `count` | `number \| ReactNode` | — | 数字 |
| `maxCount` | `number` | `99` | 最大显示数 |
| `dot` | `boolean` | — | 小红点 |
| `dotStyle` | `CSSProperties` | — | 点样式 |
| `offset` | `[number, number]` | — | 偏移 |
| `text` | `string` | — | 文本 |
| `status` | `'default' \| 'processing' \| 'success' \| 'warning' \| 'error'` | — | 状态点 |
| `color` | `string` | — | 自定义颜色 |

## 常用模式

```tsx
// 消息通知徽标
<Badge count={unreadCount}>
  <IconNotification style={{ fontSize: 24 }} />
</Badge>

// 状态指示
<Badge status="success" text="已上线" />
<Badge status="processing" text="进行中" />
<Badge status="warning" text="待审核" />
<Badge status="error" text="已失败" />

// 自定义偏移
<Badge count={5} offset={[6, -2]}>
  <Avatar shape="square">头像</Avatar>
</Badge>

// 自定义颜色标记
<Badge color="arcoblue" text="技术" />
<Badge color="green" text="通过" />
<Badge color="red" text="紧急" />
```

## 最佳实践

1. **maxCount 别设太大** —— 通常 99 或 999 就够了
2. **状态指示用 status** —— 比 count 更适合表达状态语义
3. **小红点用 dot** —— 只需提示有新内容、不需要显示数量时使用
4. **注意 count 为 0 时默认不显示** —— 如需显示设置 `count={0}` 并搭配 `showZero`

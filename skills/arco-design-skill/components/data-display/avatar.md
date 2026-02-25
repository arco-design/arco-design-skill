---
name: arco-avatar
description: Arco Avatar 头像组件用法与 API。当需要展示用户头像、头像组或带徽标的头像时使用。
user-invocable: false
---

# Avatar 头像

```tsx
import { Avatar } from '@arco-design/web-react';

<Avatar>A</Avatar>
<Avatar style={{ backgroundColor: '#165DFF' }}>张</Avatar>
<Avatar size={64}><img src="/avatar.png" alt="avatar" /></Avatar>
<Avatar shape="square">B</Avatar>

// 头像组
<Avatar.Group size={40} maxCount={3}>
  <Avatar>A</Avatar>
  <Avatar>B</Avatar>
  <Avatar>C</Avatar>
  <Avatar>D</Avatar>
</Avatar.Group>
```

### AvatarProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `size` | `number` | `40` | 大小 |
| `shape` | `'circle' \| 'square'` | `'circle'` | 形状 |
| `triggerIcon` | `ReactNode` | — | 交互图标 |
| `triggerType` | `'button' \| 'mask'` | `'button'` | 交互类型 |
| `onClick` | `(e) => void` | — | 点击回调 |

### Avatar.Group Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `size` | `number` | 统一大小 |
| `maxCount` | `number` | 最多显示个数 |
| `zIndexAscend` | `boolean` | z-index 递增 |
| `maxPopoverTriggerProps` | `TriggerProps` | 更多弹出配置 |



---
name: arco-avatar
description: "Arco Design Avatar component API. Use for user avatars, avatar groups, badges on avatars, and image/text/icon avatars."
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
| `triggerIconStyle` | `CSSProperties` | — | 交互图标样式 |
| `triggerType` | `'button' \| 'mask'` | `'button'` | 交互类型 |
| `autoFixFontSize` | `boolean` | `true` | 根据 size 自动调整字体 |
| `onClick` | `(e) => void` | — | 点击回调 |

### Avatar.Group Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `size` | `number` | 统一大小 |
| `shape` | `'circle' \| 'square'` | 统一形状 |
| `maxCount` | `number` | 最多显示个数 |
| `maxStyle` | `CSSProperties` | "+N" 头像样式 |
| `autoFixFontSize` | `boolean` | 自动调整字体（默认 true） |
| `zIndexAscend` | `boolean` | z-index 递增 |
| `maxPopoverTriggerProps` | `Partial<TriggerProps>` | "+N" 弹出层配置 |



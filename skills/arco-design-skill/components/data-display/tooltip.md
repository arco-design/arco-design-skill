---
name: arco-tooltip
description: Arco Tooltip 文字提示组件用法与 API。当需要鼠标悬停时显示简单的文字提示信息时使用。
user-invocable: false
---

# Tooltip 文字气泡

简单的文字提示气泡框。

```tsx
import { Tooltip, Button } from '@arco-design/web-react';

<Tooltip content="提示文字">
  <Button>鼠标悬停</Button>
</Tooltip>

<Tooltip position="right" content="右侧提示" color="#165DFF">
  <Button>右侧</Button>
</Tooltip>
```

### TooltipProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `content` | `ReactNode` | — | 提示内容 |
| `position` | `'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'` | `'top'` | 弹出位置 |
| `trigger` | `'hover' \| 'focus' \| 'click'` | `'hover'` | 触发方式 |
| `popupVisible` | `boolean` | — | 受控可见 |
| `defaultPopupVisible` | `boolean` | — | 默认可见 |
| `color` | `string` | — | 背景色 |
| `mini` | `boolean` | — | 迷你模式 |
| `disabled` | `boolean` | — | 禁用 |
| `getPopupContainer` | `(node) => Element` | — | 弹出容器 |
| `onVisibleChange` | `(visible: boolean) => void` | — | 可见变化 |

## 常用模式

```tsx
// 不同位置
<Tooltip position="top" content="顶部提示"><Button>上</Button></Tooltip>
<Tooltip position="right" content="右侧提示"><Button>右</Button></Tooltip>

// 迷你模式（无箭头，紧凑）
<Tooltip mini content="提示"><IconQuestionCircle /></Tooltip>

// 富文本内容
<Tooltip content={<div><strong>标题</strong><br/>详细描述</div>}>
  <Link>帮助</Link>
</Tooltip>

// 受控显示
const [visible, setVisible] = useState(false);
<Tooltip visible={visible} content="受控提示">
  <Button onMouseEnter={() => setVisible(true)} onMouseLeave={() => setVisible(false)}>悬停</Button>
</Tooltip>
```

## 最佳实践

1. **Tooltip 只放简短文字** —— 复杂内容用 Popover
2. **图标按钮必加 Tooltip** —— 仅图标按钮用 Tooltip 说明用途
3. **不要在 disabled 元素上直接用** —— disabled 元素不触发事件，需要包一层 `<span>`
4. **mini 模式适合行内提示** —— 如表格列标题旁的问号图标

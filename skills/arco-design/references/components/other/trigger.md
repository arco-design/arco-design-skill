---
name: arco-trigger
description: "Arco Design Trigger component API. Base component for popup positioning — underlying Tooltip, Popover, and Dropdown."
user-invocable: false
---

# Trigger 触发器

通用弹出层触发器，是 Tooltip、Popover、Dropdown 等组件的基础。

```tsx
import { Trigger, Button } from '@arco-design/web-react';

<Trigger
  popup={() => <div style={{ padding: 16, background: '#fff', boxShadow: '0 2px 8px rgba(0,0,0,0.15)' }}>弹出内容</div>}
  trigger="click"
  position="bottom"
>
  <Button>点击弹出</Button>
</Trigger>
```

## TriggerProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `popup` | `() => ReactNode` | — | 弹出内容 |
| `trigger` | `'hover' \| 'click' \| 'focus' \| 'contextMenu'` | `'hover'` | 触发方式 |
| `position` | `'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'` | `'bottom'` | 弹出位置 |
| `popupVisible` | `boolean` | — | 受控可见 |
| `defaultPopupVisible` | `boolean` | — | 默认可见 |
| `clickToClose` | `boolean` | `true` | 再次点击关闭 |
| `clickOutsideToClose` | `boolean` | `true` | 点击外部关闭 |
| `escToClose` | `boolean` | — | ESC 关闭 |
| `mouseEnterDelay` | `number` | `100` | 鼠标移入延迟 |
| `mouseLeaveDelay` | `number` | `100` | 鼠标移出延迟 |
| `showArrow` | `boolean` | — | 显示箭头 |
| `alignPoint` | `boolean` | — | 跟随鼠标位置 |
| `popupAlign` | `{ top, bottom, left, right }` | — | 弹出偏移 |
| `getPopupContainer` | `(node) => Element` | — | 弹出容器 |
| `autoAlignPopupWidth` | `boolean` | — | 弹出层与触发器同宽 |
| `autoAlignPopupMinWidth` | `boolean` | — | 最小宽度对齐 |
| `autoFitPosition` | `boolean` | `true` | 自动调整位置避免遮挡 |
| `autoFixPosition` | `boolean` | — | 触发元素尺寸变化时重新定位 |
| `updateOnScroll` | `boolean` | — | 容器滚动时更新位置 |
| `unmountOnExit` | `boolean` | `true` | 关闭销毁 |
| `popupStyle` | `CSSProperties` | — | 弹出层样式 |
| `classNames` | `string` | — | 自定义动画 class（CSSTransition） |
| `duration` | `number \| { enter, exit }` | — | 动画时长 |
| `childrenPrefix` | `string` | — | 触发元素 open 状态 class 前缀 |
| `focusDelay` | `number` | — | focus 触发延迟 |
| `getDocument` | `() => HTMLElement` | — | 用于点击外部判断的根节点 |
| `popupHoverStay` | `boolean` | `true` | 鼠标在弹出层时保持显示 |
| `blurToHide` | `boolean` | `true` | focus 触发模式下 blur 关闭 |
| `mouseLeaveToClose` | `boolean` | `true` | hover 触发模式下移出关闭 |
| `arrowProps` | `HTMLAttributes<HTMLDivElement>` | — | 自定义箭头属性 |
| `onVisibleChange` | `(visible) => void` | — | 可见变化 |

> **大多数情况不需要直接使用 Trigger**，应使用 Tooltip、Popover、Dropdown 等封装组件。

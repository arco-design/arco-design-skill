---
name: arco-dropdown
description: "Arco Design Dropdown component API. Use for dropdown menus, context menus, button dropdowns, and action lists."
user-invocable: false
---

# Dropdown 下拉菜单

```tsx
import { Dropdown, Menu, Button } from '@arco-design/web-react';

<Dropdown
  droplist={
    <Menu>
      <Menu.Item key="1">选项1</Menu.Item>
      <Menu.Item key="2">选项2</Menu.Item>
      <Menu.Item key="3" disabled>选项3</Menu.Item>
    </Menu>
  }
  position="bl"
>
  <Button type="text">悬停显示 <IconDown /></Button>
</Dropdown>

// 右键菜单
<Dropdown trigger="contextMenu" droplist={<Menu>...</Menu>}>
  <div style={{ width: 300, height: 200, border: '1px dashed' }}>
    右键点击区域
  </div>
</Dropdown>
```

### DropdownProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `droplist` | `ReactNode` | — | 下拉菜单（通常为 Menu） |
| `position` | `'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br'` | `'bl'` | 弹出位置 |
| `trigger` | `'hover' \| 'click' \| 'contextMenu'` | `'hover'` | 触发方式 |
| `disabled` | `boolean` | — | 禁用 |
| `popupVisible` / `defaultPopupVisible` | `boolean` | — | 可见状态 |
| `unmountOnExit` | `boolean` | `true` | 关闭销毁 |
| `getPopupContainer` | `(node) => Element` | — | 弹出容器（默认 `document.body`） |
| `triggerProps` | `Partial<TriggerProps>` | — | 透传给底层 Trigger（如 `mouseEnterDelay`、`autoFitPosition`） |
| `onVisibleChange` | `(visible) => void` | — | 可见变化 |

### Dropdown.Button

```tsx
<Dropdown.Button
  type="primary"
  droplist={<Menu>...</Menu>}
  onClick={() => handleClick()}
>
  操作
</Dropdown.Button>
```



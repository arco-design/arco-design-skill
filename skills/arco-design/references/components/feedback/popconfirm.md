---
name: arco-popconfirm
description: "Arco Design Popconfirm component API. Use for lightweight confirmation popups before actions like delete or submit."
user-invocable: false
---

# Popconfirm 气泡确认

点击弹出的确认气泡框。

```tsx
import { Popconfirm, Button } from '@arco-design/web-react';

<Popconfirm
  title="确认删除？"
  onOk={() => handleDelete()}
  onCancel={() => {}}
>
  <Button status="danger">删除</Button>
</Popconfirm>
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `title` | `ReactNode` | — | 确认标题 |
| `content` | `ReactNode` | — | 详细内容 |
| `onOk` | `() => void \| Promise` | — | 确认回调 |
| `onCancel` | `() => void` | — | 取消回调 |
| `okText` / `cancelText` | `string` | — | 按钮文字 |
| `okButtonProps` / `cancelButtonProps` | `ButtonProps` | — | 按钮属性 |
| `okType` | `ButtonProps['type']` | `'primary'` | 确认按钮类型 |
| `position` | `TooltipPosition` | `'top'` | 弹出位置 |
| `focusLock` | `boolean` | — | 焦点锁定 |
| `autoFocus` | `boolean` | — | 弹出后自动聚焦首个按钮 |
| `disabled` | `boolean` | — | 禁用（不弹出确认） |
| `trigger` | `'hover' \| 'click' \| 'focus'` | `'click'` | 触发方式（继承 Trigger） |
| `triggerProps` | `Partial<TriggerProps>` | — | 透传给底层 Trigger |
| `getPopupContainer` | `(node) => Element` | — | 弹出容器 |

## 常用模式

```tsx
// 异步确认（onOk 返回 Promise 时自动 loading）
<Popconfirm
  title="确认删除？"
  onOk={async () => {
    await deleteItem(id);
    Message.success('删除成功');
  }}
>
  <Button status="danger">删除</Button>
</Popconfirm>
```

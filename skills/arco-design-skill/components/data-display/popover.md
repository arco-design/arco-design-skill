---
name: arco-popover
description: Arco Popover 气泡卡片组件用法与 API。当需要点击或悬停弹出气泡式卡片展示更复杂内容时使用。
user-invocable: false
---

# Popover 气泡卡片

点击/悬停弹出气泡式卡片，可放置更复杂的内容。

```tsx
import { Popover, Button } from '@arco-design/web-react';

<Popover title="标题" content="气泡卡片内容">
  <Button>悬停弹出</Button>
</Popover>

<Popover trigger="click" title="操作" content={
  <div>
    <Button type="primary" size="small">确认</Button>
  </div>
}>
  <Button>点击弹出</Button>
</Popover>
```

## PopoverProps

继承 Tooltip 的所有 props，额外支持：

| 属性 | 类型 | 说明 |
|------|------|------|
| `title` | `ReactNode` | 标题 |
| `content` | `ReactNode \| (() => ReactNode)` | 内容 |
| `position` | `'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br' \| 'left' \| 'lt' \| 'lb' \| 'right' \| 'rt' \| 'rb'` | 弹出位置 |
| `trigger` | `'hover' \| 'focus' \| 'click'` | 触发方式 |
| `popupVisible` / `defaultPopupVisible` | `boolean` | 可见状态 |
| `disabled` | `boolean` | 禁用 |
| `getPopupContainer` | `(node) => Element` | 弹出容器 |
| `onVisibleChange` | `(visible: boolean) => void` | 可见变化 |

## 常用模式

```tsx
// 点击触发
<Popover trigger="click" title="用户信息" content={<UserCard userId={id} />}>
  <Button>查看详情</Button>
</Popover>

// 确认操作（类似 Popconfirm 但内容更丰富）
<Popover
  trigger="click"
  content={
    <div>
      <p>确定要删除这条记录吗？此操作不可恢复。</p>
      <Space style={{ justifyContent: 'flex-end', width: '100%' }}>
        <Button size="mini">取消</Button>
        <Button size="mini" type="primary" status="danger">删除</Button>
      </Space>
    </div>
  }
>
  <Button status="danger">删除</Button>
</Popover>

// 受控
const [visible, setVisible] = useState(false);
<Popover visible={visible} onVisibleChange={setVisible} content="受控内容">
  <Button>受控弹出</Button>
</Popover>
```

## 最佳实践

1. **简单文字用 Tooltip，复杂内容用 Popover** —— Popover 支持 title + 富文本 content
2. **确认操作优先用 Popconfirm** —— Popconfirm 是 Popover 的特化，更简洁
3. **trigger="click" 用于需要交互的内容** —— 包含按钮、链接等可操作元素时

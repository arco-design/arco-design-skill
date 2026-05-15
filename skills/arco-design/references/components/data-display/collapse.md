---
name: arco-collapse
description: "Arco Design Collapse component API. Use for collapsible panels, accordion (single expand), FAQ sections, and nested collapsible content."
user-invocable: false
---

# Collapse 折叠面板

```tsx
import { Collapse } from '@arco-design/web-react';

<Collapse defaultActiveKey={['1']}>
  <Collapse.Item header="面板1" name="1">内容1</Collapse.Item>
  <Collapse.Item header="面板2" name="2">内容2</Collapse.Item>
  <Collapse.Item header="面板3" name="3" disabled>内容3</Collapse.Item>
</Collapse>

// 手风琴模式（同时只展开一个）
<Collapse accordion>
  <Collapse.Item header="面板1" name="1">内容1</Collapse.Item>
  <Collapse.Item header="面板2" name="2">内容2</Collapse.Item>
</Collapse>
```

## CollapseProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `activeKey` / `defaultActiveKey` | `string[]` | — | 展开的面板 |
| `accordion` | `boolean` | — | 手风琴模式 |
| `bordered` | `boolean` | `true` | 边框 |
| `expandIcon` | `ReactNode` | — | 自定义展开图标 |
| `expandIconPosition` | `'left' \| 'right'` | `'left'` | 展开图标位置 |
| `triggerRegion` | `'header' \| 'icon'` | `'header'` | 触发展开的区域（2.41.0） |
| `lazyload` | `boolean` | `true` | 延迟渲染 |
| `destroyOnHide` | `boolean` | — | 隐藏时销毁 |
| `onChange` | `(key, keys, e) => void` | — | 展开变化 |

## CollapseItemProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | `string` | — | 唯一标识 |
| `header` | `ReactNode` | — | 面板标题 |
| `extra` | `ReactNode` | — | 标题右侧额外内容 |
| `disabled` | `boolean` | — | 禁用 |
| `showExpandIcon` | `boolean` | `true` | 显示展开图标 |
| `expandIcon` | `ReactNode` | — | 自定义展开图标（覆盖 Collapse） |
| `contentStyle` | `CSSProperties` | — | 内容区样式 |
| `destroyOnHide` | `boolean` | — | 隐藏时销毁（覆盖 Collapse） |

## 常用模式

```tsx
// 手风琴模式（同时只展开一个）
<Collapse accordion>
  <Collapse.Item header="章节一" name="1">内容一</Collapse.Item>
  <Collapse.Item header="章节二" name="2">内容二</Collapse.Item>
</Collapse>

// 无边框简洁模式
<Collapse bordered={false} defaultActiveKey={['1']}>
  <Collapse.Item header="FAQ 1" name="1">回答一</Collapse.Item>
  <Collapse.Item header="FAQ 2" name="2">回答二</Collapse.Item>
</Collapse>

// 嵌套折叠面板
<Collapse>
  <Collapse.Item header="父级" name="parent">
    <Collapse>
      <Collapse.Item header="子级" name="child">嵌套内容</Collapse.Item>
    </Collapse>
  </Collapse.Item>
</Collapse>
```

## 最佳实践

1. **FAQ 页面使用 accordion** —— 同时只展开一个减少认知负担
2. **默认展开重要内容** —— 通过 `defaultActiveKey` 预展开关键面板
3. **`destroyOnHide` 释放资源** —— 隐藏时销毁内容，适合包含表单或大量 DOM 的面板

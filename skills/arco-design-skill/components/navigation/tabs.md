---
name: arco-tabs
description: Arco Tabs 标签页组件用法与 API。当需要实现标签页切换、卡片式标签或可编辑标签页时使用。
user-invocable: false
---

# Tabs 标签页

```tsx
import { Tabs } from '@arco-design/web-react';

<Tabs defaultActiveTab="1">
  <Tabs.TabPane key="1" title="标签1">内容1</Tabs.TabPane>
  <Tabs.TabPane key="2" title="标签2">内容2</Tabs.TabPane>
  <Tabs.TabPane key="3" title="标签3" disabled>内容3</Tabs.TabPane>
</Tabs>

// 卡片样式
<Tabs type="card" editable onAddTab={handleAdd} onDeleteTab={handleDelete}>
  {tabs.map(tab => (
    <Tabs.TabPane key={tab.key} title={tab.title} closable>
      {tab.content}
    </Tabs.TabPane>
  ))}
</Tabs>

// 胶囊样式
<Tabs type="capsule" />

// 圆角样式
<Tabs type="rounded" />
```

## TabsProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `activeTab` / `defaultActiveTab` | `string` | — | 当前标签 |
| `type` | `'line' \| 'card' \| 'card-gutter' \| 'text' \| 'rounded' \| 'capsule'` | `'line'` | 样式 |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | 方向 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `tabPosition` | `'top' \| 'right' \| 'bottom' \| 'left'` | `'top'` | 标签位置 |
| `editable` | `boolean` | — | 可增删 |
| `showAddButton` | `boolean` | `true` | 显示新增按钮 |
| `extra` | `ReactNode` | — | 右侧附加内容 |
| `destroyOnHide` | `boolean` | — | 切换时销毁 |
| `lazyload` | `boolean` | `true` | 延迟渲染 |
| `animation` | `boolean` | — | 切换动画 |
| `overflow` | `'scroll' \| 'dropdown'` | `'scroll'` | 溢出处理 |
| `scrollPosition` | `'start' \| 'end' \| 'center' \| 'auto' \| number` | `'auto'` | 滚动位置 |
| `onChange` | `(key: string) => void` | — | 切换回调 |
| `onAddTab` | `() => void` | — | 新增回调 |
| `onDeleteTab` | `(key: string) => void` | — | 删除回调 |

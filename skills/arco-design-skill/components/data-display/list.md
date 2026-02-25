---
name: arco-list
description: Arco List 列表组件用法与 API。当需要展示通栏列表数据、支持分页加载或虚拟滚动时使用。
user-invocable: false
---

# List 列表

```tsx
import { List } from '@arco-design/web-react';

<List
  header="列表标题"
  dataSource={['项目1', '项目2', '项目3']}
  render={(item, index) => <List.Item key={index}>{item}</List.Item>}
/>

// 带分页
<List
  dataSource={data}
  pagination={{ pageSize: 10 }}
  render={(item) => (
    <List.Item key={item.id} actions={[<Button>编辑</Button>]}>
      <List.Item.Meta avatar={<Avatar />} title={item.title} description={item.desc} />
    </List.Item>
  )}
/>

// 栅格列表
<List grid={{ gutter: 16, span: 6 }} dataSource={data} render={...} />

// 虚拟滚动
<List virtualListProps={{ height: 400 }} dataSource={bigData} render={...} />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `dataSource` | `any[]` | 数据源 |
| `render` | `(item, index) => ReactNode` | 渲染函数 |
| `header` / `footer` | `ReactNode` | 头部/底部 |
| `size` | `'small' \| 'default' \| 'large'` | 尺寸 |
| `bordered` | `boolean` | 边框 |
| `split` | `boolean` | 分割线 |
| `loading` | `boolean` | 加载中 |
| `hoverable` | `boolean` | 可悬停 |
| `pagination` | `PaginationProps \| boolean` | 分页 |
| `grid` | `{ gutter, span, xs, sm, ... }` | 栅格布局 |
| `virtualListProps` | `VirtualListProps` | 虚拟滚动 |
| `scrollLoading` | `ReactNode` | 滚动加载 |
| `onReachBottom` | `() => void` | 触底回调 |

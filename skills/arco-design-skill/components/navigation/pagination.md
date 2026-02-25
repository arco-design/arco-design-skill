---
name: arco-pagination
description: Arco Pagination 分页组件用法与 API。当需要单独使用分页器或自定义分页样式时使用。
user-invocable: false
---

# Pagination 分页

```tsx
import { Pagination } from '@arco-design/web-react';

<Pagination total={200} />
<Pagination total={200} showTotal showJumper showPageSize sizeCanChange />
<Pagination total={200} size="small" simple />
```

## PaginationProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `total` | `number` | — | 总条数 |
| `current` / `defaultCurrent` | `number` | `1` | 当前页 |
| `pageSize` / `defaultPageSize` | `number` | `10` | 每页条数 |
| `pageSizeChangeResetCurrent` | `boolean` | `true` | 改变每页条数时重置到第一页 |
| `showTotal` | `boolean \| ((total, range) => ReactNode)` | — | 显示总数 |
| `showJumper` | `boolean` | — | 快速跳转 |
| `showMore` | `boolean` | — | 显示更多 |
| `sizeCanChange` | `boolean` | `true` | 可改变每页条数 |
| `sizeOptions` | `number[]` | `[10,20,30,40,50]` | 每页条数选项 |
| `simple` | `boolean` | — | 简洁模式 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `disabled` | `boolean` | — | 禁用 |
| `hideOnSinglePage` | `boolean` | — | 单页隐藏 |
| `itemRender` | `(page, type, originElement) => ReactNode` | — | 自定义页码 |
| `onChange` | `(pageNumber, pageSize) => void` | — | 页码变化 |
| `onPageSizeChange` | `(size, current) => void` | — | 每页条数变化 |

## 常用模式

```tsx
// 受控分页
const [current, setCurrent] = useState(1);
<Pagination current={current} total={200} pageSize={20} onChange={setCurrent} />

// 带尺寸切换
<Pagination
  total={500}
  showTotal
  sizeCanChange
  sizeOptions={[10, 20, 50, 100]}
  onPageSizeChange={(size) => setPageSize(size)}
/>

// 简洁模式
<Pagination simple total={100} />

// 迷你模式（紧凑场景）
<Pagination size="mini" total={100} showTotal showJumper />

// 自定义总数展示
<Pagination total={1000} showTotal={(total, range) => `第 ${range[0]}-${range[1]} 条，共 ${total} 条`} />
```

## 最佳实践

1. **Table 自带 pagination** —— 一般无需单独使用，直接配置 Table 的 pagination 属性
2. **showTotal 告知总量** —— 让用户了解数据规模
3. **sizeCanChange 给用户选择权** —— 不同用户偏好不同的每页条数
4. **simple 模式适合移动端** —— 减少占用空间

---
name: arco-empty
description: Arco Empty 空状态组件用法与 API。当数据为空时需要展示占位图和提示文字时使用。
user-invocable: false
---

# Empty 空状态

当数据为空时的占位展示。

```tsx
import { Empty } from '@arco-design/web-react';

<Empty />
<Empty description="暂无数据" />
<Empty icon={<IconFile />} description="没有文件" />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `icon` | `ReactNode` | 自定义图标 |
| `description` | `ReactNode` | 描述文字 |
| `imgSrc` | `string` | 自定义图片地址 |

## 常用模式

```tsx
// 自定义空状态
<Empty
  icon={<img src="/custom-empty.svg" style={{ width: 120 }} />}
  description="暂无搜索结果"
/>

// 嵌入在 Table 或 List 中
<Table
  columns={columns}
  data={[]}
  noDataElement={<Empty description="暂无数据" />}
/>

// 带操作按钮
<Empty description="还没有项目">
  <Button type="primary" icon={<IconPlus />}>创建项目</Button>
</Empty>
```

## 最佳实践

1. **自定义图片优于图标** —— 在品牌化产品中使用自定义插画代替默认图标
2. **提供明确的下一步操作** —— 空状态应告诉用户可以做什么
3. **不同场景使用不同描述** —— 搜索无结果、列表为空、权限不足应使用不同文案

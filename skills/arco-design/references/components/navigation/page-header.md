---
name: arco-page-header
description: "Arco Design PageHeader component API. Use for page titles with back button, breadcrumb, subtitle, and action buttons."
user-invocable: false
---

# PageHeader 页头

```tsx
import { PageHeader, Button } from '@arco-design/web-react';

<PageHeader
  title="页面标题"
  subTitle="副标题"
  breadcrumb={{
    routes: [
      { path: '/', breadcrumbName: '首页' },
      { path: '/list', breadcrumbName: '列表' },
      { breadcrumbName: '详情' },
    ],
  }}
  extra={<Button type="primary">操作</Button>}
>
  页面内容描述
</PageHeader>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `title` | `ReactNode` | 标题 |
| `subTitle` | `ReactNode` | 副标题 |
| `breadcrumb` | `BreadcrumbProps` | 面包屑配置 |
| `extra` | `ReactNode` | 右侧操作区 |
| `backIcon` | `ReactNode \| boolean` | 返回图标 |
| `onBack` | `(e) => void` | 返回回调 |
| `footer` | `ReactNode` | 底部内容 |

## 常用模式

```tsx
// 带面包屑的页头
<PageHeader
  title="详情页"
  subTitle="订单 #20240101"
  breadcrumb={{
    routes: [
      { path: '/', breadcrumbName: '首页' },
      { path: '/orders', breadcrumbName: '订单列表' },
      { breadcrumbName: '订单详情' },
    ],
  }}
  extra={<Button type="primary">编辑</Button>}
  onBack={() => navigate(-1)}
/>

// 带内容区域
<PageHeader title="页面标题" onBack={() => navigate(-1)}>
  <Descriptions
    column={3}
    data={[
      { label: '创建人', value: '张三' },
      { label: '创建时间', value: '2024-01-01' },
      { label: '状态', value: <Badge status="success" text="已完成" /> },
    ]}
  />
</PageHeader>
```

## 最佳实践

1. **onBack 结合路由** —— 使用 `navigate(-1)` 或 `navigate('/list')` 实现返回
2. **extra 放操作按钮** —— 如编辑、删除、导出等
3. **children 放页面元数据** —— 配合 Descriptions 展示关键信息

---
name: arco-descriptions
description: Arco Descriptions 描述列表组件用法与 API。当需要展示键值对描述信息（如详情页）时使用。
user-invocable: false
---

# Descriptions 描述列表

```tsx
import { Descriptions } from '@arco-design/web-react';

<Descriptions
  title="用户信息"
  data={[
    { label: '姓名', value: '张三' },
    { label: '手机号', value: '188****8888' },
    { label: '住址', value: '北京市朝阳区' },
    { label: '备注', value: '无' },
  ]}
  column={2}
/>
```

## DescriptionsProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `data` | `{ label, value, span? }[]` | — | 描述数据 |
| `title` | `ReactNode` | — | 标题 |
| `column` | `number \| ResponsiveValue` | `3` | 每行列数 |
| `layout` | `'horizontal' \| 'vertical' \| 'inline-horizontal' \| 'inline-vertical'` | `'horizontal'` | 布局 |
| `size` | `'mini' \| 'small' \| 'medium' \| 'default' \| 'large'` | — | 尺寸 |
| `border` | `boolean` | — | 边框 |
| `colon` | `ReactNode` | — | 冒号 |
| `labelStyle` / `valueStyle` | `CSSProperties` | — | 标签/值样式 |

## 常用模式

```tsx
// 详情页展示
<Descriptions title="用户信息" border column={2}>
  <Descriptions.Item label="姓名">张三</Descriptions.Item>
  <Descriptions.Item label="手机号">138****0000</Descriptions.Item>
  <Descriptions.Item label="邮箱">zhangsan@example.com</Descriptions.Item>
  <Descriptions.Item label="地址" span={2}>北京市朝阳区 xxx 路 xx 号</Descriptions.Item>
</Descriptions>

// 垂直布局
<Descriptions layout="vertical" column={3}>
  <Descriptions.Item label="创建时间">2024-01-01</Descriptions.Item>
  <Descriptions.Item label="更新时间">2024-06-15</Descriptions.Item>
  <Descriptions.Item label="状态"><Badge status="success" text="已上线" /></Descriptions.Item>
</Descriptions>

// 响应式列数
<Descriptions column={{ xs: 1, sm: 2, md: 3 }} border>
  ...
</Descriptions>
```

## 最佳实践

1. **详情页首选 Descriptions** —— 比手写 div 更规范
2. **长文本用 span 跨列** —— 地址、备注等可设置 `span={2}` 或 `span={3}`
3. **配合 border 属性** —— 有边框更易阅读

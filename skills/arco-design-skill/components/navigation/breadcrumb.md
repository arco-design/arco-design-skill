---
name: arco-breadcrumb
description: Arco Breadcrumb 面包屑组件用法与 API。当需要展示页面导航层级路径时使用。
user-invocable: false
---

# Breadcrumb 面包屑

```tsx
import { Breadcrumb } from '@arco-design/web-react';

<Breadcrumb>
  <Breadcrumb.Item>首页</Breadcrumb.Item>
  <Breadcrumb.Item href="/list">列表</Breadcrumb.Item>
  <Breadcrumb.Item>详情</Breadcrumb.Item>
</Breadcrumb>

// 自定义分隔符
<Breadcrumb separator=">" />

// 下拉菜单
<Breadcrumb.Item droplist={<Menu><Menu.Item>选项</Menu.Item></Menu>}>
  分类
</Breadcrumb.Item>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `separator` | `ReactNode` | 自定义分隔符 |
| `maxCount` | `number` | 最多显示的面包屑数量 |
| `routes` | `{ path, breadcrumbName }[]` | 通过配置生成 |

### Breadcrumb.Item

| 属性 | 类型 | 说明 |
|------|------|------|
| `href` | `string` | 链接地址 |
| `droplist` | `ReactNode` | 下拉菜单 |
| `onClick` | `(e) => void` | 点击回调 |

## 常用模式

```tsx
// 配合路由
<Breadcrumb>
  <Breadcrumb.Item><Link href="/">首页</Link></Breadcrumb.Item>
  <Breadcrumb.Item><Link href="/products">产品</Link></Breadcrumb.Item>
  <Breadcrumb.Item>详情</Breadcrumb.Item>
</Breadcrumb>

// 通过 routes 配置
<Breadcrumb
  routes={[
    { path: '/', breadcrumbName: '首页' },
    { path: '/category', breadcrumbName: '分类' },
    { breadcrumbName: '当前页' },
  ]}
/>

// 带下拉菜单
<Breadcrumb>
  <Breadcrumb.Item>首页</Breadcrumb.Item>
  <Breadcrumb.Item droplist={
    <Menu>
      <Menu.Item key="1">选项一</Menu.Item>
      <Menu.Item key="2">选项二</Menu.Item>
    </Menu>
  }>
    分类
  </Breadcrumb.Item>
  <Breadcrumb.Item>详情</Breadcrumb.Item>
</Breadcrumb>

// 自定义分隔符
<Breadcrumb separator={<IconRight />}>
  <Breadcrumb.Item>Level 1</Breadcrumb.Item>
  <Breadcrumb.Item>Level 2</Breadcrumb.Item>
</Breadcrumb>
```

## 最佳实践

1. **最后一项不要加链接** —— 当前页面不需要可点击
2. **配合 PageHeader 使用** —— PageHeader 有 breadcrumb 属性
3. **层级不宜过深** —— 一般 2-4 层即可

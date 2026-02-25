---
name: arco-layout
description: Arco Layout 页面布局组件用法与 API。当需要构建 Header/Sider/Content/Footer 页面级布局框架时使用。
user-invocable: false
---

# Layout 布局

页面级别的布局框架，提供 Header、Sider、Content、Footer 四个区域。

## 基本用法

```tsx
import { Layout } from '@arco-design/web-react';
const { Header, Sider, Content, Footer } = Layout;

<Layout>
  <Header>Header</Header>
  <Layout>
    <Sider>Sider</Sider>
    <Content>Content</Content>
  </Layout>
  <Footer>Footer</Footer>
</Layout>
```

## API

### Layout Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `hasSider` | `boolean` | — | 是否有侧边栏（自动检测） |

### Sider Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `collapsed` | `boolean` | — | 是否收起（受控） |
| `defaultCollapsed` | `boolean` | — | 默认收起 |
| `collapsible` | `boolean` | — | 是否可收起 |
| `onCollapse` | `(collapsed: boolean, type: 'clickTrigger' \| 'responsive') => void` | — | 收起回调 |
| `collapsedWidth` | `number` | `48` | 收起后宽度 |
| `width` | `number \| string` | `200` | 展开时宽度 |
| `trigger` | `ReactNode \| null` | — | 自定义触发器，null 隐藏 |
| `breakpoint` | `'xxl' \| 'xl' \| 'lg' \| 'md' \| 'sm' \| 'xs'` | — | 响应式断点自动收起 |
| `onBreakpoint` | `(broken: boolean) => void` | — | 断点变化回调 |
| `resizeDirections` | `string[]` | — | 可拖拽调整方向 |

## 常见布局

```tsx
// 上-中(侧边+内容)-下
<Layout>
  <Header style={{ height: 64 }}>顶部导航</Header>
  <Layout>
    <Sider width={220} collapsible breakpoint="lg">
      <Menu />
    </Sider>
    <Content style={{ padding: '24px' }}>
      主体内容
    </Content>
  </Layout>
  <Footer>Footer</Footer>
</Layout>

// 侧边固定 + 右侧滚动
<Layout style={{ height: '100vh' }}>
  <Sider width={220} style={{ position: 'fixed', left: 0, height: '100%' }}>
    <Menu />
  </Sider>
  <Layout style={{ marginLeft: 220 }}>
    <Header>Header</Header>
    <Content style={{ padding: 24, overflow: 'auto' }}>
      Content
    </Content>
  </Layout>
</Layout>
```

## 最佳实践

1. **使用 `breakpoint` 实现响应式侧边栏** 自动收起
2. **`collapsedWidth={0}`** 可以完全隐藏侧边栏
3. **设置 `trigger={null}`** 后自行实现收起按钮获得更好的控制
4. **搭配 Menu 组件** 使用，Menu 会自动响应 Sider 的收起状态

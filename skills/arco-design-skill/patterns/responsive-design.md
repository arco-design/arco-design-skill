---
name: arco-responsive-design
description: Arco Design 响应式设计指南。当需要使用 Grid 断点实现响应式布局或自适应页面时使用。
user-invocable: false
---

# 响应式设计

## Grid 栅格系统

### 基础断点

Arco Design Grid 支持 5 个响应式断点：

| 断点 | 最小宽度 | 说明 |
|------|----------|------|
| `xs` | < 576px | 超小屏/手机 |
| `sm` | ≥ 576px | 小屏/平板竖屏 |
| `md` | ≥ 768px | 中屏/平板横屏 |
| `lg` | ≥ 992px | 大屏/笔记本 |
| `xl` | ≥ 1200px | 超大屏/桌面 |
| `xxl` | ≥ 1600px | 宽屏显示器 |

### 响应式列宽

```tsx
import { Grid } from '@arco-design/web-react';
const { Row, Col } = Grid;

// 基础响应式 - 不同屏幕宽度不同列数
<Row gutter={24}>
  <Col xs={24} sm={12} md={8} lg={6}>
    <div>响应式列</div>
  </Col>
  <Col xs={24} sm={12} md={8} lg={6}>
    <div>响应式列</div>
  </Col>
  <Col xs={24} sm={12} md={8} lg={6}>
    <div>响应式列</div>
  </Col>
  <Col xs={24} sm={12} md={8} lg={6}>
    <div>响应式列</div>
  </Col>
</Row>
```

### 响应式对象写法

同时控制 span 和 offset：

```tsx
<Col
  xs={{ span: 24 }}
  sm={{ span: 12 }}
  md={{ span: 8, offset: 2 }}
  lg={{ span: 6, offset: 0 }}
>
  内容
</Col>
```

### 响应式间距

Row 的 gutter 也支持响应式：

```tsx
// 对象写法
<Row gutter={{ xs: 8, sm: 16, md: 24, lg: 32 }}>
  <Col span={12}>...</Col>
  <Col span={12}>...</Col>
</Row>

// 数组形式 [水平, 垂直]
<Row gutter={[24, 16]}>
  <Col span={8}>...</Col>
  <Col span={8}>...</Col>
  <Col span={8}>...</Col>
</Row>
```

## Layout 侧边栏响应式

### Sider 断点自动收缩

```tsx
import { Layout } from '@arco-design/web-react';
const { Sider, Content } = Layout;

<Layout>
  <Sider
    breakpoint="lg"       // 在 lg 断点时自动折叠
    collapsedWidth={60}   // 折叠后宽度
    onBreakpoint={(broken) => {
      console.log('breakpoint:', broken);
    }}
    onCollapse={(collapsed) => {
      console.log('collapsed:', collapsed);
    }}
  >
    <Menu>...</Menu>
  </Sider>
  <Content>...</Content>
</Layout>
```

### 手动控制 Sider 折叠

```tsx
const [collapsed, setCollapsed] = useState(false);

<Sider
  collapsed={collapsed}
  onCollapse={setCollapsed}
  collapsible
  width={220}
  collapsedWidth={60}
>
  <Menu collapse={collapsed}>...</Menu>
</Sider>
```

## Space 响应式

Space 的 size 支持响应式数组：

```tsx
// [水平间距, 垂直间距]
<Space size={[16, 8]} wrap>
  <Tag>标签1</Tag>
  <Tag>标签2</Tag>
  <Tag>标签3</Tag>
</Space>
```

## 常见响应式布局模板

### 管理后台布局

```tsx
const AdminLayout = () => {
  const [collapsed, setCollapsed] = useState(false);

  return (
    <Layout style={{ height: '100vh' }}>
      <Sider
        collapsed={collapsed}
        onCollapse={setCollapsed}
        collapsible
        breakpoint="md"
        width={220}
        collapsedWidth={60}
      >
        <Menu collapse={collapsed} defaultSelectedKeys={['1']}>
          <Menu.Item key="1">首页</Menu.Item>
          <Menu.Item key="2">设置</Menu.Item>
        </Menu>
      </Sider>
      <Layout>
        <Layout.Header style={{ height: 60, padding: '0 16px' }}>
          Header
        </Layout.Header>
        <Layout.Content style={{ padding: 16 }}>
          Content
        </Layout.Content>
      </Layout>
    </Layout>
  );
};
```

### 响应式卡片网格

```tsx
const CardGrid = ({ items }) => (
  <Row gutter={[16, 16]}>
    {items.map((item) => (
      <Col key={item.id} xs={24} sm={12} md={8} lg={6} xl={4}>
        <Card title={item.title}>
          {item.content}
        </Card>
      </Col>
    ))}
  </Row>
);
```

### 响应式表单布局

```tsx
// 小屏单列，大屏多列
<Form layout="horizontal">
  <Row gutter={24}>
    <Col xs={24} md={12}>
      <Form.Item label="姓名" field="name">
        <Input />
      </Form.Item>
    </Col>
    <Col xs={24} md={12}>
      <Form.Item label="邮箱" field="email">
        <Input />
      </Form.Item>
    </Col>
    <Col xs={24} md={8}>
      <Form.Item label="城市" field="city">
        <Select />
      </Form.Item>
    </Col>
    <Col xs={24} md={8}>
      <Form.Item label="区域" field="district">
        <Select />
      </Form.Item>
    </Col>
    <Col xs={24} md={8}>
      <Form.Item label="邮编" field="zip">
        <Input />
      </Form.Item>
    </Col>
  </Row>
</Form>
```

### Descriptions 响应式列数

```tsx
<Descriptions
  column={{ xs: 1, sm: 2, md: 3 }}
  data={[
    { label: '姓名', value: '张三' },
    { label: '年龄', value: '28' },
    { label: '城市', value: '北京' },
  ]}
/>
```

## 自定义媒体查询

结合 CSS 自定义属性实现更精细的响应式控制：

```css
/* 自定义响应式变量 */
:root {
  --page-padding: 16px;
}

@media (min-width: 768px) {
  :root {
    --page-padding: 24px;
  }
}

@media (min-width: 1200px) {
  :root {
    --page-padding: 32px;
  }
}
```

```tsx
<div style={{ padding: 'var(--page-padding)' }}>
  <Row gutter={24}>
    ...
  </Row>
</div>
```

## 最佳实践

1. **优先使用 Grid 栅格** — 而非手动媒体查询
2. **24 栅格映射** — xs=24 (全宽), sm=12 (半宽), md=8 (三等分), lg=6 (四等分)
3. **Sider 设置 breakpoint** — 小屏自动折叠侧边栏
4. **gutter 使用对象** — 不同断点不同间距
5. **Descriptions 响应式 column** — 小屏单列展示

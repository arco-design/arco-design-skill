---
name: arco-grid
description: Arco Grid 栅格布局组件用法与 API。当需要使用 Row/Col 24 栅格系统进行页面布局、响应式断点适配时使用。
user-invocable: false
---

# Grid 栅格

基于 24 栅格系统的响应式布局组件。

## 基本用法

```tsx
import { Grid } from '@arco-design/web-react';
const { Row, Col } = Grid;

<Row gutter={24}>
  <Col span={12}>col-12</Col>
  <Col span={12}>col-12</Col>
</Row>

<Row gutter={24}>
  <Col span={8}>col-8</Col>
  <Col span={8}>col-8</Col>
  <Col span={8}>col-8</Col>
</Row>

<Row gutter={24}>
  <Col span={6}>col-6</Col>
  <Col span={6}>col-6</Col>
  <Col span={6}>col-6</Col>
  <Col span={6}>col-6</Col>
</Row>
```

## API

### Row Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `gutter` | `number \| [number, number] \| ResponsiveValue` | `0` | 栅格间距，[水平, 垂直] |
| `justify` | `'start' \| 'center' \| 'end' \| 'space-between' \| 'space-around' \| 'space-evenly'` | `'start'` | 水平对齐 |
| `align` | `'start' \| 'center' \| 'end' \| 'stretch'` | `'start'` | 垂直对齐 |
| `wrap` | `boolean` | `true` | 是否自动换行 |
| `div` | `boolean` | — | 使用 div 替代 flex 行为 |

### Col Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `span` | `number` | `24` | 占据栅格数（0-24） |
| `offset` | `number` | — | 左侧偏移栅格数 |
| `order` | `number` | — | 排序 |
| `push` | `number` | — | 向右推 |
| `pull` | `number` | — | 向左拉 |
| `flex` | `number \| string \| 'auto' \| 'none'` | — | flex 布局属性 |
| `xs` | `number \| { span, offset }` | — | < 576px 响应 |
| `sm` | `number \| { span, offset }` | — | ≥ 576px 响应 |
| `md` | `number \| { span, offset }` | — | ≥ 768px 响应 |
| `lg` | `number \| { span, offset }` | — | ≥ 992px 响应 |
| `xl` | `number \| { span, offset }` | — | ≥ 1200px 响应 |
| `xxl` | `number \| { span, offset }` | — | ≥ 1600px 响应 |
| `xxxl` | `number \| { span, offset }` | — | ≥ 2000px 响应 |

## 响应式布局

```tsx
<Row gutter={[24, 16]}>
  <Col xs={24} sm={12} md={8} lg={6}>
    响应式列
  </Col>
  <Col xs={24} sm={12} md={8} lg={6}>
    响应式列
  </Col>
  <Col xs={24} sm={12} md={8} lg={6}>
    响应式列
  </Col>
  <Col xs={24} sm={12} md={8} lg={6}>
    响应式列
  </Col>
</Row>

{/* 响应式间距 */}
<Row gutter={{ xs: 8, sm: 16, md: 24 }}>
  <Col span={12}>col</Col>
  <Col span={12}>col</Col>
</Row>
```

## 常用布局模式

```tsx
// 左右布局
<Row>
  <Col flex="200px">固定宽度</Col>
  <Col flex="auto">自适应宽度</Col>
</Row>

// 居中对齐
<Row justify="center" align="center" style={{ height: 200 }}>
  <Col span={6}>居中内容</Col>
</Row>

// 等分布局
<Row justify="space-between">
  <Col span={4}>左</Col>
  <Col span={4}>中</Col>
  <Col span={4}>右</Col>
</Row>
```

### 断点说明

| 断点 | 最小宽度 | 典型设备 |
|------|---------|---------|
| `xs` | 0px | 手机竖屏 |
| `sm` | 576px | 手机横屏 |
| `md` | 768px | 平板 |
| `lg` | 992px | 小型桌面 |
| `xl` | 1200px | 桌面 |
| `xxl` | 1600px | 大桌面 |
| `xxxl` | 2000px | 超大屏 |

## 最佳实践

1. **始终设置 `gutter`**，避免列之间没有间距
2. **使用响应式属性** 替代媒体查询，保持代码简洁
3. **`flex` 属性用于不等宽布局**，比 `span` 更灵活
4. **嵌套栅格**时注意内层 `Row` 也需要设置 `gutter`

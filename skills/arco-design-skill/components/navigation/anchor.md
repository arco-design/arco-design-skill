---
name: arco-anchor
description: Arco Anchor 锚点组件用法与 API。当需要实现页面内锚点导航、滚动定位或目录导航时使用。
user-invocable: false
---

# Anchor 锚点

```tsx
import { Anchor } from '@arco-design/web-react';

<Anchor>
  <Anchor.Link href="#section1" title="章节一" />
  <Anchor.Link href="#section2" title="章节二">
    <Anchor.Link href="#section2-1" title="子章节" />
  </Anchor.Link>
  <Anchor.Link href="#section3" title="章节三" />
</Anchor>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `affix` | `boolean` | 是否固定 |
| `offsetTop` | `number` | 固定偏移 |
| `boundary` | `number \| 'start' \| 'center' \| 'end' \| 'nearest'` | 滚动边界 |
| `lineless` | `boolean` | 无左侧线 |
| `scrollContainer` | `string \| HTMLElement \| Window` | 滚动容器 |
| `onChange` | `(newLink, oldLink) => void` | 锚点变化 |

## 常用模式

```tsx
// 固定在页面右侧的目录导航
<div style={{ display: 'flex' }}>
  <div style={{ flex: 1 }}>
    <div id="section1">章节一内容...</div>
    <div id="section2">章节二内容...</div>
    <div id="section3">章节三内容...</div>
  </div>
  <Anchor affix offsetTop={80} style={{ width: 200 }}>
    <Anchor.Link href="#section1" title="章节一" />
    <Anchor.Link href="#section2" title="章节二">
      <Anchor.Link href="#section2-1" title="子章节 2.1" />
    </Anchor.Link>
    <Anchor.Link href="#section3" title="章节三" />
  </Anchor>
</div>

// 水平锚点
<Anchor direction="horizontal">
  <Anchor.Link href="#basic" title="基础" />
  <Anchor.Link href="#advanced" title="进阶" />
  <Anchor.Link href="#api" title="API" />
</Anchor>
```

## 完整 API

### AnchorProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `affix` | `boolean` | `true` | 是否固定 |
| `offsetTop` | `number` | — | 固定时顶部偏移 |
| `direction` | `'vertical' \| 'horizontal'` | `'vertical'` | 方向 |
| `boundary` | `number \| 'start' \| 'center' \| 'end' \| 'nearest'` | `'start'` | 滚动边界 |
| `lineless` | `boolean` | — | 无左侧竖线 |
| `scrollContainer` | `string \| HTMLElement \| Window` | — | 滚动容器 |
| `targetOffset` | `number` | — | 锚点滚动偏移量 |
| `hash` | `boolean` | `true` | 是否改变 URL hash |
| `onChange` | `(newLink, oldLink) => void` | — | 锚点变化回调 |
| `onSelect` | `(newLink, oldLink) => void` | — | 点击锚点回调 |

### Anchor.Link Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `href` | `string` | 锚点链接 |
| `title` | `ReactNode` | 锚点标题 |

## 最佳实践

1. **配合 Affix 使用** —— `affix` 属性使锚点导航固定在页面侧边
2. **offsetTop 要与固定导航栏配合** —— 避免锚点被导航栏遮挡
3. **文档类页面必备** —— 长文档页面右侧放锚点导航提升体验

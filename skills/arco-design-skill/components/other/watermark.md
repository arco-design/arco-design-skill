---
name: arco-watermark
description: Arco Watermark 水印组件用法与 API。当需要给页面或区域添加水印时使用。
user-invocable: false
---

# Watermark 水印

```tsx
import { Watermark } from '@arco-design/web-react';

<Watermark content="Arco Design">
  <div style={{ height: 300 }}>被水印覆盖的内容</div>
</Watermark>

// 图片水印
<Watermark image="logo.png" width={120} height={40}>
  <div>内容</div>
</Watermark>

// 多行水印
<Watermark content={['Arco Design', '字节跳动']}>
  <div>内容</div>
</Watermark>
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `content` | `string \| string[]` | — | 水印文字 |
| `image` | `string` | — | 图片水印 |
| `width` | `number` | — | 水印宽度 |
| `height` | `number` | — | 水印高度 |
| `gap` | `[number, number]` | `[100, 100]` | 间距 |
| `offset` | `[number, number]` | — | 偏移 |
| `rotate` | `number` | `-30` | 旋转角度 |
| `fontStyle` | `{ color, fontSize, fontFamily, fontWeight }` | — | 字体样式 |
| `zIndex` | `number` | — | 层级 |
| `getContainer` | `() => HTMLElement` | — | 渲染容器 |

> 也可使用 `useWatermark` Hook 实现无头水印，见 [Hooks 参考](../../hooks/hooks.md)。

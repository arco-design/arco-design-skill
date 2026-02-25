---
name: arco-back-top
description: Arco BackTop 回到顶部组件用法与 API。当需要长页面快速回到顶部的按钮时使用。
user-invocable: false
---

# BackTop 回到顶部

```tsx
import { BackTop } from '@arco-design/web-react';

<BackTop />
<BackTop visibleHeight={200} duration={500} />

// 自定义
<BackTop>
  <div style={{ width: 40, height: 40, background: '#165DFF', borderRadius: '50%', display: 'flex', alignItems: 'center', justifyContent: 'center', color: '#fff' }}>
    UP
  </div>
</BackTop>
```

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `visibleHeight` | `number` | `400` | 出现的滚动高度 |
| `target` | `() => HTMLElement` | `() => window` | 滚动容器 |
| `duration` | `number` | `400` | 滚动时长 ms |
| `onClick` | `() => void` | — | 点击回调 |

## 常用模式

```tsx
// 在指定容器中使用
<div id="scrollContainer" style={{ height: 300, overflow: 'auto' }}>
  {/* 长内容 */}
  <BackTop target={() => document.getElementById('scrollContainer')} />
</div>

// 自定义样式
<BackTop>
  <div className="custom-back-top">
    <IconArrowUp />
  </div>
</BackTop>
```

## 完整 API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `visibleHeight` | `number` | `400` | 滚动多少后出现 |
| `target` | `() => HTMLElement \| Window` | `() => window` | 滚动容器 |
| `duration` | `number` | `400` | 滚动回顶部的时长 ms |
| `easing` | `string` | `'quartOut'` | 滚动动画曲线 |
| `onClick` | `() => void` | — | 点击回调 |

## 最佳实践

1. **长列表页面必备** —— 页面内容超过 2 屏时应添加 BackTop
2. **自定义容器要设 target** —— 非 window 滚动时必须指定容器
3. **visibleHeight 不要太小** —— 避免刚开始滚动就出现

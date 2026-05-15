---
name: arco-carousel
description: "Arco Design Carousel component API. Use for image carousels, slideshows, and card carousel displays."
user-invocable: false
---

# Carousel 走马灯

```tsx
import { Carousel } from '@arco-design/web-react';

<Carousel autoPlay style={{ width: 600, height: 300 }}>
  <div><img src="/1.jpg" /></div>
  <div><img src="/2.jpg" /></div>
  <div><img src="/3.jpg" /></div>
</Carousel>
```

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `currentIndex` | `number` | `0` | 当前页（受控） |
| `autoPlay` | `boolean \| { interval, hoverToPause }` | — | 自动播放 |
| `animation` | `'slide' \| 'card' \| 'fade'` | `'slide'` | 切换动画 |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | 方向 |
| `showArrow` | `'always' \| 'hover' \| 'never'` | `'always'` | 箭头 |
| `indicatorType` | `'line' \| 'dot' \| 'slider' \| 'never'` | `'dot'` | 指示器 |
| `indicatorPosition` | `'bottom' \| 'top' \| 'left' \| 'right' \| 'outer'` | `'bottom'` | 指示器位置 |
| `miniRender` | `boolean` | — | 最小化渲染（仅渲染可见，2.21.0） |
| `moveSpeed` | `number` | `500` | 切换动画时长 ms |
| `timingFunc` | `string` | `'cubic-bezier(0.34, 0.69, 0.1, 1)'` | 过渡曲线（transition-timing-function） |
| `trigger` | `'click' \| 'hover'` | `'click'` | 指示器触发方式 |
| `icons` | `{ prev?: ReactNode; next?: ReactNode }` | — | 自定义箭头图标（2.25.0） |
| `arrowClassName` | `string \| string[]` | — | 箭头 class |
| `indicatorClassName` | `string \| string[]` | — | 指示器 class |
| `carousel` | `MutableRefObject<CarouselHandle>` | — | 命令式 API ref，提供 `goto({ index, isNegative?, isManual?, resetAutoPlayInterval? })`（2.16.1） |
| `onChange` | `(index, prevIndex, isManual) => void` | — | 切换回调（`isManual` 2.4.0） |

## 常用模式

```tsx
// 带自动播放的图片轮播
<Carousel autoPlay={{ interval: 3000, hoverToPause: true }} style={{ width: '100%', height: 400 }}>
  {images.map((src, i) => (
    <div key={i}><img src={src} style={{ width: '100%', height: '100%', objectFit: 'cover' }} /></div>
  ))}
</Carousel>

// 卡片模式
<Carousel animation="card" style={{ width: 600, height: 300 }}>
  {cards.map(card => <div key={card.id}>{card.content}</div>)}
</Carousel>

// Ref 控制翻页
const carouselRef = useRef();
<Carousel ref={carouselRef}>...</Carousel>
<Button onClick={() => carouselRef.current.goto({ index: 0 })}>回到第一页</Button>
```

## 最佳实践

1. **设置固定高度** —— Carousel 需要明确的宽高才能正常展示
2. **图片使用 objectFit: cover** —— 确保图片不变形
3. **miniRender 提升性能** —— 大量子元素时仅渲染可见项
4. **hoverToPause 提升可用性** —— 鼠标悬停时暂停自动播放

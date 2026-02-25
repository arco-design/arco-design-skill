---
name: arco-affix
description: Arco Affix 固钉组件用法与 API。当需要将元素固定在页面可视范围的特定位置时使用。
user-invocable: false
---

# Affix 固钉

```tsx
import { Affix, Button } from '@arco-design/web-react';

<Affix offsetTop={80}>
  <Button type="primary">固定在顶部 80px</Button>
</Affix>

<Affix offsetBottom={20}>
  <Button type="primary">固定在底部 20px</Button>
</Affix>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `offsetTop` | `number` | 距顶部距离 |
| `offsetBottom` | `number` | 距底部距离 |
| `target` | `() => HTMLElement` | 滚动容器 |
| `onChange` | `(affixed: boolean) => void` | 固钉状态变化 |

## 常用模式

```tsx
// 固定在页面顶部（如工具栏）
<Affix offsetTop={0}>
  <div className="toolbar" style={{ background: '#fff', padding: 16 }}>
    <Button type="primary">保存</Button>
    <Button style={{ marginLeft: 8 }}>取消</Button>
  </div>
</Affix>

// 固定在底部（如操作栏）
<Affix offsetBottom={0}>
  <div className="action-bar">
    <Button type="primary" long>提交</Button>
  </div>
</Affix>

// 在指定滚动容器内固定
<Affix target={() => document.getElementById('scroll-container')} offsetTop={10}>
  <Button>固定在容器内</Button>
</Affix>
```

## 完整 API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `offsetTop` | `number` | `0` | 距窗口顶部固定距离 |
| `offsetBottom` | `number` | — | 距窗口底部固定距离 |
| `target` | `() => HTMLElement \| Window` | `() => window` | 滚动容器 |
| `targetContainer` | `() => HTMLElement \| Window` | — | 目标容器（计算偏移的参考） |
| `affixClassName` | `string` | — | 固定状态的类名 |
| `affixStyle` | `CSSProperties` | — | 固定状态的样式 |
| `onChange` | `(affixed: boolean) => void` | — | 固钉状态变化回调 |

## 最佳实践

1. **始终设置背景色** —— 固定元素应有背景色，避免与下方内容重叠
2. **注意 z-index 层级** —— 固定元素可能需要较高的 z-index
3. **offsetTop 要考虑已有固定元素** —— 如页面已有固定导航栏高度 64px，则 offsetTop 应设为 64

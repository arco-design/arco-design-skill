---
name: arco-portal
description: Arco Portal 传送门组件用法与 API。当需要将子节点渲染到指定 DOM 节点时使用。
user-invocable: false
---

# Portal 传送门

将子节点渲染到指定 DOM 节点。

```tsx
import { Portal } from '@arco-design/web-react';

<Portal getContainer={() => document.getElementById('target')}>
  <div>被传送的内容</div>
</Portal>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `getContainer` | `() => Element` | 目标容器 |

## 常用模式

```tsx
// 渲染到 body（默认行为）
<Portal>
  <div className="my-overlay">弹出层内容</div>
</Portal>

// 渲染到指定容器
<Portal getContainer={() => document.getElementById('modal-root')}>
  <div>渲染到 #modal-root 下</div>
</Portal>

// 配合 forceRender 使用
<Portal forceRender visible={visible}>
  <MyComponent />
</Portal>
```

## 完整 API

| 属性 | 类型 | 说明 |
|------|------|------|
| `getContainer` | `() => Element` | 目标容器，默认 document.body |
| `forceRender` | `boolean` | 强制渲染（不论 visible） |
| `visible` | `boolean` | 是否可见 |
| `children` | `ReactNode` | 子节点 |

## 最佳实践

1. **Portal 是大多数弹出组件的底层** —— Modal、Drawer、Tooltip 内部都使用了 Portal
2. **指定 getContainer 时注意 DOM 生命周期** —— 确保目标容器在 Portal 渲染前已存在
3. **一般无需直接使用** —— 除非需要自定义弹出层行为，否则使用 Modal/Drawer/Trigger 即可

---
name: arco-spin
description: Arco Spin 加载中组件用法与 API。当需要展示全局或局部的加载中状态时使用。
user-invocable: false
---

# Spin 加载中

```tsx
import { Spin } from '@arco-design/web-react';

<Spin />
<Spin size={40} />

// 包裹内容
<Spin loading={loading} tip="加载中...">
  <div>被加载内容包裹的区域</div>
</Spin>

// 自定义图标
<Spin icon={<IconLoading />} />

// 全局点状加载
<Spin dot />
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `loading` | `boolean` | — | 是否加载中 |
| `size` | `number` | — | 大小 |
| `icon` | `ReactNode` | — | 自定义图标 |
| `element` | `ReactNode` | — | 自定义元素 |
| `tip` | `string \| ReactNode` | — | 提示文字 |
| `dot` | `boolean` | — | 点状加载 |
| `delay` | `number` | — | 延迟显示（避免闪烁） |
| `block` | `boolean` | — | 块级展示 |

## 最佳实践

- **使用 `delay` 避免短暂加载闪烁**（推荐 200-500ms）
- **包裹内容区域** 而非全局使用
- **`dot` 模式** 适用于更轻量的加载指示

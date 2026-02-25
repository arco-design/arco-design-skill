---
name: arco-progress
description: Arco Progress 进度条组件用法与 API。当需要展示操作进度、线性进度条或环形进度时使用。
user-invocable: false
---

# Progress 进度条

```tsx
import { Progress } from '@arco-design/web-react';

<Progress percent={30} />
<Progress percent={70} status="success" />
<Progress percent={50} status="error" />
<Progress type="circle" percent={75} />
<Progress type="circle" percent={100} status="success" />
<Progress size="small" percent={50} />

// 自定义颜色
<Progress percent={50} color="#165DFF" />

// 步骤进度
<Progress percent={60} steps={5} />
```

### ProgressProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `percent` | `number` | `0` | 百分比 |
| `type` | `'line' \| 'circle'` | `'line'` | 类型 |
| `status` | `'success' \| 'error' \| 'normal' \| 'warning'` | — | 状态 |
| `size` | `'small' \| 'default' \| 'mini' \| 'large'` | `'default'` | 尺寸 |
| `color` | `string \| Record<string, string>` | — | 颜色（渐变） |
| `trailColor` | `string` | — | 轨道颜色 |
| `showText` | `boolean` | `true` | 显示文字 |
| `formatText` | `(percent) => ReactNode` | — | 自定义文字 |
| `steps` | `number` | — | 步骤数 |
| `strokeWidth` | `number` | — | 线宽 |
| `width` | `number \| string` | — | 圆形进度条宽度 |
| `animation` | `boolean` | — | 动画效果 |
| `buffer` | `boolean` | — | 缓冲动画 |


## 最佳实践

- **展示有明确百分比的操作**（上传、导入等）
- **`type="circle"`** 适合卡片内的进度展示
- **`steps`** 适合步骤进度

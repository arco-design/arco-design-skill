---
name: arco-statistic
description: Arco Statistic 数值显示组件用法与 API。当需要展示统计数值、倒计时或带趋势的数据时使用。
user-invocable: false
---

# Statistic 数值显示

```tsx
import { Statistic } from '@arco-design/web-react';

<Statistic title="活跃用户" value={1128} />
<Statistic title="增长率" value={50.5} suffix="%" precision={1} />
<Statistic.Countdown title="倒计时" value={Date.now() + 1000 * 60 * 60} />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `title` | `ReactNode` | 标题 |
| `value` | `number \| string \| Dayjs \| Date` | 数值 |
| `precision` | `number` | 小数精度 |
| `prefix` | `ReactNode` | 前缀 |
| `suffix` | `ReactNode` | 后缀 |
| `groupSeparator` | `boolean` | 千位分隔符 |
| `loading` | `boolean` | 加载中 |
| `countUp` | `boolean` | 数字动画 |
| `countDuration` | `number` | 动画时长 ms |
| `countFrom` | `number` | 动画起始值 |
| `styleValue` | `CSSProperties` | 值样式 |
| `renderFormat` | `(value) => ReactNode` | 自定义渲染 |

### Statistic.Countdown

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `number \| string \| Date \| Dayjs` | 目标时间 |
| `format` | `string` | 格式（默认 `HH:mm:ss`） |
| `start` | `boolean` | 是否开始 |
| `now` | `number \| string \| Date \| Dayjs` | 当前时间 |
| `onFinish` | `() => void` | 倒计时结束回调 |
| `onChange` | `(value) => void` | 变化回调 |

---
name: arco-time-picker
description: Arco TimePicker 时间选择组件用法与 API。当需要选择时间、时间范围或自定义时间格式时使用。
user-invocable: false
---

# TimePicker 时间选择器

选择时间的组件。

## 基本用法

```tsx
import { TimePicker } from '@arco-design/web-react';

<TimePicker style={{ width: 200 }} />
<TimePicker format="HH:mm" style={{ width: 150 }} />
<TimePicker.RangePicker style={{ width: 280 }} />
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `Dayjs \| string` | — | 受控值 |
| `defaultValue` | `Dayjs \| string` | — | 默认值 |
| `format` | `string` | `'HH:mm:ss'` | 时间格式 |
| `use12Hours` | `boolean` | — | 12 小时制 |
| `step` | `{ hour, minute, second }` | — | 各列步长 |
| `disableConfirm` | `boolean` | — | 选择即确认 |
| `disabled` | `boolean` | — | 禁用 |
| `allowClear` | `boolean` | `true` | 可清除 |
| `placeholder` | `string` | — | 占位文字 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `showNowBtn` | `boolean` | `true` | 显示"此刻"按钮 |
| `onChange` | `(timeString, time) => void` | — | 值变化 |

## 常用模式

```tsx
// 基本使用
<TimePicker placeholder="选择时间" />

// 范围选择
<TimePicker.RangePicker placeholder={['开始时间', '结束时间']} />

// 12 小时制
<TimePicker use12Hours format="hh:mm A" />

// 步长控制（每 15 分钟）
<TimePicker step={{ minute: 15 }} />

// 禁用部分时间
<TimePicker
  disabledHours={() => [0, 1, 2, 3, 4, 5, 22, 23]}
  disabledMinutes={(hour) => hour === 6 ? [0, 15] : []}
/>

// 受控
const [time, setTime] = useState('09:00');
<TimePicker value={time} onChange={(_, timeString) => setTime(timeString)} />
```

## 最佳实践

1. **format 与 use12Hours 配合** —— 12 小时制用 `hh:mm A`，24 小时制用 `HH:mm`
2. **step 限制可选项** —— 预约场景用 15/30 分钟步长减少选择成本
3. **disabledHours/Minutes 限制营业时间** —— 如工作时间 9:00-18:00

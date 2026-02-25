---
name: arco-input-number
description: Arco InputNumber 数字输入组件用法与 API。当需要数字输入、步进器、精度控制或范围限制时使用。
user-invocable: false
---

# InputNumber 数字输入框

数字输入组件，支持步长、精度、范围限制。

## 基本用法

```tsx
import { InputNumber } from '@arco-design/web-react';

<InputNumber defaultValue={10} style={{ width: 160 }} />
<InputNumber min={0} max={100} step={5} />
<InputNumber precision={2} step={0.1} />
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number \| undefined` | — | 受控值 |
| `defaultValue` | `number` | — | 默认值 |
| `min` | `number` | `-Infinity` | 最小值 |
| `max` | `number` | `Infinity` | 最大值 |
| `step` | `number` | `1` | 步长 |
| `precision` | `number` | — | 小数精度 |
| `disabled` | `boolean` | — | 禁用 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `mode` | `'embed' \| 'button'` | `'embed'` | 模式（嵌入式/按钮式） |
| `prefix` | `ReactNode` | — | 前缀 |
| `suffix` | `ReactNode` | — | 后缀 |
| `formatter` | `(value) => string` | — | 显示格式化 |
| `parser` | `(value) => number` | — | 解析格式化后的值 |
| `strictMode` | `boolean` | — | 严格模式（输入过程中也限制范围） |
| `onChange` | `(value: number) => void` | — | 值变化 |

## 常用模式

```tsx
// 金额输入
<InputNumber
  prefix="¥"
  precision={2}
  min={0}
  formatter={(value) => `${value}`.replace(/\B(?=(\d{3})+(?!\d))/g, ',')}
  parser={(value) => value.replace(/,/g, '')}
/>

// 百分比
<InputNumber suffix="%" min={0} max={100} step={1} />

// 按钮模式
<InputNumber mode="button" defaultValue={5} min={1} max={10} />
```



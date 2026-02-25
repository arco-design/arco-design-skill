---
name: arco-slider
description: Arco Slider 滑动输入条组件用法与 API。当需要范围选择、刻度标记或垂直滑动条时使用。
user-invocable: false
---

# Slider 滑动输入条

```tsx
import { Slider } from '@arco-design/web-react';

<Slider defaultValue={30} />
<Slider range defaultValue={[20, 60]} />
<Slider marks={{ 0: '0°C', 25: '25°C', 50: '50°C', 100: '100°C' }} />
<Slider step={10} showTicks />
<Slider vertical style={{ height: 200 }} />
```

## SliderProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number \| [number, number]` | — | 受控值 |
| `defaultValue` | `number \| [number, number]` | — | 默认值 |
| `min` | `number` | `0` | 最小值 |
| `max` | `number` | `100` | 最大值 |
| `step` | `number` | `1` | 步长 |
| `range` | `boolean` | — | 范围选择 |
| `vertical` | `boolean` | — | 垂直方向 |
| `marks` | `Record<number, ReactNode>` | — | 刻度标记 |
| `showTicks` | `boolean` | — | 显示刻度 |
| `showInput` | `boolean` | — | 显示输入框 |
| `disabled` | `boolean` | — | 禁用 |
| `reverse` | `boolean` | — | 反向 |
| `tooltipVisible` | `boolean` | — | 提示是否一直显示 |
| `formatTooltip` | `(value: number) => ReactNode` | — | 提示格式化 |
| `onChange` | `(value) => void` | — | 值变化（松开后） |
| `onAfterChange` | `(value) => void` | — | 拖拽结束回调 |

## 常用模式

```tsx
// 范围选择
<Slider range defaultValue={[20, 80]} />

// 带刻度标记
<Slider marks={{ 0: '0°C', 25: '25°C', 50: '50°C', 75: '75°C', 100: '100°C' }} defaultValue={25} />

// 步长
<Slider step={10} showTicks defaultValue={30} />

// 垂直方向
<Slider vertical style={{ height: 200 }} defaultValue={50} />

// 受控 + 格式化提示
const [value, setValue] = useState(50);
<Slider value={value} onChange={setValue} formatTooltip={(val) => `${val}%`} />

// 配合 InputNumber 联动
<Space>
  <Slider value={value} onChange={setValue} style={{ width: 200 }} />
  <InputNumber value={value} onChange={setValue} style={{ width: 80 }} />
</Space>
```

## 最佳实践

1. **range 用于区间选择** —— 如价格区间、日期范围等
2. **marks 标记关键刻度** —— 帮助用户理解值的含义
3. **配合 InputNumber 使用** —— 精确输入 + 滑动调节双重操作
4. **formatTooltip 加单位** —— 显示 "50%" 比显示 "50" 更清晰

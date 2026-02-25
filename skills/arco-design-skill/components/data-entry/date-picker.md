---
name: arco-date-picker
description: Arco DatePicker 日期选择组件用法与 API。当需要选择日期、日期范围、周、月、季度、年或自定义日期面板时使用。
user-invocable: false
---

# DatePicker 日期选择器

日期/时间选择组件，支持日期、周、月、季度、年选择及范围选择。

## 基本用法

```tsx
import { DatePicker } from '@arco-design/web-react';
const { RangePicker, MonthPicker, YearPicker, QuarterPicker, WeekPicker } = DatePicker;

// 日期选择
<DatePicker style={{ width: 200 }} />

// 日期时间选择
<DatePicker showTime style={{ width: 240 }} />

// 范围选择
<RangePicker style={{ width: 300 }} />

// 月份选择
<MonthPicker />

// 年份选择
<YearPicker />

// 季度选择
<QuarterPicker />

// 周选择
<WeekPicker />
```

## API

### 共享 Props (PickerProps)

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `disabled` | `boolean` | — | 禁用 |
| `allowClear` | `boolean` | `true` | 可清除 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `placeholder` | `string` | — | 占位文字 |
| `position` | `'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br'` | — | 弹出位置 |
| `error` | `boolean` | — | 错误状态 |
| `status` | `'error' \| 'warning'` | — | 状态 |
| `editable` | `boolean` | `true` | 允许手动输入 |
| `format` | `string \| ((value: Dayjs) => string)` | — | 日期格式 |
| `shortcuts` | `ShortcutType[]` | — | 快捷选择 |
| `shortcutsPlacementLeft` | `boolean` | — | 快捷选项放左侧 |
| `disabledDate` | `(current: Dayjs) => boolean` | — | 禁用日期 |
| `utcOffset` | `number` | — | UTC 偏移 |
| `timezone` | `string` | — | 时区 |
| `onChange` | `(dateString: string, date: Dayjs) => void` | — | 日期变化 |
| `onSelect` | `(dateString: string, date: Dayjs) => void` | — | 选中回调 |
| `onVisibleChange` | `(visible: boolean) => void` | — | 弹出可见性 |
| `onOk` | `(dateString: string, date: Dayjs) => void` | — | 确认回调 |
| `dateRender` | `(currentDate: Dayjs) => ReactNode` | — | 自定义日期单元格 |
| `panelRender` | `(panelNode: ReactNode) => ReactNode` | — | 自定义面板 |
| `triggerElement` | `ReactNode \| null` | — | 自定义触发元素 |
| `getPopupContainer` | `(node: HTMLElement) => Element` | — | 弹出层容器 |

### DatePicker 专属 Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `Dayjs \| string \| number` | 受控值 |
| `defaultValue` | `Dayjs \| string \| number` | 默认值 |
| `showTime` | `boolean \| TimePickerProps` | 显示时间选择 |
| `timepickerProps` | `TimePickerProps` | 时间选择器配置 |
| `showNowBtn` | `boolean` | 显示"此刻"按钮 |
| `defaultPickerValue` | `Dayjs \| string \| number` | 面板默认日期 |

### RangePicker 专属 Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `Dayjs[]` | 受控值 [开始, 结束] |
| `mode` | `'date' \| 'month' \| 'year' \| 'week' \| 'quarter'` | 选择模式 |
| `showTime` | `boolean \| TimePickerRangeProps` | 显示时间选择 |
| `disabledTime` | `(date, type) => DisabledTimeProps` | 禁用时间 |

## 常用模式

### 快捷选择

```tsx
import dayjs from 'dayjs';

<DatePicker
  shortcuts={[
    { text: '今天', value: () => dayjs() },
    { text: '昨天', value: () => dayjs().subtract(1, 'day') },
    { text: '一周前', value: () => dayjs().subtract(1, 'week') },
  ]}
/>

<RangePicker
  shortcuts={[
    { text: '最近7天', value: () => [dayjs().subtract(7, 'day'), dayjs()] },
    { text: '最近30天', value: () => [dayjs().subtract(30, 'day'), dayjs()] },
    { text: '本月', value: () => [dayjs().startOf('month'), dayjs().endOf('month')] },
  ]}
/>
```

### 禁用日期

```tsx
// 禁止选择今天之前的日期
<DatePicker disabledDate={(current) => current.isBefore(dayjs(), 'day')} />

// 只允许选择工作日
<DatePicker disabledDate={(current) => [0, 6].includes(current.day())} />

// 范围限制：开始日期不能晚于结束日期
<RangePicker disabledDate={(current) => current.isAfter(dayjs().add(30, 'day'))} />
```

### 日期时间组合

```tsx
<DatePicker
  showTime={{
    defaultValue: '09:00:00',
    format: 'HH:mm:ss',
  }}
  format="YYYY-MM-DD HH:mm:ss"
/>
```

### 自定义日期格式

```tsx
// 使用函数自定义格式
<DatePicker format={(value) => `${value.format('YYYY')}年${value.format('MM')}月${value.format('DD')}日`} />

// 预设格式
<DatePicker format="YYYY/MM/DD" />
<MonthPicker format="YYYY年MM月" />
```

## 最佳实践

1. **日期库使用 `dayjs`**，Arco Design 原生支持
2. **使用 `shortcuts` 提供常用快捷选项**，减少用户操作
3. **`disabledDate` 限制可选范围**，在 UI 层阻止无效选择
4. **`showTime` 场景建议增加 `onOk` 确认**，避免频繁触发 onChange
5. **RangePicker 场景使用 `disabledDate` 联动**禁用开始/结束范围
6. **时区场景使用 `utcOffset` 或 `timezone`**，而非手动转换

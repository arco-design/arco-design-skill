---
name: arco-calendar
description: Arco Calendar 日历组件用法与 API。当需要展示日历视图或在日历上标注事件时使用。
user-invocable: false
---

# Calendar 日历

```tsx
import { Calendar } from '@arco-design/web-react';

<Calendar />
<Calendar panel defaultValue="2024-01-01" />  {/* 面板模式 */}
<Calendar mode="year" />                       {/* 年视图 */}
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` / `defaultValue` | `Dayjs` | 当前日期 |
| `mode` | `'month' \| 'year'` | 视图模式 |
| `panel` | `boolean` | 面板模式（无切换按钮） |
| `panelWidth` | `number` | 面板宽度 |
| `dayStartOfWeek` | `0 \| 1` | 周起始日 |
| `dateRender` | `(date) => ReactNode` | 自定义日期渲染 |
| `dateInnerContent` | `(date) => ReactNode` | 日期内容 |
| `disabledDate` | `(date) => boolean` | 禁用日期 |
| `onChange` | `(date) => void` | 日期变化 |
| `onPanelChange` | `(date) => void` | 面板变化 |

## 常用模式

```tsx
// 带事件标记的日历
<Calendar
  dateRender={(date) => {
    const events = getEventsForDate(date);
    return (
      <div className="calendar-cell">
        <div className="date">{date.date()}</div>
        {events.map(e => (
          <Badge key={e.id} status={e.status} text={e.title} />
        ))}
      </div>
    );
  }}
/>

// 受控日历
const [value, setValue] = useState(dayjs());
<Calendar value={value} onChange={setValue} />

// 面板选择器（嵌入表单等场景）
<Calendar panel panelWidth={280} />
```

## 最佳实践

1. **dateRender 和 dateInnerContent 的区别** —— dateRender 替换整个单元格，dateInnerContent 只在单元格内追加内容
2. **panel 模式用于内嵌场景** —— 隐藏头部切换按钮，适合嵌入卡片或弹窗
3. **注意日期库是 dayjs** —— value 接收 Dayjs 对象

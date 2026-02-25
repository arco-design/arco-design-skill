---
name: arco-switch
description: Arco Switch 开关组件用法与 API。当需要切换开关状态、带文字或图标的开关时使用。
user-invocable: false
---

# Switch 开关

```tsx
import { Switch } from '@arco-design/web-react';

<Switch />
<Switch defaultChecked />
<Switch type="round" />  {/* 圆形 */}
<Switch type="line" />   {/* 线性 */}
<Switch checkedText="ON" uncheckedText="OFF" />
<Switch loading />
```

### SwitchProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `checked` | `boolean` | — | 受控选中 |
| `defaultChecked` | `boolean` | — | 默认选中 |
| `type` | `'circle' \| 'round' \| 'line'` | `'circle'` | 类型 |
| `size` | `'small' \| 'default'` | `'default'` | 尺寸 |
| `loading` | `boolean` | — | 加载中 |
| `disabled` | `boolean` | — | 禁用 |
| `checkedText` | `ReactNode` | — | 选中时文字 |
| `uncheckedText` | `ReactNode` | — | 未选中时文字 |
| `checkedIcon` | `ReactNode` | — | 选中时图标 |
| `uncheckedIcon` | `ReactNode` | — | 未选中时图标 |
| `onChange` | `(value: boolean, e: Event) => void` | — | 变化回调 |

> **在 Form 中使用**：设置 `<Form.Item triggerPropName="checked">` 因为 Switch 使用 `checked` 而非 `value`。

## 常用模式

```tsx
// 受控
const [checked, setChecked] = useState(false);
<Switch checked={checked} onChange={setChecked} />

// 带文字
<Switch checkedText="开" uncheckedText="关" />

// 带图标
<Switch checkedIcon={<IconCheck />} uncheckedIcon={<IconClose />} />

// 加载中（异步操作）
const [loading, setLoading] = useState(false);
<Switch loading={loading} onChange={async (val) => {
  setLoading(true);
  await updateSetting(val);
  setLoading(false);
}} />

// 不同尺寸
<Switch size="small" />
<Switch />
<Switch size="small" type="round" />

// 配合 Form
<Form.Item field="enabled" label="启用" triggerPropName="checked">
  <Switch />
</Form.Item>
```

## 最佳实践

1. **Form 中 Switch 需设 `triggerPropName="checked"`** —— Switch 的值属性是 checked 不是 value
2. **异步操作用 loading** —— 切换后等待接口返回时显示 loading
3. **checkedText/uncheckedText 增强语义** —— 让用户明确知道开/关代表什么

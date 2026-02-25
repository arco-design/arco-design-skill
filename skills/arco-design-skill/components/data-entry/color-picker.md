---
name: arco-color-picker
description: Arco ColorPicker 颜色选择器组件用法与 API。当需要选择颜色值时使用。
user-invocable: false
---

# ColorPicker 颜色选择器

```tsx
import { ColorPicker } from '@arco-design/web-react';

<ColorPicker defaultValue="#165DFF" />
<ColorPicker showHistory showPreset />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `string` | 受控颜色值 |
| `defaultValue` | `string` | 默认颜色 |
| `format` | `'hex' \| 'rgb'` | 颜色格式 |
| `showHistory` | `boolean` | 显示历史颜色 |
| `showPreset` | `boolean` | 显示预设颜色 |
| `showText` | `boolean` | 显示颜色文字 |
| `disabled` | `boolean` | 禁用 |
| `disabledAlpha` | `boolean` | 禁用透明度 |
| `onChange` | `(value: string) => void` | 变化回调 |

## 常用模式

```tsx
// 受控使用
const [color, setColor] = useState('#165DFF');
<ColorPicker value={color} onChange={setColor} />

// 显示颜色文字
<ColorPicker showText defaultValue="#165DFF" />

// 禁用透明度
<ColorPicker disabledAlpha defaultValue="#165DFF" />

// 带预设和历史
<ColorPicker
  showPreset
  showHistory
  presetColors={['#165DFF', '#0FC6C2', '#FF7D00', '#F53F3F']}
/>

// 配合 Form 使用
<Form.Item field="brandColor" label="品牌色">
  <ColorPicker showText />
</Form.Item>
```

## 完整 API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` / `defaultValue` | `string` | — | 颜色值 |
| `format` | `'hex' \| 'rgb'` | `'hex'` | 颜色格式 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `showText` | `boolean` | — | 显示颜色文字 |
| `showHistory` | `boolean` | — | 显示历史颜色 |
| `showPreset` | `boolean` | — | 显示预设颜色 |
| `presetColors` | `string[]` | — | 预设颜色列表 |
| `disabled` | `boolean` | — | 禁用 |
| `disabledAlpha` | `boolean` | — | 禁用透明度 |
| `triggerElement` | `ReactNode` | — | 自定义触发元素 |
| `onChange` | `(value: string) => void` | — | 变化回调 |

## 最佳实践

1. **品牌色选择用 disabledAlpha** —— 通常不需要透明度
2. **提供 presetColors** —— 减少用户选择成本
3. **显示 showText** —— 让用户看到精确的颜色值

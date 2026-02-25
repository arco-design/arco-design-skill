---
name: arco-input-tag
description: Arco InputTag 标签输入组件用法与 API。当需要输入并管理标签列表时使用。
user-invocable: false
---

# InputTag 标签输入

输入并管理标签列表。

```tsx
import { InputTag } from '@arco-design/web-react';

<InputTag
  allowClear
  placeholder="输入后按回车添加标签"
  defaultValue={['标签1', '标签2']}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `string[]` | 受控值 |
| `defaultValue` | `string[]` | 默认值 |
| `allowClear` | `boolean` | 可清除 |
| `placeholder` | `string` | 占位文字 |
| `maxTagCount` | `number` | 最多显示标签数 |
| `validate` | `(value, values) => boolean \| Promise` | 标签校验 |
| `onChange` | `(value: string[]) => void` | 变化回调 |
| `onRemove` | `(value: string, index: number) => void` | 删除标签 |
| `onPressEnter` | `(e: Event) => void` | 回车回调 |

## 常用模式

```tsx
// 受控使用
const [tags, setTags] = useState(['React', 'TypeScript']);
<InputTag value={tags} onChange={setTags} allowClear />

// 标签校验
<InputTag
  placeholder="输入标签后按回车"
  validate={(value) => {
    if (value.length > 20) return false;  // 长度限制
    return true;
  }}
/>

// 最大标签数
<InputTag maxTagCount={5} placeholder="最多 5 个标签" />

// 拖拽排序
<InputTag dragToSort defaultValue={['A', 'B', 'C']} />

// 配合 Form 使用
<Form.Item field="tags" label="标签">
  <InputTag allowClear placeholder="输入后回车" />
</Form.Item>
```

## 完整 API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` / `defaultValue` | `string[]` | — | 值 |
| `placeholder` | `string` | — | 占位文字 |
| `allowClear` | `boolean` | — | 可清除全部 |
| `maxTagCount` | `number` | — | 最多显示标签数 |
| `dragToSort` | `boolean` | — | 拖拽排序 |
| `disabled` | `boolean` | — | 禁用 |
| `readOnly` | `boolean` | — | 只读 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `validate` | `(value, values) => boolean \| Promise` | — | 标签校验 |
| `saveOnBlur` | `boolean` | — | 失焦时保存输入 |
| `tokenSeparators` | `string[]` | — | 触发添加的分隔符 |
| `onChange` | `(value: string[], reason) => void` | — | 变化回调 |
| `onRemove` | `(value, index, e) => void` | — | 删除标签 |
| `onPressEnter` | `(e) => void` | — | 回车回调 |
| `onInputChange` | `(inputValue, e) => void` | — | 输入变化 |

## 最佳实践

1. **validate 做去重和格式检查** —— 防止重复标签和无效输入
2. **tokenSeparators 支持粘贴批量添加** —— 如 `[',', '\n']` 支持逗号和换行分隔
3. **maxTagCount 配合 +N 提示** —— 超出部分自动显示 "+N" 标记

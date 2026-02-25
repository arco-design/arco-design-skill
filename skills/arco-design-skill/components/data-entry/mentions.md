---
name: arco-mentions
description: Arco Mentions 提及组件用法与 API。当需要在输入框中 @ 提及用户或话题时使用。
user-invocable: false
---

# Mentions 提及

```tsx
import { Mentions } from '@arco-design/web-react';

<Mentions
  options={['张三', '李四', '王五'].map(name => ({ value: name, label: name }))}
  placeholder="输入 @ 提及用户"
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `prefix` | `string \| string[]` | 触发字符（默认 `@`） |
| `options` | `{ value, label }[]` | 提及选项 |
| `split` | `string` | 分隔符 |
| `onSearch` | `(text, prefix) => void` | 搜索回调 |
| `onChange` | `(value) => void` | 值变化 |

## 常用模式

```tsx
// 受控使用
const [value, setValue] = useState('');
<Mentions value={value} onChange={setValue} options={users} />

// 远程搜索
<Mentions
  prefix="@"
  onSearch={async (text) => {
    const result = await searchUsers(text);
    setOptions(result.map(u => ({ value: u.name, label: u.name })));
  }}
  options={options}
/>

// 多触发字符
<Mentions
  prefix={['@', '#']}
  onSearch={(text, prefix) => {
    if (prefix === '@') loadUsers(text);
    else loadTopics(text);
  }}
  options={options}
/>

// 只读
<Mentions readOnly value="感谢 @张三 的贡献" />
```

## 完整 API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` / `defaultValue` | `string` | — | 值 |
| `prefix` | `string \| string[]` | `'@'` | 触发字符 |
| `options` | `{ value, label }[]` | — | 提及选项 |
| `split` | `string` | `' '` | 选中项前后分隔符 |
| `position` | `'top' \| 'bottom'` | `'bottom'` | 下拉框位置 |
| `disabled` | `boolean` | — | 禁用 |
| `allowClear` | `boolean` | — | 可清除 |
| `rows` | `number` | — | 文本域行数 |
| `onSearch` | `(text, prefix) => void` | — | 搜索回调 |
| `onChange` | `(value) => void` | — | 值变化 |
| `onPressEnter` | `(e) => void` | — | 回车回调 |

## 最佳实践

1. **配合 Form 使用** —— Mentions 可直接放在 Form.Item 中
2. **远程搜索加防抖** —— 使用 lodash.debounce 包装 onSearch
3. **prefix 不要用常见字符** —— 避免用户正常输入时误触发

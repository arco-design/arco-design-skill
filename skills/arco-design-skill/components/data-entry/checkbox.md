---
name: arco-checkbox
description: Arco Checkbox 复选框组件用法与 API。当需要多选操作、全选/半选或复选框组时使用。
user-invocable: false
---

# Checkbox 复选框

```tsx
import { Checkbox } from '@arco-design/web-react';

// 单个
<Checkbox>选项</Checkbox>
<Checkbox defaultChecked>默认选中</Checkbox>
<Checkbox indeterminate>半选</Checkbox>

// 复选框组
<Checkbox.Group
  defaultValue={['A']}
  options={['A', 'B', 'C']}
  onChange={(values) => console.log(values)}
/>

// 垂直排列
<Checkbox.Group direction="vertical" options={['选项A', '选项B', '选项C']} />
```

### CheckboxProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `checked` | `boolean` | — | 受控选中 |
| `defaultChecked` | `boolean` | — | 默认选中 |
| `disabled` | `boolean` | — | 禁用 |
| `indeterminate` | `boolean` | — | 半选状态 |
| `value` | `string \| number` | — | 在 Group 中的值 |
| `onChange` | `(checked: boolean, e: Event) => void` | — | 变化回调 |

### Checkbox.Group Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` / `defaultValue` | `(string \| number)[]` | 选中的值 |
| `options` | `(string \| { label, value, disabled })[]` | 选项列表 |
| `direction` | `'horizontal' \| 'vertical'` | 排列方向 |
| `onChange` | `(values: any[]) => void` | 变化回调 |

### 全选 / 半选

```tsx
const [checkedList, setCheckedList] = useState([]);
const allOptions = ['A', 'B', 'C'];
const indeterminate = checkedList.length > 0 && checkedList.length < allOptions.length;
const checkAll = checkedList.length === allOptions.length;

<Checkbox
  indeterminate={indeterminate}
  checked={checkAll}
  onChange={(checked) => setCheckedList(checked ? allOptions : [])}
>
  全选
</Checkbox>
<Checkbox.Group value={checkedList} onChange={setCheckedList} options={allOptions} />
```



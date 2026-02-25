---
name: arco-cascader
description: Arco Cascader 级联选择组件用法与 API。当需要多层级数据选择（如省市区、分类层级）、远程加载或搜索时使用。
user-invocable: false
---

# Cascader 级联选择

用于多层级数据选择，如省市区、分类等。

## 基本用法

```tsx
import { Cascader } from '@arco-design/web-react';

const options = [
  {
    value: 'beijing',
    label: '北京',
    children: [
      { value: 'chaoyang', label: '朝阳区' },
      { value: 'haidian', label: '海淀区' },
    ],
  },
  {
    value: 'shanghai',
    label: '上海',
    children: [
      { value: 'pudong', label: '浦东新区' },
      { value: 'huangpu', label: '黄浦区' },
    ],
  },
];

<Cascader options={options} placeholder="请选择" style={{ width: 300 }} />
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `(string \| string[])[]` | — | 受控值 |
| `defaultValue` | `(string \| string[])[]` | — | 默认值 |
| `options` | `CascaderOption[]` | `[]` | 级联数据 |
| `mode` | `'multiple'` | — | 多选模式 |
| `changeOnSelect` | `boolean` | — | 选中即改变（非叶子节点也可选） |
| `expandTrigger` | `'click' \| 'hover'` | `'click'` | 展开触发方式 |
| `showSearch` | `boolean \| { filter, render, limit }` | — | 搜索 |
| `loading` | `boolean` | — | 加载中 |
| `allowClear` | `boolean` | — | 可清除 |
| `placeholder` | `string` | — | 占位文字 |
| `loadMore` | `(pathValue, level) => Promise<CascaderOption[]>` | — | 动态加载 |
| `fieldNames` | `{ label, value, children, disabled, isLeaf }` | — | 自定义字段名 |
| `renderFormat` | `(valueShow: string[]) => ReactNode` | — | 自定义显示格式 |
| `onChange` | `(value, selectedOptions, extra) => void` | — | 选中回调 |

### 动态加载

```tsx
<Cascader
  options={options}
  loadMore={(pathValue, level) => {
    return new Promise((resolve) => {
      fetchChildren(pathValue).then((children) => resolve(children));
    });
  }}
/>
```



---
name: arco-cascader
description: "Arco Design Cascader component API. Use for multi-level cascading selection (province/city/district), remote loading, search, and change-on-select."
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
| `icons` | `{ loading?: ReactNode; checked?: ReactNode; next?: ReactNode }` | — | 自定义图标（2.50.0） |
| `dropdownMenuClassName` | `string \| string[]` | — | 下拉菜单 class（2.35.0） |
| `dropdownMenuColumnStyle` | `CSSProperties` | — | 下拉菜单列样式（2.35.0） |
| `virtualListProps` | `Pick<AvailableVirtualListProps, 'height' \| 'itemHeight' \| 'threshold' \| 'isStaticItemHeight'>` | — | 虚拟滚动（2.35.0） |
| `triggerProps` | `Partial<TriggerProps>` | — | 透传给底层 Trigger |
| `getPopupContainer` | `(node) => Element` | — | 弹出容器 |
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



---
name: arco-tree-select
description: Arco TreeSelect 树选择组件用法与 API。当需要从树形结构中选择数据、支持搜索或多选时使用。
user-invocable: false
---

# TreeSelect 树选择

```tsx
import { TreeSelect } from '@arco-design/web-react';

<TreeSelect
  treeData={[
    {
      key: 'node1', title: '节点1',
      children: [
        { key: 'node1-1', title: '节点1-1' },
        { key: 'node1-2', title: '节点1-2' },
      ],
    },
    { key: 'node2', title: '节点2' },
  ]}
  placeholder="请选择"
  style={{ width: 300 }}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `treeData` | `TreeNodeData[]` | 树数据 |
| `value` / `defaultValue` | `string \| string[]` | 选中值 |
| `multiple` | `boolean` | 多选 |
| `treeCheckable` | `boolean` | 复选框模式 |
| `treeCheckStrictly` | `boolean` | 严格父子无关 |
| `showSearch` | `boolean` | 搜索 |
| `allowClear` | `boolean` | 可清除 |
| `loadMore` | `(node) => Promise` | 动态加载 |
| `fieldNames` | `{ key, title, children }` | 字段映射 |
| `onChange` | `(value) => void` | 变化回调 |

## 常用模式

```tsx
// 基本使用
<TreeSelect
  treeData={[
    { key: '1', title: '总部', children: [
      { key: '1-1', title: '技术部' },
      { key: '1-2', title: '产品部' },
    ]},
    { key: '2', title: '分公司' },
  ]}
  placeholder="选择部门"
  style={{ width: 300 }}
/>

// 多选 + 可搜索
<TreeSelect
  treeCheckable
  showSearch
  treeData={treeData}
  placeholder="选择多个"
  maxTagCount={3}
/>

// 受控
const [value, setValue] = useState([]);
<TreeSelect value={value} onChange={setValue} treeData={treeData} treeCheckable />

// 异步加载子节点
<TreeSelect
  treeData={treeData}
  loadMore={(node) => fetchChildren(node.props.dataRef.key).then(updateTreeData)}
/>
```

## 最佳实践

1. **treeCheckable 用于多选** —— 带复选框的树选择
2. **showSearch 配合大数据量** —— 方便用户快速定位
3. **loadMore 做懒加载** —— 大量节点时按需加载子节点
4. **与 Cascader 的区别** —— TreeSelect 展示完整树结构，Cascader 逐级选择

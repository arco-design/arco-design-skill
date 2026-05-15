---
name: arco-tree-select
description: "Arco Design TreeSelect component API. Use for selecting from tree structure data, tree checkboxes, searchable tree, and async node loading."
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
| `treeCheckedStrategy` | `'all' \| 'parent' \| 'child'` | 返回的 checked keys 包含哪些层级 |
| `treeProps` | `Partial<TreeProps>` | 透传给底层 Tree |
| `triggerProps` | `Partial<TriggerProps>` | 透传给底层 Trigger |
| `showSearch` | `boolean \| { retainInputValue?, retainInputValueWhileSelect? }` | 搜索 |
| `filterTreeNode` | `(inputValue, node) => boolean` | 自定义过滤函数 |
| `allowClear` | `boolean` | 可清除 |
| `bordered` | `boolean` | 显示边框（默认 true） |
| `loadMore` | `(node) => Promise` | 动态加载 |
| `fieldNames` | `{ key, title, children }` | 字段映射 |
| `dropdownMenuStyle` | `CSSProperties` | 下拉菜单样式 |
| `dropdownRender` | `(menu: ReactNode) => ReactNode` | 自定义下拉内容 |
| `getPopupContainer` | `(node) => HTMLElement` | 弹出层挂载节点 |
| `onChange` | `(value) => void` | 变化回调 |
| `onInputValueChange` | `(value: string) => void` | 搜索输入变化（2.39.0） |

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

---
name: arco-tree
description: Arco Tree 树形控件组件用法与 API。当需要展示层级结构数据、可勾选树、可拖拽排序或虚拟滚动树时使用。
user-invocable: false
---

# Tree 树

树形控件，用于展示层级结构数据。

## 基本用法

```tsx
import { Tree } from '@arco-design/web-react';

const treeData = [
  {
    key: '0-0',
    title: '节点 0',
    children: [
      { key: '0-0-0', title: '叶子 0-0' },
      { key: '0-0-1', title: '叶子 0-1' },
    ],
  },
  {
    key: '0-1',
    title: '节点 1',
    children: [{ key: '0-1-0', title: '叶子 1-0' }],
  },
];

<Tree treeData={treeData} defaultExpandedKeys={['0-0']} />
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `treeData` | `TreeNodeData[]` | — | 树数据 |
| `checkable` | `boolean` | — | 带复选框 |
| `selectable` | `boolean` | `true` | 可选中 |
| `multiple` | `boolean` | — | 多选 |
| `checkedKeys` / `defaultCheckedKeys` | `string[]` | — | 选中的 key |
| `expandedKeys` / `defaultExpandedKeys` | `string[]` | — | 展开的 key |
| `selectedKeys` / `defaultSelectedKeys` | `string[]` | — | 选中的 key |
| `checkStrictly` | `boolean` | — | 父子不关联 |
| `autoExpandParent` | `boolean` | `true` | 自动展开父节点 |
| `draggable` | `boolean` | — | 可拖拽 |
| `blockNode` | `boolean` | — | 整行选中 |
| `showLine` | `boolean` | — | 显示连接线 |
| `loadMore` | `(node) => Promise` | — | 异步加载 |
| `virtualListProps` | `VirtualListProps` | — | 虚拟滚动 |
| `fieldNames` | `{ key, title, children, isLeaf, disabled, selectable, checkable }` | — | 自定义字段 |
| `renderTitle` | `(node) => ReactNode` | — | 自定义标题 |
| `renderExtra` | `(node) => ReactNode` | — | 自定义额外内容 |
| `icons` | `{ switcherIcon, dragIcon, loadingIcon }` | — | 自定义图标 |
| `onSelect` | `(selectedKeys, extra) => void` | — | 选中回调 |
| `onCheck` | `(checkedKeys, extra) => void` | — | 勾选回调 |
| `onExpand` | `(expandedKeys, extra) => void` | — | 展开回调 |
| `onDrop` | `(info) => void` | — | 拖拽放置 |
| `allowDrop` | `(options) => boolean` | — | 是否允许放置 |

## 常用模式

```tsx
// 可搜索的树
const [searchValue, setSearchValue] = useState('');
const filterTree = (data, keyword) => { /* 递归过滤 */ };

<Input.Search onChange={setSearchValue} />
<Tree treeData={filterTree(treeData, searchValue)} />

// 异步加载子节点
<Tree
  treeData={treeData}
  loadMore={async (node) => {
    const children = await fetchChildren(node.key);
    // 更新 treeData
  }}
/>

// 虚拟滚动
<Tree treeData={bigTreeData} virtualListProps={{ height: 400 }} />

// 拖拽排序
<Tree treeData={treeData} draggable onDrop={handleDrop} />
```

## 最佳实践

1. **大数据量使用 `virtualListProps`** 虚拟滚动
2. **`loadMore` 实现懒加载**，避免一次加载整棵树
3. **`fieldNames` 映射后端数据字段**，无需额外转换
4. **`checkStrictly` 用于独立选择**，不联动父子

---
name: arco-transfer
description: "Arco Design Transfer component API. Use for transferring items between two lists, searchable transfer, simple mode, and custom rendering."
user-invocable: false
---

# Transfer 穿梭框

```tsx
import { Transfer } from '@arco-design/web-react';

<Transfer
  dataSource={[
    { key: '1', value: '选项一' },
    { key: '2', value: '选项二' },
    { key: '3', value: '选项三' },
  ]}
  targetKeys={['1']}
  titleTexts={['源列表', '目标列表']}
  onChange={(newTargetKeys) => setTargetKeys(newTargetKeys)}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `dataSource` | `TransferItem[]` | 数据源 |
| `targetKeys` | `string[]` | 右侧列表 key（受控） |
| `defaultTargetKeys` | `string[]` | 默认右侧 key |
| `selectedKeys` | `string[]` | 左右两边当前选中项 key（受控） |
| `defaultSelectedKeys` | `string[]` | 默认选中项 key |
| `showSearch` | `boolean \| { placeholder? }` | 搜索 |
| `searchPlaceholder` | `string` | 搜索框占位（2.40.0） |
| `showFooter` | `boolean` | 底部 |
| `titleTexts` | `ReactNode[]` | 标题 |
| `operations` | `ReactNode[]` | 自定义中间按钮内容 |
| `operationTexts` | `string[]` | 中间按钮文案 |
| `operationStyle` | `CSSProperties` | 中间按钮样式 |
| `oneWay` | `boolean` | 单向模式（右侧不可移回） |
| `simple` | `boolean \| { retainSelectedItems? }` | 简单模式 |
| `pagination` | `boolean \| PaginationProps` | 分页 |
| `filterOption` | `(inputValue, item) => boolean` | 自定义搜索过滤 |
| `render` | `(item) => ReactNode` | 自定义项渲染 |
| `children` | `(props) => ReactNode` | 完全自定义列表 |
| `onChange` | `(newTargetKeys, direction, moveKeys) => void` | 变化回调 |
| `onSelectChange` | `(sourceSelectedKeys, targetSelectedKeys) => void` | 选中态变化 |
| `onSearch` | `(value, type: 'source' \| 'target') => void` | 搜索回调 |
| `onResetData` | `() => void` | 重置数据回调 |

## 常用模式

```tsx
// 基本使用
<Transfer
  dataSource={allItems.map(item => ({ key: item.id, value: item.name }))}
  targetKeys={selectedKeys}
  onChange={(keys) => setSelectedKeys(keys)}
  titleTexts={['可选', '已选']}
/>

// 带搜索
<Transfer
  showSearch
  dataSource={dataSource}
  targetKeys={targetKeys}
  onChange={setTargetKeys}
/>

// 自定义渲染
<Transfer
  dataSource={users}
  targetKeys={targetKeys}
  onChange={setTargetKeys}
  render={(item) => (
    <div style={{ display: 'flex', alignItems: 'center', gap: 8 }}>
      <Avatar size={24}>{item.value[0]}</Avatar>
      {item.value}
    </div>
  )}
/>

// 简单模式（无穿梭按钮）
<Transfer simple dataSource={dataSource} targetKeys={targetKeys} onChange={setTargetKeys} />
```

## 最佳实践

1. **数据量大时开启 showSearch** —— 方便用户快速查找
2. **titleTexts 说明左右含义** —— 如 ['待选人员', '已选人员']
3. **simple 模式更直觉** —— 点击直接转移，无需先选再穿梭

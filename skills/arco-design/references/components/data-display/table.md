---
name: arco-table
description: "Arco Design Table component full API. Use for data tables with sorting, filtering, pagination, fixed columns/headers, virtual scroll, row selection, expandable rows, tree data, and custom cell rendering."
user-invocable: false
---

# Table 表格

功能强大的表格组件，支持排序、筛选、分页、固定列/表头、虚拟滚动、行展开、行选择等。

## 基本用法

```tsx
import { Table } from '@arco-design/web-react';

const columns = [
  { title: '姓名', dataIndex: 'name' },
  { title: '年龄', dataIndex: 'age', sorter: (a, b) => a.age - b.age },
  { title: '地址', dataIndex: 'address' },
  {
    title: '操作',
    render: (_, record) => (
      <Space>
        <Button type="text" size="small">编辑</Button>
        <Button type="text" status="danger" size="small">删除</Button>
      </Space>
    ),
  },
];

const data = [
  { key: '1', name: '张三', age: 28, address: '北京市朝阳区' },
  { key: '2', name: '李四', age: 32, address: '上海市浦东新区' },
];

<Table columns={columns} data={data} />
```

## API

### TableProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `columns` | `ColumnProps[]` | — | 列配置 |
| `data` | `T[]` | — | 数据源 |
| `rowKey` | `string \| ((record) => string)` | `'key'` | 行唯一标识 |
| `loading` | `boolean \| SpinProps` | — | 加载状态 |
| `border` | `boolean \| { wrapper, cell, headerCell, bodyCell }` | `true` | 边框 |
| `borderCell` | `boolean` | — | 单元格边框 |
| `stripe` | `boolean` | — | 斑马纹 |
| `size` | `'default' \| 'middle' \| 'small' \| 'mini'` | — | 表格尺寸 |
| `noDataElement` | `ReactNode` | — | 无数据展示 |
| `showHeader` | `boolean` | `true` | 显示表头 |
| `showSorterTooltip` | `boolean` | `true` | 排序提示 |
| `onChange` | `(pagination, sorter, filters, extra) => void` | — | 分页/排序/筛选变化。extra 包含 `{ currentData, currentAllData, action }` (currentAllData 自 2.53.0) |
| `rowClassName` | `string \| ((record, index) => string)` | — | 行类名 |
| `onRow` | `(record, index) => HTMLAttributes` | — | 行属性 |
| `onHeaderRow` | `(columns, index) => HTMLAttributes` | — | 表头行属性 |
| `onCell` | `(column, index) => HTMLAttributes` | — | 单元格属性 |
| `tableLayoutFixed` | `boolean` | — | 强制 `table-layout: fixed`（默认有固定列/省略时自动启用） |
| `footer` | `(currentPageData) => ReactNode` | — | 表尾 |
| `summary` | `(currentData) => ReactNode` | — | 总结栏（详见下文 `Table.Summary` 示例） |
| `placeholder` | `ReactNode` | — | 全局空数据占位（优先级低于 `noDataElement`） |
| `childrenColumnName` | `string` | `'children'` | 树形数据子节点字段名 |
| `indentSize` | `number` | `16` | 树形数据缩进像素 |
| `defaultExpandAllRows` | `boolean` | — | 默认展开所有子行 |
| `defaultExpandedRowKeys` | `Array<string \| number>` | — | 默认展开行（非受控） |
| `expandedRowKeys` | `Array<string \| number>` | — | 受控展开行 |
| `expandedRowRender` | `(record, index) => ReactNode` | — | 行展开内容 |
| `expandProps` | `ExpandProps` | — | 行展开高级配置（详见下文）|
| `onExpand` | `(record, expanded) => void` | — | 单行展开回调 |
| `onExpandedRowsChange` | `(expandedRows) => void` | — | 展开行变化回调 |

### 分页 Pagination

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `pagination` | `boolean \| PaginationProps` | — | 分页配置，false 禁用 |
| `pagePosition` | `'tl' \| 'tr' \| 'bl' \| 'br' \| 'topCenter' \| 'bottomCenter'` | `'br'` | 分页位置 |
| `renderPagination` | `(paginationNode: ReactNode) => ReactNode` | — | 自定义分页渲染 |

### 滚动 Scroll

| 属性 | 类型 | 说明 |
|------|------|------|
| `scroll` | `{ x: number \| string \| boolean, y: number \| string }` | 滚动区域 |
| `virtualized` | `boolean` | 虚拟滚动 |
| `virtualListProps` | `VirtualListProps` | 虚拟列表配置 |

### 行选择 RowSelection

`rowSelection` 接收 `RowSelectionProps`：

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `'checkbox' \| 'radio'` | `'checkbox'` | 多选/单选 |
| `selectedRowKeys` | `(string \| number)[]` | — | 受控选中（需配合 `onChange`） |
| `checkAll` | `boolean` | — | 多选模式显示全选 |
| `checkStrictly` | `boolean` | `true` | `false` 时父子选择自动联动（2.33.0） |
| `checkCrossPage` | `boolean` | — | 复选跨分页（非受控；受控需 `preserveSelectedRowKeys`） |
| `columnTitle` | `string \| ReactNode` | — | 选择列表头 |
| `columnWidth` | `number` | — | 选择列宽度 |
| `checkboxProps` | `(record) => object` | — | 复选框属性 |
| `fixed` | `boolean` | — | 固定到左侧 |
| `renderCell` | `(originNode, checked, record) => ReactNode` | — | 自定义复选框（2.19.0） |
| `preserveSelectedRowKeys` | `boolean` | — | 跨页/删除后保留 keys（2.19.0） |
| `onChange` | `(keys, rows) => void` | — | 选中变化 |
| `onSelect` | `(selected, record, selectedRows) => void` | — | 单行选中（2.22.0） |
| `onSelectAll` | `(selected, selectedRows) => void` | — | 全选（2.6.0） |

```tsx
const [selectedRowKeys, setSelectedRowKeys] = useState([]);

<Table
  rowSelection={{
    type: 'checkbox',
    selectedRowKeys,
    onChange: (keys, rows) => setSelectedRowKeys(keys),
    checkboxProps: (record) => ({ disabled: record.disabled }),
    checkAll: true,
    fixed: true,
    columnWidth: 60,
    preserveSelectedRowKeys: true,
    onSelectAll: (selected, selectedRows) => {},
  }}
  columns={columns}
  data={data}
/>
```

### 行展开 Expand

`expandProps` 接收 `ExpandProps`：

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `icon` | `(props: { expanded, record }) => ReactNode` | — | 自定义展开图标 |
| `width` | `number` | — | 展开列宽 |
| `columnTitle` | `ReactNode` | — | 展开列表头 |
| `rowExpandable` | `(record) => boolean` | — | 是否允许展开（2.16.0） |
| `expandRowByClick` | `boolean` | — | 点击行展开（2.19.0） |
| `strictTreeData` | `boolean` | `true` | 树形数据下 children 长度 > 1 才显示展开图标（2.27.0） |

```tsx
<Table
  expandedRowRender={(record) => <p>{record.description}</p>}
  expandProps={{
    expandRowByClick: true,
    rowExpandable: (record) => record.hasDetail,
    icon: (props) => <IconRight />,
    width: 60,
  }}
  columns={columns}
  data={data}
/>
```

### ColumnProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `title` | `ReactNode` | — | 列标题 |
| `dataIndex` | `string` | — | 数据字段名 |
| `key` | `string` | — | 列唯一标识 |
| `width` | `number \| string` | — | 列宽 |
| `align` | `'left' \| 'center' \| 'right'` | `'left'` | 对齐方式 |
| `fixed` | `'left' \| 'right'` | — | 固定列 |
| `ellipsis` | `boolean` | — | 文本省略 |
| `render` | `(col, record, index) => ReactNode` | — | 自定义渲染 |
| `sorter` | `boolean \| ((a, b) => number) \| { compare?: (a, b) => number; multiple?: number }` | — | 排序（`multiple` 用于多列排序优先级） |
| `defaultSortOrder` | `'ascend' \| 'descend'` | — | 默认排序（非受控） |
| `sortOrder` | `'ascend' \| 'descend'` | — | 受控排序值 |
| `sortDirections` | `('ascend' \| 'descend')[]` | — | 排序方向 |
| `filters` | `{ text, value }[]` | — | 筛选菜单 |
| `onFilter` | `(value, record) => boolean` | — | 筛选函数 |
| `filterMultiple` | `boolean` | `true` | 多选筛选 |
| `defaultFilters` | `string[]` | — | 默认筛选值 |
| `filteredValue` | `string[]` | — | 受控筛选值 |
| `filterDropdown` | `(props) => ReactNode` | — | 自定义筛选菜单 |
| `filterIcon` | `ReactNode` | — | 自定义筛选图标 |
| `filterDropdownProps` | `{ triggerProps?: TriggerProps }` | — | 筛选弹窗 Trigger 配置 |
| `onFilterDropdownVisibleChange` | `(visible: boolean) => void` | — | 筛选弹窗显隐回调 |
| `children` | `ColumnProps[]` | — | 多级表头 |
| `onCell` | `(record, index) => HTMLAttributes` | — | 单元格属性 |
| `onHeaderCell` | `(column, index) => HTMLAttributes` | — | 表头单元格属性 |
| `headerCellStyle` | `CSSProperties` | — | 表头单元格样式 |
| `bodyCellStyle` | `CSSProperties` | — | 表体单元格样式 |
| `placeholder` | `ReactNode` | — | 空值占位 |

### Summary 总结栏

```tsx
<Table
  columns={columns}
  data={data}
  summary={(currentData) => (
    <Table.Summary>
      <Table.Summary.Row>
        <Table.Summary.Cell>合计</Table.Summary.Cell>
        <Table.Summary.Cell>
          {currentData.reduce((sum, row) => sum + row.amount, 0)}
        </Table.Summary.Cell>
      </Table.Summary.Row>
    </Table.Summary>
  )}
/>
```

## 常用模式

### 服务端分页排序筛选

```tsx
function ServerTable() {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [pagination, setPagination] = useState({ current: 1, pageSize: 10, total: 0 });

  const fetchData = async (params) => {
    setLoading(true);
    const res = await api.getList(params);
    setData(res.data);
    setPagination(prev => ({ ...prev, total: res.total }));
    setLoading(false);
  };

  useEffect(() => { fetchData({ page: 1, pageSize: 10 }); }, []);

  return (
    <Table
      columns={columns}
      data={data}
      loading={loading}
      pagination={pagination}
      onChange={(pag, sorter, filters) => {
        fetchData({
          page: pag.current,
          pageSize: pag.pageSize,
          sortField: sorter.field,
          sortOrder: sorter.direction,
          ...filters,
        });
      }}
    />
  );
}
```

### 固定列 + 固定表头

```tsx
<Table
  scroll={{ x: 1500, y: 400 }}
  columns={[
    { title: 'ID', dataIndex: 'id', fixed: 'left', width: 80 },
    { title: '名称', dataIndex: 'name', width: 200 },
    // ... 更多列
    { title: '操作', fixed: 'right', width: 120, render: () => <Button>操作</Button> },
  ]}
  data={data}
/>
```

### 虚拟滚动（大数据量）

```tsx
<Table
  virtualized
  scroll={{ y: 500 }}
  columns={columns}
  data={bigData}  // 上万条数据
/>
```

### 可编辑单元格

```tsx
const EditableCell = ({ value, onChange }) => {
  const [editing, setEditing] = useState(false);
  return editing ? (
    <Input value={value} onChange={onChange} onBlur={() => setEditing(false)} autoFocus />
  ) : (
    <span onClick={() => setEditing(true)}>{value}</span>
  );
};

const columns = [{
  title: '名称',
  dataIndex: 'name',
  render: (col, record) => (
    <EditableCell value={col} onChange={(v) => updateRecord(record.key, 'name', v)} />
  ),
}];
```

### 多级表头

```tsx
const columns = [{
  title: '基本信息',
  children: [
    { title: '姓名', dataIndex: 'name' },
    { title: '年龄', dataIndex: 'age' },
  ],
}, {
  title: '联系方式',
  children: [
    { title: '电话', dataIndex: 'phone' },
    { title: '邮箱', dataIndex: 'email' },
  ],
}];
```

### TableInstance (Ref)

```tsx
const tableRef = useRef<TableInstance>(null);
tableRef.current.scrollIntoView('rowKey');  // 滚动到指定行
```

## 最佳实践

1. **始终设置 `rowKey`**，确保行唯一性
2. **固定列必须设置 `width`**，且搭配 `scroll.x`
3. **大数据量用 `virtualized`**，搭配固定 `scroll.y`
4. **服务端场景在 `onChange` 中统一处理**分页、排序、筛选
5. **`preserveSelectedRowKeys`** 在分页场景保持跨页选中
6. **使用 `ellipsis` 处理长文本**列，避免撑破布局
7. **性能优化**：避免在 `render` 中创建新的函数或对象引用

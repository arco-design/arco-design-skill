---
name: arco-table-patterns
description: Arco Design 表格常见模式与最佳实践。当需要实现远程数据加载、可编辑表格、虚拟滚动大数据表或自定义筛选时使用。
user-invocable: false
---

# 表格模式

Arco Design Table 组件的常见使用模式。

## 服务端分页 + 排序 + 筛选

```tsx
function ServerTable() {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [pagination, setPagination] = useState({ current: 1, pageSize: 10, total: 0 });
  const [sorter, setSorter] = useState({});
  const [filters, setFilters] = useState({});

  const fetchData = useCallback(async () => {
    setLoading(true);
    const res = await api.getList({
      page: pagination.current,
      pageSize: pagination.pageSize,
      sortField: sorter.field,
      sortOrder: sorter.direction,
      ...filters,
    });
    setData(res.data);
    setPagination(prev => ({ ...prev, total: res.total }));
    setLoading(false);
  }, [pagination.current, pagination.pageSize, sorter, filters]);

  useEffect(() => { fetchData(); }, [fetchData]);

  const columns = [
    {
      title: '名称',
      dataIndex: 'name',
      sorter: true,  // 服务端排序只需 true，不传排序函数
      filters: [
        { text: '类型A', value: 'A' },
        { text: '类型B', value: 'B' },
      ],
      onFilter: undefined,  // 不传则走服务端筛选
    },
    { title: '金额', dataIndex: 'amount', sorter: true },
    { title: '日期', dataIndex: 'date' },
  ];

  return (
    <Table
      columns={columns}
      data={data}
      loading={loading}
      pagination={{
        ...pagination,
        showTotal: true,
        showJumper: true,
        sizeCanChange: true,
      }}
      onChange={(pag, sorterInfo, filtersInfo) => {
        setPagination({ ...pagination, current: pag.current, pageSize: pag.pageSize });
        setSorter(sorterInfo);
        setFilters(filtersInfo);
      }}
    />
  );
}
```

## 行选择 + 批量操作

```tsx
function SelectableTable() {
  const [selectedRowKeys, setSelectedRowKeys] = useState([]);

  return (
    <div>
      {selectedRowKeys.length > 0 && (
        <Alert
          content={`已选择 ${selectedRowKeys.length} 项`}
          closable
          action={
            <Space>
              <Button size="small" onClick={() => batchDelete(selectedRowKeys)}>批量删除</Button>
              <Button size="small" onClick={() => setSelectedRowKeys([])}>取消选择</Button>
            </Space>
          }
        />
      )}
      <Table
        columns={columns}
        data={data}
        rowSelection={{
          type: 'checkbox',
          selectedRowKeys,
          onChange: (keys) => setSelectedRowKeys(keys),
          preserveSelectedRowKeys: true,  // 跨页保持选中
          checkboxProps: (record) => ({
            disabled: record.status === 'locked',
          }),
        }}
      />
    </div>
  );
}
```

## 可展开行

```tsx
<Table
  columns={columns}
  data={data}
  expandedRowRender={(record) => (
    <Descriptions
      column={3}
      data={[
        { label: '创建时间', value: record.createdAt },
        { label: '更新时间', value: record.updatedAt },
        { label: '备注', value: record.remark },
      ]}
    />
  )}
  expandProps={{
    expandRowByClick: true,
    rowExpandable: (record) => record.hasDetail,
  }}
/>
```

## 固定列 + 固定表头

```tsx
<Table
  scroll={{ x: 1600, y: 500 }}
  columns={[
    { title: 'ID', dataIndex: 'id', fixed: 'left', width: 80 },
    { title: '名称', dataIndex: 'name', fixed: 'left', width: 150 },
    { title: '字段1', dataIndex: 'field1', width: 200 },
    { title: '字段2', dataIndex: 'field2', width: 200 },
    { title: '字段3', dataIndex: 'field3', width: 200 },
    { title: '字段4', dataIndex: 'field4', width: 200 },
    { title: '字段5', dataIndex: 'field5', width: 200 },
    {
      title: '操作',
      fixed: 'right',
      width: 120,
      render: (_, record) => <Button type="text" size="small">编辑</Button>,
    },
  ]}
  data={data}
/>
```

## 虚拟滚动（万级数据）

```tsx
<Table
  virtualized
  scroll={{ y: 500 }}
  columns={columns}
  data={bigData}  // 10000+ 行
  rowKey="id"
/>
```

## 可编辑表格

```tsx
function EditableTable() {
  const [data, setData] = useState(initialData);

  const handleSave = (rowKey, field, value) => {
    setData(prev => prev.map(row =>
      row.key === rowKey ? { ...row, [field]: value } : row
    ));
  };

  const columns = [
    {
      title: '名称',
      dataIndex: 'name',
      editable: true,
      render: (col, record) => (
        <EditableCell
          value={col}
          onSave={(value) => handleSave(record.key, 'name', value)}
        />
      ),
    },
    {
      title: '金额',
      dataIndex: 'amount',
      render: (col, record) => (
        <EditableCell
          value={col}
          component={InputNumber}
          onSave={(value) => handleSave(record.key, 'amount', value)}
        />
      ),
    },
  ];

  return <Table columns={columns} data={data} />;
}

function EditableCell({ value, onSave, component: Component = Input }) {
  const [editing, setEditing] = useState(false);
  const [editValue, setEditValue] = useState(value);

  if (editing) {
    return (
      <Component
        autoFocus
        value={editValue}
        onChange={setEditValue}
        onBlur={() => { onSave(editValue); setEditing(false); }}
        onPressEnter={() => { onSave(editValue); setEditing(false); }}
      />
    );
  }
  return <span onClick={() => setEditing(true)} style={{ cursor: 'pointer' }}>{value}</span>;
}
```

## 表格 + 搜索筛选栏

```tsx
function SearchTable() {
  const [form] = Form.useForm();
  const [params, setParams] = useState({});

  return (
    <div>
      <Form form={form} layout="inline" style={{ marginBottom: 16 }}>
        <Form.Item field="name" label="名称">
          <Input placeholder="搜索名称" />
        </Form.Item>
        <Form.Item field="status" label="状态">
          <Select options={['全部', '启用', '禁用']} placeholder="选择状态" />
        </Form.Item>
        <Form.Item>
          <Button type="primary" onClick={async () => {
            const values = form.getFieldsValue();
            setParams(values);
          }}>搜索</Button>
          <Button onClick={() => { form.resetFields(); setParams({}); }} style={{ marginLeft: 8 }}>重置</Button>
        </Form.Item>
      </Form>
      <Table columns={columns} data={filteredData} />
    </div>
  );
}
```

## 最佳实践总结

1. **始终设置 `rowKey`**（默认使用 `key` 字段）
2. **固定列必须设置 `width`**
3. **大数据量用 `virtualized`** + `scroll.y`
4. **服务端排序/筛选在 `onChange` 统一处理**
5. **使用 `preserveSelectedRowKeys`** 跨页保持选中
6. **`loading` 接受 SpinProps**，可自定义加载样式
7. **避免在 `render` 中创建新引用**（函数、对象），影响性能
8. **`ellipsis` 处理长文本列**

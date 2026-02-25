---
name: arco-modal-patterns
description: Arco Design 弹层相关组件使用模式。当需要实现表单弹窗、确认流程、嵌套抽屉或全局消息通知等模式时使用。
user-invocable: false
---

# 弹层模式

Modal、Drawer、Message、Notification 的使用模式。

## Modal vs Drawer 选择

| 场景 | 推荐 | 原因 |
|------|------|------|
| 简单确认操作 | Modal | 轻量，居中吸引注意力 |
| 简短表单（3-5 个字段） | Modal | 不需要大空间 |
| 复杂表单 / 详情查看 | Drawer | 更大空间，不遮挡背景内容 |
| 多步骤向导 | Modal | 居中聚焦 |
| 编辑面板 | Drawer | 可对照原始数据 |

## 确认删除模式

### 方式一：Popconfirm（轻量）

```tsx
<Popconfirm
  title="确认删除此项？"
  onOk={() => handleDelete(id)}
>
  <Button type="text" status="danger" size="small">删除</Button>
</Popconfirm>
```

### 方式二：Modal.confirm（重要操作）

```tsx
const handleDelete = (record) => {
  Modal.confirm({
    title: '确认删除',
    content: `确定要删除「${record.name}」吗？此操作不可恢复。`,
    okButtonProps: { status: 'danger' },
    onOk: async () => {
      await api.delete(record.id);
      Message.success('删除成功');
      refresh();
    },
  });
};
```

## 异步操作 + 加载状态

```tsx
function EditModal({ visible, onClose, record }) {
  const [form] = Form.useForm();
  const [loading, setLoading] = useState(false);

  return (
    <Modal
      title="编辑"
      visible={visible}
      confirmLoading={loading}
      onOk={async () => {
        try {
          const values = await form.validate();
          setLoading(true);
          await api.update(record.id, values);
          Message.success('保存成功');
          onClose(true);  // true 表示需要刷新
        } catch {
          // form.validate 失败不需要处理
        } finally {
          setLoading(false);
        }
      }}
      onCancel={() => onClose(false)}
      afterClose={() => form.resetFields()}
      maskClosable={false}  // 防止误关闭
    >
      <Form form={form} layout="vertical" initialValues={record}>
        <Form.Item field="name" label="名称" rules={[{ required: true }]}>
          <Input />
        </Form.Item>
      </Form>
    </Modal>
  );
}
```

## Message 操作反馈模式

```tsx
// 基本反馈
const handleSave = async () => {
  try {
    await api.save(data);
    Message.success('保存成功');
  } catch (err) {
    Message.error(`保存失败: ${err.message}`);
  }
};

// 加载→成功/失败 模式
const handleSubmit = async () => {
  Message.loading({ id: 'submit', content: '提交中...' });
  try {
    await api.submit(data);
    Message.success({ id: 'submit', content: '提交成功' });
  } catch {
    Message.error({ id: 'submit', content: '提交失败' });
  }
};
```

## Notification 通知模式

```tsx
// 带操作按钮的通知
Notification.info({
  title: '新版本可用',
  content: '发现新版本 v2.0.0',
  duration: 0,  // 不自动关闭
  btn: (
    <Space>
      <Button type="secondary" size="small" onClick={() => Notification.remove('update')}>
        稍后
      </Button>
      <Button type="primary" size="small" onClick={() => { window.location.reload(); }}>
        立即更新
      </Button>
    </Space>
  ),
  id: 'update',
});

// WebSocket 实时通知
ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  Notification.info({
    title: data.title,
    content: data.content,
    position: 'bottomRight',
  });
};
```

## useModal / useMessage 使用场景

当需要在弹层中使用 ConfigProvider 的 context（locale、theme）时：

```tsx
function App() {
  const [modal, modalHolder] = Modal.useModal();
  const [message, messageHolder] = Message.useMessage();

  return (
    <ConfigProvider locale={enUS}>
      {modalHolder}
      {messageHolder}
      <Button onClick={() => {
        modal.confirm({
          title: 'Confirm',
          content: 'Are you sure?',  // 会使用 enUS locale
        });
      }}>
        Action
      </Button>
    </ConfigProvider>
  );
}
```

## 最佳实践

1. **简单反馈用 Message**，复杂通知用 Notification
2. **确认操作优先 Popconfirm**，重要操作用 Modal.confirm
3. **弹窗表单设 `maskClosable={false}`** 防误关闭
4. **使用 `afterClose` 重置表单**，而非 `onCancel`
5. **异步操作使用 `confirmLoading`** 禁用重复提交
6. **需要 context 时使用 Hook API**（useModal / useMessage）
7. **`Message.loading` + id 更新**实现加载→结果转换

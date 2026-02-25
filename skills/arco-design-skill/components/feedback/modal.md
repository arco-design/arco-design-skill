---
name: arco-modal
description: Arco Modal 对话框组件用法与 API。当需要模态弹窗、确认对话框（Modal.confirm）、信息提示或 useModal Hook 时使用。
user-invocable: false
---

# Modal 对话框

模态对话框，用于重要交互确认。

## 基本用法

```tsx
import { Modal, Button } from '@arco-design/web-react';

function Demo() {
  const [visible, setVisible] = useState(false);

  return (
    <>
      <Button onClick={() => setVisible(true)}>打开弹窗</Button>
      <Modal
        title="标题"
        visible={visible}
        onOk={() => { handleOk(); setVisible(false); }}
        onCancel={() => setVisible(false)}
      >
        弹窗内容
      </Modal>
    </>
  );
}
```

## API

### ModalProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `visible` | `boolean` | — | 是否可见 |
| `title` | `ReactNode` | — | 标题 |
| `onOk` | `(e) => void \| Promise` | — | 确认回调 |
| `onCancel` | `(e) => void` | — | 取消回调 |
| `okText` | `string` | `'确定'` | 确认按钮文字 |
| `cancelText` | `string` | `'取消'` | 取消按钮文字 |
| `okButtonProps` | `ButtonProps` | — | 确认按钮属性 |
| `cancelButtonProps` | `ButtonProps` | — | 取消按钮属性 |
| `footer` | `ReactNode \| null` | — | 底部内容（null 隐藏） |
| `closable` | `boolean` | `true` | 显示关闭按钮 |
| `mask` | `boolean` | `true` | 显示遮罩 |
| `maskClosable` | `boolean` | `true` | 点击遮罩关闭 |
| `confirmLoading` | `boolean` | — | 确认按钮加载中 |
| `simple` | `boolean` | — | 简洁模式（无标题栏） |
| `alignCenter` | `boolean` | `true` | 垂直居中 |
| `escToExit` | `boolean` | `true` | ESC 关闭 |
| `focusLock` | `boolean` | `true` | 焦点锁定 |
| `autoFocus` | `boolean` | `true` | 自动聚焦 |
| `mountOnEnter` | `boolean` | `true` | 首次打开时才渲染 |
| `unmountOnExit` | `boolean` | — | 关闭后销毁 DOM |
| `getPopupContainer` | `() => Element` | — | 弹出容器 |
| `getChildrenPopupContainer` | `(node) => Element` | — | 子弹出层容器 |
| `wrapClassName` | `string` | — | 遮罩层类名 |
| `modalRender` | `(node: ReactNode) => ReactNode` | — | 自定义渲染 |
| `afterOpen` | `() => void` | — | 打开后回调 |
| `afterClose` | `() => void` | — | 关闭后回调 |

### 静态方法

```tsx
// 确认框
Modal.confirm({
  title: '确认删除？',
  content: '此操作不可恢复',
  onOk: () => deleteItem(),
});

// 信息提示
Modal.info({ title: '提示', content: '操作成功' });
Modal.success({ title: '成功', content: '提交成功' });
Modal.warning({ title: '警告', content: '请注意' });
Modal.error({ title: '错误', content: '操作失败' });

// 静态方法返回实例，可以更新和关闭
const modal = Modal.confirm({ title: '加载中', content: <Spin /> });
setTimeout(() => {
  modal.update({ title: '完成', content: '操作已完成' });
}, 2000);
modal.close();
```

### useModal Hook

```tsx
const [modal, contextHolder] = Modal.useModal();

// 在 JSX 中放置 contextHolder
<ConfigProvider>
  {contextHolder}
  <Button onClick={() => {
    modal.confirm({ title: '确认', content: '确认操作？' });
  }}>
    操作
  </Button>
</ConfigProvider>
```

> **`useModal` 的优势**：能够读取 ConfigProvider 的 context（locale、theme 等），而静态方法 `Modal.confirm` 无法获取 context。

## 异步关闭

```tsx
<Modal
  title="提交"
  visible={visible}
  confirmLoading={loading}
  onOk={async () => {
    setLoading(true);
    await submitData();
    setLoading(false);
    setVisible(false);
  }}
>
  表单内容
</Modal>
```

## 最佳实践

1. **优先使用声明式 `<Modal>`**，而非静态方法
2. **需要 context 时使用 `useModal`** hook
3. **长表单场景考虑使用 Drawer** 替代 Modal
4. **设置 `maskClosable={false}`** 避免误关闭重要表单
5. **`unmountOnExit` 用于重置表单状态**
6. **`afterClose` 中清理数据**，避免在 visible 变化时清理

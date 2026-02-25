---
name: arco-drawer
description: Arco Drawer 抽屉组件用法与 API。当需要侧边滑出面板进行详情查看、表单编辑或多级抽屉时使用。
user-invocable: false
---

# Drawer 抽屉

侧边滑出的面板，用于详情查看、表单编辑等。

## 基本用法

```tsx
import { Drawer, Button } from '@arco-design/web-react';

function Demo() {
  const [visible, setVisible] = useState(false);
  return (
    <>
      <Button onClick={() => setVisible(true)}>打开抽屉</Button>
      <Drawer
        title="详情"
        visible={visible}
        onOk={() => setVisible(false)}
        onCancel={() => setVisible(false)}
        width={500}
      >
        内容区域
      </Drawer>
    </>
  );
}
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `visible` | `boolean` | — | 是否可见 |
| `title` | `ReactNode` | — | 标题 |
| `placement` | `'top' \| 'right' \| 'bottom' \| 'left'` | `'right'` | 出现位置 |
| `width` | `number \| string` | `250` | 宽度（left/right） |
| `height` | `number \| string` | `250` | 高度（top/bottom） |
| `onOk` | `(e) => void` | — | 确认回调 |
| `onCancel` | `(e) => void` | — | 取消/关闭回调 |
| `footer` | `ReactNode \| null` | — | 底部（null 隐藏） |
| `closable` | `boolean` | `true` | 关闭按钮 |
| `mask` | `boolean` | `true` | 遮罩 |
| `maskClosable` | `boolean` | `true` | 遮罩关闭 |
| `escToExit` | `boolean` | `true` | ESC 关闭 |
| `confirmLoading` | `boolean` | — | 确认加载 |
| `mountOnEnter` | `boolean` | `true` | 首次渲染 |
| `unmountOnExit` | `boolean` | — | 关闭销毁 |
| `focusLock` | `boolean` | `true` | 焦点锁定 |
| `autoFocus` | `boolean` | `true` | 自动聚焦 |
| `getPopupContainer` | `() => Element` | — | 挂载容器 |
| `afterOpen` | `() => void` | — | 打开后回调 |
| `afterClose` | `() => void` | — | 关闭后回调 |

## 嵌套抽屉

```tsx
<Drawer title="一级" visible={visible1} width={600}>
  <Button onClick={() => setVisible2(true)}>打开二级</Button>
  <Drawer title="二级" visible={visible2} width={400}>
    二级内容
  </Drawer>
</Drawer>
```

## 最佳实践

1. **详情和编辑表单使用 Drawer**，比 Modal 提供更大的空间
2. **设置合理的 `width`**，常用 400-600px
3. **移动端可使用 `placement="bottom"`** 从底部弹出

---
name: arco-resize-box
description: Arco ResizeBox 伸缩框组件用法与 API。当需要可拖拽调整大小的容器或分割面板时使用。
user-invocable: false
---

# ResizeBox 伸缩框

可拖拽调整大小的容器。

```tsx
import { ResizeBox } from '@arco-design/web-react';

<ResizeBox
  directions={['right', 'bottom']}
  style={{ width: 500, minWidth: 100, maxWidth: 800, height: 300 }}
>
  可拖拽调整大小
</ResizeBox>

// 分栏
<ResizeBox.Split
  direction="horizontal"
  panes={[
    { content: <div>左侧面板</div>, size: 0.3, min: '100px' },
    { content: <div>右侧面板</div> },
  ]}
/>

// 多栏分割
<ResizeBox.SplitGroup direction="horizontal">
  <ResizeBox.SplitGroup.Pane size={0.2}>面板1</ResizeBox.SplitGroup.Pane>
  <ResizeBox.SplitGroup.Pane>面板2</ResizeBox.SplitGroup.Pane>
  <ResizeBox.SplitGroup.Pane size={0.3}>面板3</ResizeBox.SplitGroup.Pane>
</ResizeBox.SplitGroup>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `width` / `height` | `number` | 受控尺寸 |
| `directions` | `('left' \| 'right' \| 'top' \| 'bottom')[]` | 拖拽方向 |
| `onMoving` | `(e, { width, height }) => void` | 拖拽中 |
| `onMovingStart` | `() => void` | 开始拖拽 |
| `onMovingEnd` | `() => void` | 结束拖拽 |

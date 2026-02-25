---
name: arco-button
description: Arco Button 按钮组件用法与 API。当需要创建按钮、按钮组、图标按钮或处理按钮加载状态时使用。
user-invocable: false
---

# Button 按钮

用于触发操作的基础交互组件。

## 基本用法

```tsx
import { Button } from '@arco-design/web-react';

// 基本类型
<Button type="primary">主要按钮</Button>
<Button type="secondary">次要按钮</Button>
<Button type="dashed">虚线按钮</Button>
<Button type="text">文字按钮</Button>
<Button type="outline">线框按钮</Button>

// 状态按钮
<Button type="primary" status="warning">警告</Button>
<Button type="primary" status="danger">危险</Button>
<Button type="primary" status="success">成功</Button>
```

## API

### ButtonProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `'default' \| 'primary' \| 'secondary' \| 'dashed' \| 'text' \| 'outline'` | `'default'` | 按钮类型 |
| `status` | `'warning' \| 'danger' \| 'success' \| 'default'` | `'default'` | 按钮状态 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | `'default'` | 尺寸 |
| `shape` | `'circle' \| 'round' \| 'square'` | `'square'` | 按钮形状 |
| `disabled` | `boolean` | — | 是否禁用 |
| `loading` | `boolean` | — | 是否加载中 |
| `loadingFixedWidth` | `boolean` | — | 加载时保持宽度不变 |
| `icon` | `ReactNode` | — | 按钮图标 |
| `iconOnly` | `boolean` | — | 仅图标模式 |
| `long` | `boolean` | — | 按钮宽度撑满容器 |
| `href` | `string` | — | 作为链接使用 |
| `htmlType` | `'button' \| 'submit' \| 'reset'` | `'button'` | 原生 HTML type |
| `onClick` | `(e: Event) => void` | — | 点击回调 |

### Button.Group

按钮组合，用于将多个按钮组合在一起：

```tsx
<Button.Group>
  <Button type="primary">左</Button>
  <Button type="primary">中</Button>
  <Button type="primary">右</Button>
</Button.Group>
```

## 常用模式

```tsx
// 图标按钮
import { IconPlus, IconDelete } from '@arco-design/web-react/icon';

<Button type="primary" icon={<IconPlus />}>新建</Button>
<Button shape="circle" icon={<IconDelete />} status="danger" />

// 加载状态
const [loading, setLoading] = useState(false);
<Button type="primary" loading={loading} onClick={async () => {
  setLoading(true);
  await submitForm();
  setLoading(false);
}}>
  提交
</Button>

// 全宽按钮（常用于移动端或表单底部）
<Button type="primary" long>全宽按钮</Button>

// 链接按钮
<Button type="text" href="https://arco.design" target="_blank">
  访问官网
</Button>
```

## 最佳实践

1. **每个页面只有一个 primary 按钮**作为主操作
2. **使用 `loadingFixedWidth`** 避免加载时按钮宽度跳动
3. **确认操作使用 `status="danger"`**，如删除按钮
4. **表单中使用 `htmlType="submit"`** 而非 onClick 提交
5. **图标按钮无文字时设置 `iconOnly`** 以获得正确的样式

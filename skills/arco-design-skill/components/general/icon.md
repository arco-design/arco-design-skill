---
name: arco-icon
description: Arco Icon 图标组件用法。当需要使用内置图标、自定义图标或 IconFont 时使用。
user-invocable: false
---

# Icon 图标

Arco Design 图标库，作为独立包 `@arco-design/web-react/icon` 提供。

## 基本用法

```tsx
import { IconSearch, IconPlus, IconDelete, IconEdit } from '@arco-design/web-react/icon';

<IconSearch />
<IconPlus style={{ fontSize: 24, color: '#165DFF' }} />
```

## API

### IconProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `style` | `CSSProperties` | — | 行内样式（支持 fontSize、color） |
| `className` | `string` | — | 自定义类名 |
| `spin` | `boolean` | — | 是否旋转 |
| `onClick` | `(e: Event) => void` | — | 点击回调 |

## 图标分类

图标按功能分为以下几类：
- **方向类**: IconUp, IconDown, IconLeft, IconRight, IconArrowUp, IconArrowDown...
- **提示类**: IconInfo, IconInfoCircle, IconWarning, IconCheck, IconClose...
- **编辑类**: IconEdit, IconDelete, IconCopy, IconPaste, IconUndo, IconRedo...
- **媒体类**: IconImage, IconVideo, IconCamera, IconMusic...
- **通用类**: IconSearch, IconPlus, IconMinus, IconMore, IconFilter, IconSettings...
- **文件类**: IconFile, IconFolder, IconUpload, IconDownload...
- **用户类**: IconUser, IconUserGroup, IconUserAdd...

## 在组件中使用

```tsx
import { Button, Input, Menu } from '@arco-design/web-react';
import { IconSearch, IconHome, IconSettings } from '@arco-design/web-react/icon';

// 按钮图标
<Button type="primary" icon={<IconSearch />}>搜索</Button>

// 输入框前缀
<Input prefix={<IconSearch />} placeholder="搜索..." />

// 菜单图标
<Menu.Item key="home">
  <IconHome /> 首页
</Menu.Item>
```

## 自定义图标

使用 SVG 创建自定义图标：

```tsx
import { Icon } from '@arco-design/web-react/icon';

const CustomIcon = (props) => (
  <Icon {...props} viewBox="0 0 1024 1024">
    <path d="M..." />
  </Icon>
);
```

## 最佳实践

1. **按需导入图标** 避免打包所有图标
2. **通过 `style` 控制大小和颜色**：`style={{ fontSize: 20, color: '#333' }}`
3. **加载状态使用 `spin` 属性**：`<IconLoading spin />`
4. **语义化选择图标** 保持交互一致性

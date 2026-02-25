---
name: arco-typography
description: Arco Typography 排版组件用法与 API。当需要展示标题、段落、文本，或实现文本省略、可复制、可编辑功能时使用。
user-invocable: false
---

# Typography 排版

用于展示标题、段落、文本等排版元素，支持省略、可复制、可编辑。

## 基本用法

```tsx
import { Typography } from '@arco-design/web-react';
const { Title, Paragraph, Text } = Typography;

<Typography>
  <Title heading={1}>一级标题</Title>
  <Title heading={2}>二级标题</Title>
  <Paragraph>这是一段正文内容。</Paragraph>
  <Text>普通文本</Text>
  <Text bold>加粗文本</Text>
  <Text disabled>禁用文本</Text>
  <Text type="secondary">次要文本</Text>
  <Text type="success">成功文本</Text>
  <Text type="warning">警告文本</Text>
  <Text type="error">错误文本</Text>
  <Text mark>标记文本</Text>
  <Text underline>下划线</Text>
  <Text delete>删除线</Text>
  <Text code>代码文本</Text>
</Typography>
```

## API

### Title Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `heading` | `1 \| 2 \| 3 \| 4 \| 5 \| 6` | `1` | 标题级别 |

### Text / Paragraph 通用 Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `'primary' \| 'secondary' \| 'success' \| 'warning' \| 'error'` | — | 文本类型 |
| `bold` | `boolean` | — | 加粗 |
| `disabled` | `boolean` | — | 禁用 |
| `mark` | `boolean \| { color: string }` | — | 标记高亮 |
| `underline` | `boolean` | — | 下划线 |
| `delete` | `boolean` | — | 删除线 |
| `code` | `boolean` | — | 代码样式 |
| `copyable` | `boolean \| CopyableConfig` | — | 可复制 |
| `editable` | `boolean \| EditableConfig` | — | 可编辑 |
| `ellipsis` | `boolean \| EllipsisConfig` | — | 文本省略 |

### EllipsisConfig

```tsx
// 单行省略
<Paragraph ellipsis>很长的文本内容...</Paragraph>

// 多行省略
<Paragraph ellipsis={{ rows: 3, showTooltip: true }}>
  很长的多行文本内容...
</Paragraph>

// 可展开/收起
<Paragraph ellipsis={{ rows: 2, expandable: true }}>
  很长的文本内容...
</Paragraph>
```

### CopyableConfig

```tsx
// 可复制文本
<Paragraph copyable>这段文字可以复制</Paragraph>

// 自定义复制文本
<Paragraph copyable={{ text: '自定义复制内容' }}>
  展示文本
</Paragraph>
```

## 最佳实践

1. **使用 `ellipsis` 处理长文本**，配合 `showTooltip` 展示完整内容
2. **可编辑场景使用 `editable`**，替代单独的 Input 组件
3. **`copyable` 用于展示地址、ID 等需要复制的内容**

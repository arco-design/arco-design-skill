---
name: arco-tag
description: Arco Tag 标签组件用法与 API。当需要展示状态标签、可关闭标签或可选中标签时使用。
user-invocable: false
---

# Tag 标签

```tsx
import { Tag } from '@arco-design/web-react';

<Tag>默认</Tag>
<Tag color="red">红色</Tag>
<Tag color="arcoblue">主题色</Tag>
<Tag closable onClose={() => {}}>可关闭</Tag>
<Tag checkable defaultChecked>可选中</Tag>
<Tag size="large" bordered>大号有边框</Tag>

// 预设颜色
// red, orangered, orange, gold, lime, green, cyan, blue, arcoblue, purple, pinkpurple, magenta, gray
```

## TagProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `color` | `string` | — | 颜色（预设名或自定义色值） |
| `size` | `'small' \| 'default' \| 'medium' \| 'large'` | `'default'` | 尺寸 |
| `closable` | `boolean` | — | 可关闭 |
| `checkable` | `boolean` | — | 可选中 |
| `checked` / `defaultChecked` | `boolean` | — | 选中状态 |
| `visible` / `defaultVisible` | `boolean` | — | 显示状态 |
| `bordered` | `boolean` | — | 边框 |
| `icon` | `ReactNode` | — | 图标 |
| `closeIcon` | `ReactNode` | — | 关闭图标 |
| `onClose` | `(e) => void` | — | 关闭回调 |
| `onCheck` | `(checked) => void` | — | 选中回调 |

## 常用模式

```tsx
// 可关闭标签
<Tag closable onClose={() => removeTag(id)}>标签内容</Tag>

// 可选中标签（筛选场景）
const [checked, setChecked] = useState(false);
<Tag.CheckableTag checked={checked} onChange={setChecked}>筛选项</Tag.CheckableTag>

// 多种预设颜色
{['red', 'orangered', 'orange', 'gold', 'lime', 'green', 'cyan', 'blue', 'arcoblue', 'purple', 'magenta'].map(color => (
  <Tag key={color} color={color}>{color}</Tag>
))}

// 动态添加标签
const [tags, setTags] = useState(['Tag1', 'Tag2']);
const [inputVisible, setInputVisible] = useState(false);
<Space>
  {tags.map(tag => <Tag key={tag} closable onClose={() => setTags(tags.filter(t => t !== tag))}>{tag}</Tag>)}
  {inputVisible ? (
    <Input size="mini" autoFocus onPressEnter={(e) => { setTags([...tags, e.target.value]); setInputVisible(false); }} />
  ) : (
    <Tag icon={<IconPlus />} onClick={() => setInputVisible(true)}>添加</Tag>
  )}
</Space>
```

## 最佳实践

1. **状态标签用预设颜色** —— 如 success=green、error=red、warning=orange
2. **CheckableTag 用于筛选** —— 比 Checkbox 更紧凑
3. **closable 配合列表使用** —— 展示已选项并支持移除

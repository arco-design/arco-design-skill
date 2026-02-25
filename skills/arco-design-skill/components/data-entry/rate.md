---
name: arco-rate
description: Arco Rate 评分组件用法与 API。当需要星级评分、半选评分或自定义评分字符时使用。
user-invocable: false
---

# Rate 评分

```tsx
import { Rate } from '@arco-design/web-react';

<Rate defaultValue={3} />
<Rate allowHalf defaultValue={2.5} />
<Rate count={10} />
<Rate character={<IconHeart />} />
<Rate readonly defaultValue={4} />
```

## RateProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `number` | — | 受控值 |
| `defaultValue` | `number` | — | 默认值 |
| `count` | `number` | `5` | 总数 |
| `allowHalf` | `boolean` | — | 允许半选 |
| `allowClear` | `boolean` | — | 允许清零 |
| `readonly` | `boolean` | — | 只读 |
| `disabled` | `boolean` | — | 禁用 |
| `grading` | `boolean` | — | 笑脸分级 |
| `character` | `ReactNode \| ((index: number) => ReactNode)` | — | 自定义图标 |
| `tooltips` | `string[]` | — | 各分值提示文案 |
| `onChange` | `(value: number) => void` | — | 变化回调 |
| `onHoverChange` | `(value: number) => void` | — | hover 变化 |

## 常用模式

```tsx
// 受控使用
const [value, setValue] = useState(3);
<Rate value={value} onChange={setValue} />

// 半选
<Rate allowHalf defaultValue={3.5} />

// 只读展示
<Rate readonly defaultValue={4} />

// 自定义字符
<Rate character={<IconHeart />} defaultValue={3} />

// 带文字说明
const labels = ['极差', '差', '一般', '好', '极好'];
<Rate onChange={(val) => setDesc(labels[val - 1])} />
<span style={{ marginLeft: 8 }}>{desc}</span>

// 配合 Form
<Form.Item field="rating" label="评分" rules={[{ required: true, type: 'number', min: 1, message: '请评分' }]}>
  <Rate allowHalf />
</Form.Item>
```

## 最佳实践

1. **allowHalf 提高精度** —— 评分场景建议开启半选
2. **readonly 用于展示** —— 展示已有评分时设为只读
3. **count 默认 5** —— 一般无需修改，符合用户认知

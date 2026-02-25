---
name: arco-divider
description: Arco Divider 分割线组件用法与 API。当需要在内容之间添加水平或垂直分隔线时使用。
user-invocable: false
---

# Divider 分割线

区隔内容的分割线，支持水平和垂直方向。

```tsx
import { Divider } from '@arco-design/web-react';

// 水平分割线
<Divider />

// 带文字
<Divider>居中文字</Divider>
<Divider orientation="left">左侧文字</Divider>
<Divider orientation="right">右侧文字</Divider>

// 垂直分割线
<span>文本</span>
<Divider type="vertical" />
<span>文本</span>

// 虚线
<Divider style={{ borderBottomStyle: 'dashed' }} />
```

## DividerProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `'horizontal' \| 'vertical'` | `'horizontal'` | 方向 |
| `orientation` | `'left' \| 'center' \| 'right'` | `'center'` | 文字位置 |

## 常用模式

```tsx
// 带文字的分割线
<Divider>居中标题</Divider>
<Divider orientation="left">左侧标题</Divider>
<Divider orientation="right">右侧标题</Divider>

// 虚线
<Divider type="dashed" />

// 垂直分割线（行内使用）
<Space>
  <Link>首页</Link>
  <Divider type="vertical" />
  <Link>关于</Link>
  <Divider type="vertical" />
  <Link>联系</Link>
</Space>
```

## 最佳实践

1. **水平分割线用于内容分区** —— 段落之间、章节之间
2. **垂直分割线用于行内分隔** —— 如操作按钮组、导航链接之间
3. **带文字分割线做小标题** —— 替代简单的 h4/h5 标题

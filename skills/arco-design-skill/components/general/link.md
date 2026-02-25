---
name: arco-link
description: Arco Link 链接组件用法与 API。当需要创建超链接、带图标链接或不同状态的链接时使用。
user-invocable: false
---

# Link 链接

基础超链接组件，支持不同状态和图标。

```tsx
import { Link } from '@arco-design/web-react';

<Link href="https://arco.design">默认链接</Link>
<Link href="/page" status="success">成功链接</Link>
<Link href="/page" status="warning">警告链接</Link>
<Link href="/page" status="danger">危险链接</Link>
<Link disabled>禁用链接</Link>
<Link icon>带图标的链接</Link>  {/* 自动添加外链图标 */}
```

### LinkProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `href` | `string` | — | 链接地址 |
| `status` | `'success' \| 'warning' \| 'danger' \| 'default'` | `'default'` | 链接状态 |
| `disabled` | `boolean` | — | 禁用 |
| `icon` | `boolean \| ReactNode` | — | 显示图标 |
| `hoverable` | `boolean` | `true` | 是否有 hover 下划线 |

## 常用模式

```tsx
// 配合 React Router
import { Link as ArcoLink } from '@arco-design/web-react';
import { useNavigate } from 'react-router-dom';

const navigate = useNavigate();
<ArcoLink onClick={() => navigate('/about')}>关于我们</ArcoLink>

// 外部链接（带图标提示）
<Link href="https://arco.design" target="_blank" icon>
  Arco Design 官网
</Link>

// 在文本中使用
<Typography.Paragraph>
  请查看 <Link href="/docs">使用文档</Link> 了解更多。
</Typography.Paragraph>

// 不同状态
<Space>
  <Link status="success">成功</Link>
  <Link status="warning">警告</Link>
  <Link status="danger">危险</Link>
</Space>
```

## 最佳实践

1. **外部链接使用 icon** —— `icon` 属性自动添加外链图标，提示用户将跳转外部
2. **搭配 React Router 时用 onClick** —— 避免页面刷新，使用路由导航
3. **与 Button type="text" 的区别** —— Link 有下划线语义更明确，Button text 无下划线

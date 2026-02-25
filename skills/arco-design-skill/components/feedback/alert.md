---
name: arco-alert
description: Arco Alert 警告提示组件用法与 API。当需要在页面内展示警告、提示、成功或错误等信息条时使用。
user-invocable: false
---

# Alert 警告提示

页面内的警告信息展示。

```tsx
import { Alert } from '@arco-design/web-react';

<Alert type="info" content="信息提示" />
<Alert type="success" content="成功提示" />
<Alert type="warning" content="警告提示" />
<Alert type="error" content="错误提示" />
<Alert type="info" title="标题" content="带标题的提示" closable />
<Alert banner type="warning" content="横幅式警告，适用于页面顶部" />
```

### AlertProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `'info' \| 'success' \| 'warning' \| 'error'` | `'info'` | 类型 |
| `title` | `ReactNode` | — | 标题 |
| `content` | `ReactNode` | — | 内容 |
| `showIcon` | `boolean` | `true` | 显示图标 |
| `icon` | `ReactNode` | — | 自定义图标 |
| `closable` | `boolean` | — | 可关闭 |
| `closeElement` | `ReactNode` | — | 自定义关闭元素 |
| `banner` | `boolean` | — | 横幅模式 |
| `action` | `ReactNode` | — | 操作区域 |
| `onClose` | `(e) => void` | — | 关闭回调 |
| `afterClose` | `() => void` | — | 关闭动画结束后 |

## 常用模式

```tsx
// 不同类型
<Alert type="info" content="这是一条提示信息" />
<Alert type="success" content="操作成功" />
<Alert type="warning" content="请注意安全" />
<Alert type="error" content="操作失败，请重试" />

// 带标题和描述
<Alert type="warning" title="注意" content="该功能即将下线，请及时迁移到新版本。" />

// 可关闭
<Alert type="info" closable content="可关闭的提示" onClose={() => console.log('closed')} />

// 带操作按钮
<Alert type="info" title="新版本可用" content="发现新版本 v2.0" action={<Button size="mini" type="primary">升级</Button>} />

// 横幅模式（页面顶部通栏）
<Alert banner type="warning" content="系统将于今晚 22:00 进行维护" closable />
```

## 最佳实践

1. **banner 用于全局通知** —— 放在页面最顶部，无边框无圆角
2. **type 对应语义** —— info=提示、success=成功、warning=警告、error=错误
3. **重要告警不要设 closable** —— 确保用户不会忽略关键信息
4. **action 放操作入口** —— 如「立即升级」「查看详情」

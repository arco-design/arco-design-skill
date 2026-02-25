---
name: arco-result
description: Arco Result 结果页组件用法与 API。当需要展示操作结果（成功、失败、404 等）的反馈页面时使用。
user-invocable: false
---

# Result 结果页

```tsx
import { Result, Button } from '@arco-design/web-react';

<Result
  status="success"
  title="操作成功"
  subTitle="订单已提交，请等待审核。"
  extra={[
    <Button key="back" type="secondary">返回列表</Button>,
    <Button key="again" type="primary">再次提交</Button>,
  ]}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `status` | `'success' \| 'error' \| 'info' \| 'warning' \| '404' \| '403' \| '500' \| null` | 状态 |
| `title` | `ReactNode` | 标题 |
| `subTitle` | `ReactNode` | 副标题 |
| `icon` | `ReactNode` | 自定义图标 |
| `extra` | `ReactNode` | 操作区 |

## 常用模式

```tsx
// 提交成功页
<Result
  status="success"
  title="提交成功"
  subTitle="订单号: 2024010100001，预计 2 个工作日内处理完成。"
  extra={[
    <Button key="home" type="primary" onClick={() => navigate('/')}>返回首页</Button>,
    <Button key="detail" onClick={() => navigate('/orders')}>查看订单</Button>,
  ]}
/>

// 权限不足
<Result status="403" subTitle="抱歉，您没有权限访问此页面。">
  <Button type="primary" onClick={() => navigate('/')}>返回首页</Button>
</Result>

// 404 页面
<Result status="404" subTitle="页面不存在">
  <Button type="primary" onClick={() => navigate(-1)}>返回上一页</Button>
</Result>

// 自定义图标
<Result icon={<IconCheckCircleFill style={{ color: '#00b42a', fontSize: 48 }} />} title="自定义成功">
  <Typography.Paragraph>自定义描述内容</Typography.Paragraph>
</Result>
```

## 最佳实践

1. **始终提供操作按钮** —— 告诉用户下一步可以做什么
2. **subTitle 给出具体信息** —— 如订单号、预计时间等
3. **错误页面提供返回路径** —— 403/404/500 页面必须有返回链接

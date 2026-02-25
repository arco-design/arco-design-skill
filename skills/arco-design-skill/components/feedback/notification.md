---
name: arco-notification
description: Arco Notification 通知提醒组件用法与 API。当需要在页面角落展示更丰富的通知内容时使用。
user-invocable: false
---

# Notification 通知提醒

更丰富的全局通知，显示在页面角落。

```tsx
import { Notification, Button } from '@arco-design/web-react';

<Button onClick={() => Notification.info({
  title: '通知标题',
  content: '这是通知内容，可以包含更多信息。',
})}>通知</Button>

<Button onClick={() => Notification.success({
  title: '操作成功',
  content: '数据已保存。',
  duration: 5000,
})}>成功通知</Button>
```

## API

```tsx
Notification.info(config: NotificationConfig);
Notification.success(config);
Notification.warning(config);
Notification.error(config);
Notification.normal(config);

// config
{
  title: ReactNode,        // 标题（必填）
  content: ReactNode,      // 内容
  duration: 3000,          // 持续时间 ms
  position: 'topRight',    // 位置: topLeft | topRight | bottomLeft | bottomRight
  closable: true,          // 可关闭
  showIcon: true,          // 显示图标
  id: 'unique',            // 唯一标识
  btn: ReactNode,          // 自定义操作按钮
  icon: ReactNode,         // 自定义图标
  onClose: () => {},       // 关闭回调
  onClick: () => {},       // 点击回调
}

// 更新
Notification.info({ id: 'progress', title: '下载中', content: '30%' });
Notification.success({ id: 'progress', title: '下载完成', content: '100%' });

// 移除
Notification.remove(id);
Notification.clear();

// 全局配置
Notification.config({
  maxCount: 5,
  duration: 3000,
  getContainer: () => document.body,
});
```

## useNotification Hook

```tsx
const [notification, contextHolder] = Notification.useNotification();

<ConfigProvider locale={enUS}>
  {contextHolder}
  <Button onClick={() => notification.success({ title: 'Done!' })}>操作</Button>
</ConfigProvider>
```

## 最佳实践

1. **简单反馈用 Message**，复杂通知用 Notification
2. **用 `id` 实现状态更新**（如下载进度→完成）
3. **`duration: 0`** 需要手动关闭的场景
4. **需要 context 时用 Hook 版本**（useNotification）

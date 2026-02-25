---
name: arco-message
description: Arco Message 全局消息组件用法与 API。当需要在页面顶部显示轻量级的成功、警告、错误等操作反馈时使用。
user-invocable: false
---

# Message 全局提示

轻量级的操作反馈，显示在页面顶部居中。

```tsx
import { Message, Button } from '@arco-design/web-react';

<Button onClick={() => Message.info('这是一条信息')}>信息</Button>
<Button onClick={() => Message.success('操作成功')}>成功</Button>
<Button onClick={() => Message.warning('请注意')}>警告</Button>
<Button onClick={() => Message.error('操作失败')}>错误</Button>
<Button onClick={() => Message.loading('加载中...')}>加载</Button>
```

### API

```tsx
// 基本调用
Message.info(content: string | MessageConfig);
Message.success(content);
Message.warning(content);
Message.error(content);
Message.loading(content);
Message.normal(content);

// 详细配置
Message.info({
  content: '操作成功',
  duration: 3000,       // 持续时间 ms（0 不自动关闭）
  showIcon: true,       // 显示图标
  closable: true,       // 显示关闭按钮
  id: 'unique-msg',     // 唯一标识（相同 id 会更新而非新增）
  position: 'top',      // 位置: top | bottom
  onClose: () => {},    // 关闭回调
});

// 更新已有消息
Message.info({ id: 'loading', content: '加载中...' });
// 稍后更新
Message.success({ id: 'loading', content: '加载完成' });

// 清除所有
Message.clear();

// 全局配置
Message.config({
  maxCount: 5,          // 最大数量
  duration: 3000,       // 默认持续时间
  getContainer: () => document.body,
});
```

### useMessage Hook

```tsx
const [message, contextHolder] = Message.useMessage();

// 能读取 ConfigProvider context
<ConfigProvider locale={enUS}>
  {contextHolder}
  <Button onClick={() => message.success('Done!')}>操作</Button>
</ConfigProvider>
```



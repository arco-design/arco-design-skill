---
name: arco-steps
description: Arco Steps 步骤条组件用法与 API。当需要展示多步骤流程进度或引导用户完成分步操作时使用。
user-invocable: false
---

# Steps 步骤条

```tsx
import { Steps } from '@arco-design/web-react';

<Steps current={2}>
  <Steps.Step title="提交" description="提交申请" />
  <Steps.Step title="审核" description="等待审核" />
  <Steps.Step title="完成" description="审核通过" />
</Steps>

// 垂直
<Steps direction="vertical" current={1}>...</Steps>

// 点状
<Steps type="dot" current={2}>...</Steps>

// 导航类型
<Steps type="navigation" current={1}>...</Steps>
```

## API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `current` | `number` | `1` | 当前步骤 |
| `type` | `'default' \| 'arrow' \| 'dot' \| 'navigation'` | `'default'` | 类型 |
| `size` | `'default' \| 'small'` | `'default'` | 尺寸 |
| `direction` | `'vertical' \| 'horizontal'` | `'horizontal'` | 方向 |
| `status` | `'wait' \| 'process' \| 'finish' \| 'error'` | — | 当前步骤状态 |
| `lineless` | `boolean` | — | 无连接线 |
| `onChange` | `(current, id) => void` | — | 点击步骤 |

## 常用模式

```tsx
// 受控步骤条
const [current, setCurrent] = useState(1);
<Steps current={current} onChange={setCurrent}>
  <Steps.Step title="基本信息" description="填写名称和描述" />
  <Steps.Step title="详细配置" description="设置参数" />
  <Steps.Step title="完成" description="提交审核" />
</Steps>

// 带状态
<Steps current={2}>
  <Steps.Step title="已完成" status="finish" />
  <Steps.Step title="进行中" status="process" />
  <Steps.Step title="出错" status="error" />
  <Steps.Step title="等待" status="wait" />
</Steps>

// 垂直步骤条
<Steps direction="vertical" current={1}>
  <Steps.Step title="步骤一" description="详细描述..." />
  <Steps.Step title="步骤二" description="详细描述..." />
</Steps>

// 点状步骤条
<Steps type="dot" current={2}>
  <Steps.Step title="Step 1" />
  <Steps.Step title="Step 2" />
  <Steps.Step title="Step 3" />
</Steps>
```

## 最佳实践

1. **步骤数建议 3-5 个** —— 过多步骤会让用户感到复杂
2. **description 说明每步内容** —— 帮助用户预知后续操作
3. **error 状态标记问题步骤** —— 配合表单校验，哪步出错标哪步

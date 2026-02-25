---
name: arco-verification-code
description: Arco VerificationCode 验证码输入组件用法与 API。当需要实现验证码输入框时使用。
user-invocable: false
---

# VerificationCode 验证码

```tsx
import { VerificationCode } from '@arco-design/web-react';

<VerificationCode length={6} onChange={(value) => console.log(value)} />
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `length` | `number` | 验证码位数 |
| `value` / `defaultValue` | `string` | 值 |
| `separator` | `(data: { index, character }) => ReactNode` | 分隔符 |
| `disabled` | `boolean` | 禁用 |
| `masked` | `boolean` | 掩码显示 |
| `onChange` | `(value: string) => void` | 变化回调 |
| `onFinish` | `(value: string) => void` | 输入完成 |

## 常用模式

```tsx
// 受控使用
const [code, setCode] = useState('');
<VerificationCode value={code} onChange={setCode} onFinish={(val) => verifyCode(val)} />

// 自定义长度与尺寸
<VerificationCode length={4} size="large" />

// 掩码模式（密码输入）
<VerificationCode masked length={6} />

// 带分隔符
<VerificationCode
  length={6}
  separator={({ index }) => index === 2 ? <span style={{ margin: '0 8px' }}>-</span> : null}
/>

// 错误状态
<VerificationCode status="error" length={6} />
```

## 最佳实践

1. **使用 onFinish 处理完成事件** —— 比 onChange 更适合触发验证请求
2. **设置合理的 length** —— 短信验证码一般 4-6 位
3. **错误时清空并聚焦** —— 验证失败后重置 value 并让用户重新输入

---
name: arco-input
description: Arco Input 输入框组件用法与 API。当需要文本输入、密码输入、搜索框、文本域或带前后缀的输入框时使用。
user-invocable: false
---

# Input 输入框

基础文本输入组件，支持前后缀、密码框、搜索框、文本域。

## 基本用法

```tsx
import { Input } from '@arco-design/web-react';

<Input placeholder="基本输入框" />
<Input allowClear placeholder="可清除" />
<Input disabled placeholder="禁用" />
<Input status="error" placeholder="错误状态" />
<Input status="warning" placeholder="警告状态" />
```

## API

### InputProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | — | 受控值 |
| `defaultValue` | `string` | — | 默认值 |
| `placeholder` | `string` | — | 占位文字 |
| `allowClear` | `boolean` | — | 可清除 |
| `disabled` | `boolean` | — | 禁用 |
| `readOnly` | `boolean` | — | 只读 |
| `status` | `'error' \| 'warning'` | — | 状态 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `prefix` | `ReactNode` | — | 前缀 |
| `suffix` | `ReactNode` | — | 后缀 |
| `addBefore` | `ReactNode` | — | 前置标签 |
| `addAfter` | `ReactNode` | — | 后置标签 |
| `maxLength` | `number \| { length: number; errorOnly: boolean }` | — | 最大长度 |
| `showWordLimit` | `boolean` | — | 显示字数统计 |
| `onChange` | `(value: string, e: Event) => void` | — | 值变化 |
| `onPressEnter` | `(e: Event) => void` | — | 回车回调 |
| `onClear` | `() => void` | — | 清除回调 |
| `normalize` | `(value: string) => string` | — | 值规范化 |
| `height` | `number \| string` | — | 自定义高度 |

### Input.Search

```tsx
<Input.Search placeholder="搜索" onSearch={(value) => search(value)} />
<Input.Search
  searchButton="搜索"
  placeholder="点击按钮搜索"
  onSearch={(value) => search(value)}
/>
```

| 属性 | 类型 | 说明 |
|------|------|------|
| `searchButton` | `boolean \| ReactNode` | 搜索按钮 |
| `loading` | `boolean` | 搜索加载中 |
| `onSearch` | `(value: string) => void` | 搜索回调 |

### Input.TextArea

```tsx
<Input.TextArea
  placeholder="多行输入"
  autoSize={{ minRows: 3, maxRows: 6 }}
  maxLength={500}
  showWordLimit
/>
```

| 属性 | 类型 | 说明 |
|------|------|------|
| `autoSize` | `boolean \| { minRows, maxRows }` | 自动调整高度 |

### Input.Password

```tsx
<Input.Password placeholder="请输入密码" />
```

| 属性 | 类型 | 说明 |
|------|------|------|
| `visibilityToggle` | `boolean` | 显示/隐藏密码切换 |

### Input.Group

```tsx
<Input.Group compact>
  <Select defaultValue="http" style={{ width: 100 }}>
    <Option value="http">http://</Option>
    <Option value="https">https://</Option>
  </Select>
  <Input placeholder="域名" style={{ width: 300 }} />
</Input.Group>
```

## 常用模式

```tsx
// 带图标前缀
import { IconUser, IconLock } from '@arco-design/web-react/icon';

<Input prefix={<IconUser />} placeholder="用户名" />
<Input.Password prefix={<IconLock />} placeholder="密码" />

// 前后置标签
<Input addBefore="http://" addAfter=".com" placeholder="域名" />

// 字数限制 + 统计
<Input maxLength={20} showWordLimit placeholder="最多20字" />

// 受控输入 + 格式化
<Input
  value={value}
  onChange={setValue}
  normalize={(val) => val.toUpperCase()}  // 自动转大写
/>
```

## Ref API

```tsx
const inputRef = useRef<RefInputType>(null);
inputRef.current.focus();
inputRef.current.blur();
inputRef.current.dom;  // 原生 input 元素
```

## 最佳实践

1. **表单中配合 Form.Item 使用**，自动处理 value/onChange
2. **`allowClear` 在搜索场景中应开启**
3. **`autoSize` 用于评论、备注等多行输入**
4. **`normalize` 用于输入格式化**（如手机号加空格）
5. **使用 `status` 而非自定义样式** 展示校验状态

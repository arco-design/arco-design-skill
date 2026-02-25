---
name: arco-form
description: Arco Form 表单组件完整用法与 API。当需要构建表单、表单校验、动态表单（Form.List）、嵌套表单或使用 useForm 实例方法时使用。
user-invocable: false
---

# Form 表单

高性能表单组件，支持数据收集、校验、提交。

## 基本用法

```tsx
import { Form, Input, Button, Select } from '@arco-design/web-react';
const FormItem = Form.Item;

function BasicForm() {
  const [form] = Form.useForm();

  const onSubmit = async () => {
    try {
      const values = await form.validate();
      console.log('表单值:', values);
    } catch (errors) {
      console.log('校验失败:', errors);
    }
  };

  return (
    <Form form={form} layout="vertical" autoComplete="off">
      <FormItem label="用户名" field="username" rules={[{ required: true, message: '请输入用户名' }]}>
        <Input placeholder="请输入用户名" />
      </FormItem>
      <FormItem label="邮箱" field="email" rules={[
        { required: true, message: '请输入邮箱' },
        { type: 'email', message: '邮箱格式不正确' },
      ]}>
        <Input placeholder="请输入邮箱" />
      </FormItem>
      <FormItem label="角色" field="role" rules={[{ required: true }]}>
        <Select options={['admin', 'user', 'guest']} />
      </FormItem>
      <FormItem>
        <Button type="primary" onClick={onSubmit}>提交</Button>
        <Button onClick={() => form.resetFields()} style={{ marginLeft: 16 }}>重置</Button>
      </FormItem>
    </Form>
  );
}
```

## API

### Form Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `form` | `FormInstance` | — | 表单控制实例 |
| `layout` | `'horizontal' \| 'vertical' \| 'inline'` | `'horizontal'` | 布局方式 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 组件尺寸 |
| `labelCol` | `{ span, offset }` | — | 标签布局 |
| `wrapperCol` | `{ span, offset }` | — | 控件布局 |
| `initialValues` | `object` | — | 默认表单数据 |
| `requiredSymbol` | `boolean \| { position: 'start' \| 'end' }` | `true` | 必填标识 |
| `validateTrigger` | `string \| string[]` | `'onChange'` | 校验时机 |
| `scrollToFirstError` | `boolean \| ScrollIntoViewOptions` | — | 校验失败自动滚动 |
| `colon` | `boolean \| ReactNode` | — | 标签后冒号 |
| `disabled` | `boolean` | — | 禁用所有控件 |
| `onValuesChange` | `(changedValues, allValues) => void` | — | 值变化回调 |
| `onSubmit` | `(values) => void` | — | 提交成功回调 |
| `onSubmitFailed` | `(errors) => void` | — | 提交失败回调 |
| `onChange` | `(values, changedValues) => void` | — | 变化回调 |
| `wrapper` | `ComponentType` | `form` | 外层包裹元素 |
| `id` | `string` | — | 表单 id |

### Form.Item Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `field` | `string` | — | 字段路径（支持 `a.b.c` 嵌套） |
| `label` | `ReactNode` | — | 标签 |
| `rules` | `RuleObject[]` | — | 校验规则 |
| `required` | `boolean` | — | 必填（会添加必填校验） |
| `initialValue` | `any` | — | 字段默认值 |
| `dependencies` | `string[]` | — | 依赖字段（联动校验） |
| `shouldUpdate` | `boolean \| (prev, next, info) => boolean` | — | 是否重新渲染 |
| `noStyle` | `boolean` | — | 不渲染布局，仅注册字段 |
| `hidden` | `boolean` | — | 隐藏（仍参与校验） |
| `disabled` | `boolean` | — | 禁用 |
| `trigger` | `string` | `'onChange'` | 收集值的事件名 |
| `triggerPropName` | `string` | `'value'` | 值属性名 |
| `validateTrigger` | `string \| string[]` | — | 校验时机 |
| `formatter` | `(value) => any` | — | 值格式化（展示用） |
| `normalize` | `(value, prevValue, allValues) => any` | — | 值规范化（存储用） |
| `tooltip` | `ReactNode` | — | 标签提示 |
| `extra` | `ReactNode` | — | 额外提示文字 |

### 校验规则 RuleObject

| 属性 | 类型 | 说明 |
|------|------|------|
| `required` | `boolean` | 必填 |
| `type` | `'string' \| 'number' \| 'boolean' \| 'array' \| 'object' \| 'email' \| 'url' \| 'ip'` | 类型校验 |
| `min` / `max` | `number` | 最小/最大长度或值 |
| `length` | `number` | 精确长度 |
| `match` | `RegExp` | 正则匹配 |
| `message` | `string` | 错误消息 |
| `validateTrigger` | `string \| string[]` | 触发时机 |
| `when` | `(values) => boolean` | 条件校验 |
| `validator` | `(value, callback) => void \| Promise` | 自定义校验函数 |
| `validateLevel` | `'error' \| 'warning'` | 校验级别 |

### FormInstance (useForm)

```tsx
const [form] = Form.useForm();
```

| 方法 | 签名 | 说明 |
|------|------|------|
| `getFieldsValue` | `() => Values` | 获取所有字段值 |
| `getFieldValue` | `(field: string) => any` | 获取单个字段值 |
| `setFieldsValue` | `(values: Partial<Values>) => void` | 设置多个字段值 |
| `setFieldValue` | `(field: string, value: any) => void` | 设置单个字段值 |
| `validate` | `(fields?: string[]) => Promise<Values>` | 校验字段 |
| `resetFields` | `(fields?: string[]) => void` | 重置字段 |
| `clearFields` | `(fields?: string[]) => void` | 清空字段 |
| `getFieldsError` | `(fields?: string[]) => Record<string, FieldError>` | 获取校验错误 |
| `getFieldError` | `(field: string) => FieldError \| null` | 获取单个字段错误 |
| `getTouchedFields` | `() => string[]` | 获取已操作的字段 |
| `scrollToField` | `(field: string, options?) => void` | 滚动到指定字段 |

### Form.List — 动态表单列表

```tsx
<Form.List field="users">
  {(fields, { add, remove, move }) => (
    <>
      {fields.map((field, index) => (
        <div key={field.key}>
          <Form.Item field={`${field.field}.name`} rules={[{ required: true }]}>
            <Input placeholder="姓名" />
          </Form.Item>
          <Form.Item field={`${field.field}.age`}>
            <InputNumber placeholder="年龄" />
          </Form.Item>
          <Button onClick={() => remove(index)} status="danger">删除</Button>
        </div>
      ))}
      <Button onClick={() => add()}>添加用户</Button>
    </>
  )}
</Form.List>
```

### Form.Provider — 多表单联动

```tsx
<Form.Provider onFormSubmit={(name, values, { forms }) => {
  if (name === 'form1') {
    const form2Values = forms.form2.getFieldsValue();
    // 合并两个表单的值
  }
}}>
  <Form id="form1" form={form1}>...</Form>
  <Form id="form2" form={form2}>...</Form>
</Form.Provider>
```

## 高级用法

### 联动校验

```tsx
// 确认密码
<Form.Item field="password" rules={[{ required: true }]}>
  <Input.Password placeholder="密码" />
</Form.Item>
<Form.Item
  field="confirmPassword"
  dependencies={['password']}
  rules={[{
    required: true,
    validator: (value, callback) => {
      if (value !== form.getFieldValue('password')) {
        callback('两次密码不一致');
      }
    },
  }]}
>
  <Input.Password placeholder="确认密码" />
</Form.Item>
```

### 自定义表单控件

```tsx
// 自定义控件需接收 value 和 onChange
function PriceInput({ value, onChange }) {
  return (
    <Space>
      <InputNumber value={value?.amount} onChange={(v) => onChange({ ...value, amount: v })} />
      <Select value={value?.currency} onChange={(v) => onChange({ ...value, currency: v })}
        options={['CNY', 'USD', 'EUR']} />
    </Space>
  );
}

<Form.Item field="price" label="价格">
  <PriceInput />
</Form.Item>
```

### 异步校验

```tsx
<Form.Item
  field="username"
  rules={[{
    required: true,
    validator: async (value, callback) => {
      const exists = await checkUsername(value);
      if (exists) callback('用户名已存在');
    },
  }]}
>
  <Input />
</Form.Item>
```

### useWatch — 监听字段值

```tsx
import { Form } from '@arco-design/web-react';

function MyForm() {
  const [form] = Form.useForm();
  const type = Form.useWatch('type', form);

  return (
    <Form form={form}>
      <Form.Item field="type" label="类型">
        <Select options={['A', 'B']} />
      </Form.Item>
      {type === 'A' && (
        <Form.Item field="detail" label="详情">
          <Input />
        </Form.Item>
      )}
    </Form>
  );
}
```

## 最佳实践

1. **始终使用 `Form.useForm()`** 创建表单实例，方便外部控制
2. **`field` 支持嵌套路径**：`user.name`、`addresses[0].city`
3. **校验时机**：输入密码用 `onBlur`，实时搜索用 `onChange`
4. **复杂表单拆分为 `Form.List`**，避免手动管理动态字段
5. **`shouldUpdate` 用于条件渲染**，避免不必要的重渲染
6. **`noStyle` 用于嵌套表单项**，如 Input.Group 内多个字段
7. **使用 `scrollToFirstError`** 提升长表单的用户体验
8. **`normalize` 用于格式化存储值**，如自动 trim、大小写转换

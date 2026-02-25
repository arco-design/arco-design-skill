---
name: arco-form-patterns
description: Arco Design 表单常见模式与最佳实践。当需要实现动态表单、联动校验、嵌套表单、异步提交或复杂表单布局时使用。
user-invocable: false
---

# 表单模式

Arco Design Form 组件的常见使用模式。

## 基本表单

```tsx
import { Form, Input, Select, Button, Message } from '@arco-design/web-react';

function BasicForm() {
  const [form] = Form.useForm();

  const onSubmit = async () => {
    try {
      const values = await form.validate();
      await api.submit(values);
      Message.success('提交成功');
    } catch (errors) {
      // errors 是字段名到错误信息的映射
      console.log(errors);
    }
  };

  return (
    <Form
      form={form}
      layout="vertical"
      initialValues={{ role: 'user' }}
      scrollToFirstError
      autoComplete="off"
    >
      <Form.Item field="name" label="姓名" rules={[{ required: true, message: '请输入姓名' }]}>
        <Input placeholder="请输入" />
      </Form.Item>
      <Form.Item field="email" label="邮箱" rules={[
        { required: true, message: '请输入邮箱' },
        { type: 'email', message: '邮箱格式不正确' },
      ]}>
        <Input placeholder="请输入" />
      </Form.Item>
      <Form.Item field="role" label="角色" rules={[{ required: true }]}>
        <Select options={['admin', 'user', 'guest']} />
      </Form.Item>
      <Form.Item>
        <Button type="primary" onClick={onSubmit} style={{ marginRight: 16 }}>提交</Button>
        <Button onClick={() => form.resetFields()}>重置</Button>
      </Form.Item>
    </Form>
  );
}
```

## 动态表单 (Form.List)

```tsx
function DynamicForm() {
  const [form] = Form.useForm();

  return (
    <Form form={form}>
      <Form.List field="users">
        {(fields, { add, remove }) => (
          <>
            {fields.map((field, index) => (
              <div key={field.key} style={{ display: 'flex', gap: 16, marginBottom: 16 }}>
                <Form.Item
                  field={`${field.field}.name`}
                  rules={[{ required: true, message: '请输入姓名' }]}
                  noStyle
                >
                  <Input placeholder="姓名" />
                </Form.Item>
                <Form.Item
                  field={`${field.field}.phone`}
                  rules={[{ required: true }, { match: /^1\d{10}$/, message: '手机号格式不正确' }]}
                  noStyle
                >
                  <Input placeholder="手机号" />
                </Form.Item>
                <Button status="danger" onClick={() => remove(index)}>删除</Button>
              </div>
            ))}
            <Button type="dashed" long onClick={() => add()}>
              <IconPlus /> 添加用户
            </Button>
          </>
        )}
      </Form.List>
    </Form>
  );
}
```

## 嵌套表单

```tsx
<Form form={form}>
  {/* 嵌套对象 */}
  <Form.Item field="user.name" label="姓名" rules={[{ required: true }]}>
    <Input />
  </Form.Item>
  <Form.Item field="user.email" label="邮箱">
    <Input />
  </Form.Item>
  <Form.Item field="address.city" label="城市">
    <Input />
  </Form.Item>
  {/* 产出值: { user: { name, email }, address: { city } } */}
</Form>
```

## 条件渲染 (联动表单)

```tsx
function ConditionalForm() {
  const [form] = Form.useForm();
  const type = Form.useWatch('type', form);

  return (
    <Form form={form}>
      <Form.Item field="type" label="类型" rules={[{ required: true }]}>
        <Radio.Group options={['个人', '企业']} />
      </Form.Item>

      {type === '个人' && (
        <Form.Item field="idCard" label="身份证" rules={[{ required: true }]}>
          <Input />
        </Form.Item>
      )}

      {type === '企业' && (
        <>
          <Form.Item field="company" label="公司名称" rules={[{ required: true }]}>
            <Input />
          </Form.Item>
          <Form.Item field="taxId" label="税号" rules={[{ required: true }]}>
            <Input />
          </Form.Item>
        </>
      )}
    </Form>
  );
}
```

## 分步表单

```tsx
function StepForm() {
  const [step, setStep] = useState(0);
  const [form] = Form.useForm();

  const steps = [
    { title: '基本信息', fields: ['name', 'email'] },
    { title: '详细信息', fields: ['address', 'phone'] },
    { title: '确认', fields: [] },
  ];

  const handleNext = async () => {
    try {
      await form.validate(steps[step].fields);
      setStep(step + 1);
    } catch {}
  };

  return (
    <>
      <Steps current={step + 1}>
        {steps.map(s => <Steps.Step key={s.title} title={s.title} />)}
      </Steps>
      <Form form={form} layout="vertical">
        <div style={{ display: step === 0 ? 'block' : 'none' }}>
          <Form.Item field="name" label="姓名" rules={[{ required: true }]}>
            <Input />
          </Form.Item>
          <Form.Item field="email" label="邮箱" rules={[{ required: true, type: 'email' }]}>
            <Input />
          </Form.Item>
        </div>
        <div style={{ display: step === 1 ? 'block' : 'none' }}>
          <Form.Item field="address" label="地址" rules={[{ required: true }]}>
            <Input />
          </Form.Item>
        </div>
        <div style={{ display: step === 2 ? 'block' : 'none' }}>
          确认提交？
        </div>
        <Space>
          {step > 0 && <Button onClick={() => setStep(step - 1)}>上一步</Button>}
          {step < 2 && <Button type="primary" onClick={handleNext}>下一步</Button>}
          {step === 2 && <Button type="primary" onClick={() => form.validate().then(submit)}>提交</Button>}
        </Space>
      </Form>
    </>
  );
}
```

## 弹窗表单

```tsx
function ModalForm() {
  const [visible, setVisible] = useState(false);
  const [form] = Form.useForm();

  return (
    <>
      <Button onClick={() => setVisible(true)}>新建</Button>
      <Modal
        title="新建用户"
        visible={visible}
        onOk={async () => {
          const values = await form.validate();
          await createUser(values);
          setVisible(false);
          form.resetFields();
        }}
        onCancel={() => setVisible(false)}
        afterClose={() => form.resetFields()}  // 关闭后重置
      >
        <Form form={form} layout="vertical">
          <Form.Item field="name" label="姓名" rules={[{ required: true }]}>
            <Input />
          </Form.Item>
        </Form>
      </Modal>
    </>
  );
}
```

## 自定义校验规则

```tsx
const rules = {
  password: [
    { required: true, message: '请输入密码' },
    { minLength: 8, message: '密码不少于8位' },
    {
      validator: (value, callback) => {
        if (!/[A-Z]/.test(value)) callback('需要包含大写字母');
        if (!/[0-9]/.test(value)) callback('需要包含数字');
      },
    },
  ],
  confirmPassword: [
    { required: true },
    {
      validator: (value, callback) => {
        if (value !== form.getFieldValue('password')) {
          callback('两次密码不一致');
        }
      },
    },
  ],
};
```

## 最佳实践总结

1. **始终使用 `Form.useForm()`** 获取 form 实例
2. **`initialValues` 在 Form 上设置**，而非每个 Item 的 `initialValue`
3. **`scrollToFirstError` 对长表单必备**
4. **弹窗表单在 `afterClose` 中 `resetFields`**
5. **分步表单使用 `form.validate(fields)` 局部校验**
6. **`Form.useWatch` 替代 `onValuesChange`** 实现条件渲染
7. **使用 `noStyle` 的 Form.Item** 做内联多字段布局

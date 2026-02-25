---
name: arco-architecture
description: Arco Design 组件架构与设计模式。当需要理解组件目录结构、受控/非受控模式、Props 合并优先级、子组件模式或 Ref 转发等内部机制时使用。
user-invocable: false
---

# 架构与设计模式

## 组件目录结构

每个组件遵循统一的目录结构：

```
ComponentName/
├── index.tsx           # 入口，组装子组件并导出
├── interface.ts(x)     # TypeScript 接口定义（Props、Ref 等）
├── component-name.tsx  # 核心实现
├── style/              # Less 样式文件
│   └── index.less
├── __demo__/           # 示例 Markdown 文件
├── __test__/           # Jest 测试用例
├── __template__/       # 文档模板
├── __changelog__/      # 组件变更日志
├── README.en-US.md     # 英文文档
└── README.zh-CN.md     # 中文文档
```

## 导入导出模式

所有组件统一从 `components/index.tsx` 导出：

```tsx
// 导出组件
export { default as Button } from './Button';
// 同时导出类型
export type { ButtonProps } from './Button/interface';
```

使用时：

```tsx
import { Button, Select, Table } from '@arco-design/web-react';
import type { ButtonProps, SelectProps, TableProps } from '@arco-design/web-react';
```

## 受控与非受控模式

**核心原则**：所有有状态的组件同时支持受控和非受控两种模式。

### 命名约定

| 非受控（默认值） | 受控（当前值） | 变更回调 |
|----------------|--------------|---------|
| `defaultValue` | `value` | `onChange` |
| `defaultVisible` | `visible` | `onVisibleChange` |
| `defaultActiveKey` | `activeKey` | `onChange` |
| `defaultSelectedKeys` | `selectedKeys` | `onSelect` |
| `defaultExpandedKeys` | `expandedKeys` | `onExpand` |
| `defaultChecked` | `checked` | `onChange` |
| `defaultCurrentPage` | `current` | `onChange` |

### 使用方式

```tsx
// 非受控 —— 组件内部管理状态
<Select defaultValue="option1" onChange={(val) => console.log(val)} />

// 受控 —— 外部管理状态
const [value, setValue] = useState('option1');
<Select value={value} onChange={setValue} />
```

### 内部实现：`useMergeValue` Hook

组件内部使用 `useMergeValue` hook 统一处理两种模式：

```tsx
// 简化版实现逻辑
const [value, setValue] = useMergeValue(defaultValue, {
  value: propValue,      // 受控值
  defaultValue,          // 非受控默认值
});
```

## Props 合并优先级

组件 props 的合并顺序（优先级从低到高）：

1. **组件内部默认值** — 组件 `defaultProps` 或 `useMergeProps` 默认值
2. **ConfigProvider.componentConfig** — 全局默认 props
3. **组件实例 props** — 使用者直接传入的 props

```tsx
// 优先级: componentConfig.Button.type < 这里传入的 type
<ConfigProvider componentConfig={{ Button: { type: 'primary' } }}>
  <Button type="secondary">此按钮为 secondary</Button>
  <Button>此按钮为 primary（来自 componentConfig）</Button>
</ConfigProvider>
```

## 子组件模式

复合组件通过静态属性挂载子组件：

```tsx
// 点号访问子组件
<Select>
  <Select.Option value="a">A</Select.Option>
  <Select.OptGroup label="Group">
    <Select.Option value="b">B</Select.Option>
  </Select.OptGroup>
</Select>

<Form form={form}>
  <Form.Item field="name" rules={[{ required: true }]}>
    <Input />
  </Form.Item>
  <Form.List field="users">
    {(fields) => fields.map(/* ... */)}
  </Form.List>
</Form>

<Layout>
  <Layout.Header />
  <Layout>
    <Layout.Sider />
    <Layout.Content />
  </Layout>
  <Layout.Footer />
</Layout>

<Menu>
  <Menu.Item key="1">菜单项</Menu.Item>
  <Menu.SubMenu key="sub" title="子菜单">
    <Menu.Item key="2">子项</Menu.Item>
  </Menu.SubMenu>
  <Menu.ItemGroup title="分组">
    <Menu.Item key="3">分组项</Menu.Item>
  </Menu.ItemGroup>
</Menu>
```

## Ref 转发

组件通过 `React.forwardRef` 暴露 Ref，提供命令式操作：

```tsx
// Select Ref
const selectRef = useRef<SelectHandle>(null);
selectRef.current.focus();
selectRef.current.blur();
selectRef.current.getOptionInfoList();  // 获取所有选项信息

// Form Ref / useForm
const [form] = Form.useForm();
form.setFieldsValue({ name: 'Arco' });
form.validate();
form.resetFields();
form.getFieldsValue();

// Table Ref
const tableRef = useRef<TableInstance>(null);
tableRef.current.scrollIntoView('rowKey');

// Input Ref
const inputRef = useRef<RefInputType>(null);
inputRef.current.focus();
inputRef.current.blur();
inputRef.current.dom;  // 获取原生 input DOM
```

## CSS 命名约定

CSS 类名遵循 BEM-like 命名（可通过 `prefixCls` 自定义前缀）：

```
{prefix}-{component}                    → arco-btn
{prefix}-{component}-{modifier}         → arco-btn-primary
{prefix}-{component}-{element}          → arco-btn-icon
{prefix}-{component}-{element}-{mod}    → arco-table-header-fixed
{prefix}-{component}-size-{size}        → arco-btn-size-large
```

## 构建产物

| 目录 | 格式 | 用途 |
|------|------|------|
| `es/` | ESM | 现代打包工具（Vite、Webpack 5+） |
| `lib/` | CJS | Node.js / 旧打包工具 |
| `dist/` | UMD | CDN / 直接 `<script>` 引入 |

每个组件在 `es/` 和 `lib/` 下都有独立目录，支持按需加载。

## 内部共享模块

| 模块 | 位置 | 说明 |
|------|------|------|
| `VirtualList` | `_class/VirtualList/` | 虚拟滚动列表（Table、Select、Tree 共用） |
| `Draggable` | `_class/Draggable/` | 拖拽基础组件 |
| `SelectView` | `_class/select-view.tsx` | 共享选择器输入框（Select、Cascader、TreeSelect） |
| `Notice` | `_class/notice.tsx` | 通知基础组件（Message、Notification） |
| `Picker` | `_class/picker/` | 日期/时间选择器输入框 |
| Hooks | `_util/hooks/` | 22 个内部 Hooks |
| Utils | `_util/` | 类型判断、DOM 操作、颜色处理等工具 |

## 最佳实践

1. **始终从主入口导入** `@arco-design/web-react`，配合 tree-shaking
2. **类型导入使用 `import type`**，避免在运行时引入不必要的模块
3. **优先使用非受控模式**，除非需要外部管理状态（如表单联动）
4. **善用 ConfigProvider** 减少重复配置
5. **使用 Ref API** 进行命令式操作，而非直接操作 DOM

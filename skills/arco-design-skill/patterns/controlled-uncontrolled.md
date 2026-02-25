---
name: arco-controlled-uncontrolled
description: Arco Design 受控与非受控模式指南。当需要理解或选择组件的受控（value）和非受控（defaultValue）状态管理方式时使用。
user-invocable: false
---

# 受控与非受控模式

## 核心概念

Arco Design 中所有有状态的组件同时支持**受控**和**非受控**两种模式。

### 非受控模式（推荐简单场景）

组件内部管理自身状态，通过 `defaultXxx` 设置初始值：

```tsx
// 组件自己管理 value 状态
<Input defaultValue="初始值" onChange={(val) => console.log(val)} />
<Select defaultValue="option1" onChange={(val) => console.log(val)} />
<DatePicker defaultValue="2024-01-01" />
<Checkbox defaultChecked />
<Switch defaultChecked />
<Tabs defaultActiveTab="1">...</Tabs>
```

### 受控模式（需要外部管理状态）

外部通过 state 完全控制组件状态：

```tsx
const [value, setValue] = useState('初始值');
<Input value={value} onChange={setValue} />

const [checked, setChecked] = useState(true);
<Switch checked={checked} onChange={setChecked} />

const [visible, setVisible] = useState(false);
<Modal visible={visible} onCancel={() => setVisible(false)}>...</Modal>
```

## 何时使用受控

| 场景 | 模式 | 说明 |
|------|------|------|
| 简单的独立控件 | 非受控 | 不需要读取或操控状态 |
| 表单 (Form.Item 内) | 非受控 | Form 内部管理状态 |
| 组件间联动 | 受控 | 一个控件影响另一个 |
| 外部重置/赋值 | 受控 | 需要 setState 改变值 |
| 与 URL 参数同步 | 受控 | 值来源于 URL |
| 格式化/拦截输入 | 受控 | onChange 中过滤/转换值 |

## 常见命名约定

| 组件 | 非受控 | 受控 | 回调 |
|------|--------|------|------|
| Input | `defaultValue` | `value` | `onChange` |
| Select | `defaultValue` | `value` | `onChange` |
| DatePicker | `defaultValue` | `value` | `onChange` |
| Checkbox | `defaultChecked` | `checked` | `onChange` |
| Switch | `defaultChecked` | `checked` | `onChange` |
| Modal | — | `visible` | `onCancel` |
| Drawer | — | `visible` | `onCancel` |
| Collapse | `defaultActiveKey` | `activeKey` | `onChange` |
| Tabs | `defaultActiveTab` | `activeTab` | `onChange` |
| Tree | `defaultExpandedKeys` | `expandedKeys` | `onExpand` |
| Tree | `defaultSelectedKeys` | `selectedKeys` | `onSelect` |
| Tree | `defaultCheckedKeys` | `checkedKeys` | `onCheck` |
| Pagination | `defaultCurrent` | `current` | `onChange` |
| Tooltip | `defaultPopupVisible` | `popupVisible` | `onVisibleChange` |
| Menu | `defaultSelectedKeys` | `selectedKeys` | `onClickMenuItem` |
| Menu | `defaultOpenKeys` | `openKeys` | `onClickSubMenu` |

## 在 Form 中的受控模式

Form.Item 自动管理子组件的 value/onChange，不需要手动受控：

```tsx
// ✅ 正确：让 Form 管理
<Form.Item field="name">
  <Input />
</Form.Item>

// ❌ 错误：不要在 Form.Item 内同时手动受控
<Form.Item field="name">
  <Input value={value} onChange={setValue} />
</Form.Item>
```

### 特殊 Props 映射

某些组件使用 `checked` 而非 `value`：

```tsx
// Switch 在 Form 中
<Form.Item field="enabled" triggerPropName="checked">
  <Switch />
</Form.Item>

// Checkbox 在 Form 中
<Form.Item field="agree" triggerPropName="checked">
  <Checkbox>我同意协议</Checkbox>
</Form.Item>

// Upload 在 Form 中
<Form.Item field="files" triggerPropName="fileList">
  <Upload action="/upload" />
</Form.Item>
```

## 最佳实践

1. **简单场景优先使用非受控** — 减少代码量
2. **Form 内的控件不需要手动受控** — Form 会自动管理
3. **联动场景必须受控** — 一个控件值影响另一个的选项
4. **受控模式必须同时提供 value 和 onChange** — 否则组件不可编辑
5. **`triggerPropName` 处理特殊控件** — Switch、Checkbox 等

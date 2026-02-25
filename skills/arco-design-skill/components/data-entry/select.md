---
name: arco-select
description: Arco Select 选择器组件用法与 API。当需要下拉选择、多选、搜索选择、远程搜索、分组选项或虚拟滚动长列表时使用。
user-invocable: false
---

# Select 选择器

下拉选择组件，支持单选、多选、搜索、创建、虚拟滚动。

## 基本用法

```tsx
import { Select } from '@arco-design/web-react';
const Option = Select.Option;

// 基本单选
<Select placeholder="请选择" style={{ width: 200 }}>
  <Option value="beijing">北京</Option>
  <Option value="shanghai">上海</Option>
  <Option value="guangzhou">广州</Option>
</Select>

// 使用 options 数据
<Select
  options={['北京', '上海', '广州']}
  placeholder="请选择"
  style={{ width: 200 }}
/>

// 结构化 options
<Select
  options={[
    { label: '北京', value: 'beijing' },
    { label: '上海', value: 'shanghai', disabled: true },
    { label: '广州', value: 'guangzhou' },
  ]}
/>
```

## API

### SelectProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string \| string[] \| LabeledValue \| LabeledValue[]` | — | 受控值 |
| `defaultValue` | 同上 | — | 默认值 |
| `mode` | `'multiple' \| 'tags'` | — | 多选 / 标签创建模式 |
| `options` | `(string \| number \| OptionInfo)[]` | — | 数据化选项 |
| `labelInValue` | `boolean` | — | 值为 `{ label, value }` 格式 |
| `placeholder` | `string` | — | 占位文字 |
| `allowClear` | `boolean` | — | 允许清除 |
| `allowCreate` | `boolean` | — | 允许创建新选项 |
| `showSearch` | `boolean` | — | 可搜索 |
| `filterOption` | `boolean \| (inputValue, option) => boolean` | `true` | 本地搜索过滤 |
| `onSearch` | `(value: string) => void` | — | 搜索回调（远程搜索） |
| `loading` | `boolean` | — | 加载中 |
| `disabled` | `boolean` | — | 禁用 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | — | 尺寸 |
| `bordered` | `boolean` | `true` | 显示边框 |
| `maxTagCount` | `number` | — | 多选时最多显示标签数 |
| `virtualListProps` | `AvailableVirtualListProps` | — | 虚拟滚动配置 |
| `triggerProps` | `TriggerProps` | — | 下拉框触发器属性 |
| `dropdownMenuStyle` | `CSSProperties` | — | 下拉菜单样式 |
| `dropdownRender` | `(menu: ReactNode) => ReactNode` | — | 自定义下拉内容 |
| `triggerElement` | `ReactNode` | — | 自定义触发元素 |
| `onChange` | `(value, option) => void` | — | 值变化回调 |
| `onVisibleChange` | `(visible: boolean) => void` | — | 下拉可见性变化 |
| `onDeselect` | `(value, option) => void` | — | 取消选中回调 |

### Select.Option Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `value` | `string \| number` | 选项值 |
| `disabled` | `boolean` | 禁用 |
| `extra` | `any` | 附加数据 |

### Select.OptGroup Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `label` | `ReactNode` | 分组标签 |

### SelectHandle (Ref)

```tsx
const ref = useRef<SelectHandle>(null);
ref.current.focus();
ref.current.blur();
ref.current.getOptionInfoList();     // 获取所有选项
ref.current.activeOptionValue;        // 当前高亮选项值
ref.current.scrollIntoView(value);    // 滚动到指定选项
```

## 常用模式

### 远程搜索

```tsx
function RemoteSelect() {
  const [options, setOptions] = useState([]);
  const [loading, setLoading] = useState(false);

  const handleSearch = async (value) => {
    if (!value) return;
    setLoading(true);
    const data = await fetchOptions(value);
    setOptions(data.map(d => ({ label: d.name, value: d.id })));
    setLoading(false);
  };

  return (
    <Select
      showSearch
      filterOption={false}  // 禁用本地过滤
      options={options}
      onSearch={handleSearch}
      loading={loading}
      placeholder="搜索用户"
    />
  );
}
```

### 多选 + 标签模式

```tsx
// 多选
<Select mode="multiple" maxTagCount={3} placeholder="选择标签">
  <Option value="red">红色</Option>
  <Option value="blue">蓝色</Option>
  <Option value="green">绿色</Option>
</Select>

// 标签创建模式（可输入新选项）
<Select mode="tags" placeholder="输入标签" allowCreate />
```

### 自定义下拉内容

```tsx
<Select
  dropdownRender={(menu) => (
    <div>
      {menu}
      <Divider style={{ margin: '4px 0' }} />
      <div style={{ padding: '4px 8px' }}>
        <Button type="text" size="small" onClick={addNewOption}>
          <IconPlus /> 新增选项
        </Button>
      </div>
    </div>
  )}
>
  {options.map(opt => <Option key={opt} value={opt}>{opt}</Option>)}
</Select>
```

### 虚拟滚动（大数据量）

```tsx
<Select
  virtualListProps={{ height: 200 }}
  options={Array.from({ length: 10000 }, (_, i) => ({
    label: `选项 ${i}`,
    value: i,
  }))}
/>
```

## 最佳实践

1. **数据量大时使用 `virtualListProps`** 开启虚拟滚动
2. **远程搜索设置 `filterOption={false}`** 禁用本地过滤
3. **使用 `labelInValue`** 当需要同时获取 label 和 value 时
4. **`maxTagCount` 控制多选标签显示数量**，避免撑开容器
5. **`allowClear` 通常应开启**，让用户可以清除选择
6. **分组使用 `OptGroup`**，大量选项时提升可读性

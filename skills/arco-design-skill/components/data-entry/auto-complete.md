---
name: arco-auto-complete
description: Arco AutoComplete 自动补全组件用法与 API。当需要输入时自动提示候选项或搜索建议时使用。
user-invocable: false
---

# AutoComplete 自动补全

输入框自动补全组件。

```tsx
import { AutoComplete } from '@arco-design/web-react';

<AutoComplete
  placeholder="请输入"
  data={['北京', '上海', '广州', '深圳']}
  style={{ width: 300 }}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `data` | `(string \| { value, name })[]` | 数据源 |
| `filterOption` | `boolean \| (inputValue, option) => boolean` | 过滤函数 |
| `triggerElement` | `ReactNode` | 自定义触发元素 |
| `onSearch` | `(value: string) => void` | 搜索回调 |
| `onSelect` | `(value: string) => void` | 选中回调 |
| `virtualListProps` | `object` | 虚拟滚动 |

## 常用模式

```tsx
// 远程搜索
const [options, setOptions] = useState([]);
<AutoComplete
  placeholder="搜索用户"
  data={options}
  onSearch={async (value) => {
    const result = await searchAPI(value);
    setOptions(result.map(item => item.name));
  }}
  onSelect={(value) => navigate(`/user/${value}`)}
/>

// 对象格式数据
<AutoComplete
  data={[
    { value: 'bj', name: '北京' },
    { value: 'sh', name: '上海' },
  ]}
  filterOption={(inputValue, option) =>
    option.props.children.toLowerCase().includes(inputValue.toLowerCase())
  }
/>

// 自定义触发元素
<AutoComplete
  data={suggestions}
  triggerElement={<Input.Search placeholder="搜索..." />}
/>
```

## 完整 API

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `data` | `(string \| { value, name })[]` | — | 数据源 |
| `value` / `defaultValue` | `string` | — | 值 |
| `placeholder` | `string` | — | 占位文字 |
| `filterOption` | `boolean \| (inputValue, option) => boolean` | `true` | 过滤函数（false 禁用过滤） |
| `triggerElement` | `ReactNode` | — | 自定义触发元素 |
| `defaultActiveFirstOption` | `boolean` | `true` | 默认高亮第一项 |
| `allowClear` | `boolean` | — | 可清除 |
| `disabled` | `boolean` | — | 禁用 |
| `virtualListProps` | `object` | — | 虚拟滚动配置 |
| `dropdownRender` | `(menu) => ReactNode` | — | 自定义下拉框 |
| `onSearch` | `(value: string) => void` | — | 搜索回调 |
| `onSelect` | `(value: string, option) => void` | — | 选中回调 |
| `onChange` | `(value: string) => void` | — | 值变化 |
| `onFocus` | `(e) => void` | — | 聚焦 |
| `onBlur` | `(e) => void` | — | 失焦 |

## 最佳实践

1. **远程搜索时设 filterOption={false}** —— 由后端过滤，前端不二次过滤
2. **加防抖** —— onSearch 配合 lodash.debounce 避免频繁请求
3. **与 Select + showSearch 的区别** —— AutoComplete 更适合自由文本输入 + 建议，Select 适合从固定选项中选择

---
name: arco-config-provider
description: ConfigProvider 全局配置指南。当需要统一设置组件尺寸、主题色、语言、默认 props 或给所有组件注入统一配置时使用。
user-invocable: false
---

# 全局配置 ConfigProvider

`ConfigProvider` 用于全局配置所有组件的默认行为，包括主题、尺寸、语言、默认 props 等。

## 基本用法

```tsx
import { ConfigProvider, Button, DatePicker } from '@arco-design/web-react';
import enUS from '@arco-design/web-react/es/locale/en-US';

function App() {
  return (
    <ConfigProvider locale={enUS} size="large">
      <Button type="primary">Large Button</Button>
      <DatePicker />
    </ConfigProvider>
  );
}
```

## 核心 API

### ConfigProviderProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `locale` | `Locale` | 中文 | 语言包 |
| `theme` | `Record<string, any>` | — | CSS 变量主题对象 |
| `size` | `'mini' \| 'small' \| 'default' \| 'large'` | `'default'` | 全局组件尺寸 |
| `prefixCls` | `string` | `'arco'` | 全局 CSS 类名前缀 |
| `rtl` | `boolean` | `false` | 从右到左布局（RTL） |
| `componentConfig` | `ComponentConfig` | — | 全局组件默认 props |
| `getPopupContainer` | `(node: HTMLElement) => Element` | — | 全局弹出层挂载节点 |
| `loadingElement` | `ReactNode` | — | 全局加载动画元素 |
| `tablePagination` | `PaginationProps` | — | 全局表格分页配置 |
| `renderEmpty` | `(componentName?: string) => ReactNode` | — | 全局空状态渲染 |
| `focusLock` | `{ modal?: boolean; drawer?: boolean }` | — | 全局焦点锁定设置 |
| `autoInsertSpaceInButton` | `boolean` | `true` | 按钮中中文字符间自动插入空格 |
| `effectGlobalModal` | `boolean` | `true` | 是否影响全局 Modal 配置 |
| `effectGlobalNotification` | `boolean` | `true` | 是否影响全局 Notification 配置 |
| `effectGlobalMessage` | `boolean` | `true` | 是否影响全局 Message 配置 |

## 全局组件默认 Props

通过 `componentConfig` 可以为任意组件设置默认 props，覆盖组件自身默认值：

```tsx
<ConfigProvider
  componentConfig={{
    Button: {
      type: 'primary',
      shape: 'round',
    },
    Table: {
      border: true,
      stripe: true,
      pagePosition: 'bottomCenter',
    },
    Modal: {
      maskClosable: false,
      escToExit: false,
    },
    Select: {
      allowClear: true,
      placeholder: '请选择...',
    },
    Input: {
      allowClear: true,
    },
    DatePicker: {
      allowClear: true,
    },
  }}
>
  {children}
</ConfigProvider>
```

**`componentConfig` 支持所有组件**，key 为组件名（PascalCase），value 为该组件的 Props 类型。

## 嵌套使用

`ConfigProvider` 支持嵌套，内层配置会覆盖外层：

```tsx
<ConfigProvider size="large" locale={zhCN}>
  {/* 这里的组件都是 large + 中文 */}
  <ConfigProvider size="small">
    {/* 这里的组件是 small + 中文（继承外层 locale） */}
  </ConfigProvider>
</ConfigProvider>
```

## 全局弹出层容器

```tsx
// 所有 Popover、Select 下拉、DatePicker 面板等挂载到指定容器
<ConfigProvider getPopupContainer={(triggerNode) => triggerNode.parentElement}>
  <Select options={options} />
</ConfigProvider>
```

## 最佳实践

1. **在应用根节点包裹 `ConfigProvider`**，统一管理全局配置
2. **使用 `componentConfig` 统一风格**，避免在每个组件上重复设置相同的 props
3. **主题变量通过 `theme` 属性注入**，而非手动覆盖 CSS
4. **RTL 支持**：设置 `rtl={true}` 配合 RTL CSS 文件即可实现从右到左布局
5. **生产环境建议设置 `prefixCls`** 避免与其他 UI 库的类名冲突

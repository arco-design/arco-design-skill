---
name: arco-menu
description: Arco Menu 导航菜单组件用法与 API。当需要创建侧边栏菜单、顶部导航栏、多级菜单或可折叠菜单时使用。
user-invocable: false
---

# Menu 导航菜单

用于页面导航的菜单组件，支持垂直、水平、弹出等模式。

## 基本用法

```tsx
import { Menu } from '@arco-design/web-react';
const MenuItem = Menu.Item;
const SubMenu = Menu.SubMenu;
const ItemGroup = Menu.ItemGroup;

// 水平菜单
<Menu mode="horizontal" defaultSelectedKeys={['1']}>
  <MenuItem key="1"><IconHome /> 首页</MenuItem>
  <MenuItem key="2"><IconApps /> 应用</MenuItem>
  <SubMenu key="sub" title={<><IconSettings /> 设置</>}>
    <MenuItem key="3">个人设置</MenuItem>
    <MenuItem key="4">系统设置</MenuItem>
  </SubMenu>
</Menu>

// 垂直菜单（侧边栏）
<Menu style={{ width: 200 }} defaultOpenKeys={['sub']} defaultSelectedKeys={['1']}>
  <MenuItem key="1"><IconHome /> 首页</MenuItem>
  <SubMenu key="sub" title={<><IconApps /> 应用</>}>
    <MenuItem key="2">应用列表</MenuItem>
    <MenuItem key="3">应用详情</MenuItem>
  </SubMenu>
  <ItemGroup title="更多">
    <MenuItem key="4">关于</MenuItem>
  </ItemGroup>
</Menu>
```

## API

### MenuProps

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `mode` | `'vertical' \| 'horizontal' \| 'pop' \| 'popButton'` | `'vertical'` | 菜单模式 |
| `theme` | `'light' \| 'dark'` | `'light'` | 主题 |
| `selectedKeys` / `defaultSelectedKeys` | `string[]` | — | 选中的菜单项 |
| `openKeys` / `defaultOpenKeys` | `string[]` | — | 展开的子菜单 |
| `collapse` | `boolean` | — | 收起菜单（垂直模式） |
| `accordion` | `boolean` | — | 手风琴模式 |
| `levelIndent` | `number` | — | 层级缩进 |
| `autoOpen` | `boolean` | — | 默认展开选中项父菜单 |
| `autoScrollIntoView` | `boolean` | — | 自动滚动到选中项 |
| `hasCollapseButton` | `boolean` | — | 显示收起按钮 |
| `icons` | `{ horizontalArrowDown, popArrowRight, collapseDefault, collapseActive }` | — | 自定义图标 |
| `ellipsis` | `boolean` | `true` | 水平模式溢出省略 |
| `onClickMenuItem` | `(key, event, keyPath) => void` | — | 点击菜单项 |
| `onClickSubMenu` | `(key, openKeys, keyPath) => void` | — | 点击子菜单 |
| `onCollapseChange` | `(collapse) => void` | — | 收起变化 |

### Menu.Item Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `key` | `string` | 唯一标识 |
| `disabled` | `boolean` | 禁用 |
| `wrapper` | `string` | 外层元素标签 |

### Menu.SubMenu Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `key` | `string` | 唯一标识 |
| `title` | `ReactNode` | 子菜单标题 |
| `selectable` | `boolean` | 子菜单本身可选 |

## 常用模式

```tsx
// 配合 Layout.Sider 使用
<Layout.Sider collapsible collapsed={collapsed} onCollapse={setCollapsed}>
  <Menu collapse={collapsed} selectedKeys={[currentPath]}>
    {menuItems.map(item => (
      <MenuItem key={item.path} onClick={() => navigate(item.path)}>
        {item.icon} {item.title}
      </MenuItem>
    ))}
  </Menu>
</Layout.Sider>

// 弹出菜单模式
<Menu mode="pop" style={{ width: 200 }}>
  <SubMenu key="1" title="子菜单">
    <MenuItem key="1-1">选项1</MenuItem>
    <MenuItem key="1-2">选项2</MenuItem>
  </SubMenu>
</Menu>
```



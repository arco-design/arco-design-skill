---
name: arco-getting-started
description: Arco Design 安装与项目初始化指南。当需要安装 @arco-design/web-react、配置按需加载、引入样式或设置 TypeScript 时使用。
user-invocable: false
---

# 快速开始

## 安装

```bash
# npm
npm install @arco-design/web-react

# yarn
yarn add @arco-design/web-react

# pnpm
pnpm add @arco-design/web-react
```

**Peer Dependencies**: `react >= 16`、`react-dom >= 16`

## 全量引入

```tsx
import React from 'react';
import { Button, Input, Select } from '@arco-design/web-react';
import '@arco-design/web-react/dist/css/arco.css';

function App() {
  return (
    <div>
      <Button type="primary">Hello Arco</Button>
    </div>
  );
}
```

## 按需加载（推荐）

### 方式一：使用 babel-plugin-import

```bash
npm install babel-plugin-import --save-dev
```

```json
// .babelrc 或 babel.config.js
{
  "plugins": [
    ["import", { "libraryName": "@arco-design/web-react", "libraryDirectory": "es", "style": true }]
  ]
}
```

### 方式二：使用 ESM tree-shaking

直接从 `@arco-design/web-react/es` 导入，配合构建工具的 tree-shaking 能力：

```tsx
import Button from '@arco-design/web-react/es/Button';
import '@arco-design/web-react/es/Button/style/css';
```

## 图标库

图标作为独立包发布：

```bash
npm install @arco-design/web-react-icon
```

```tsx
import { IconSearch, IconPlus } from '@arco-design/web-react/icon';

<Button icon={<IconSearch />}>搜索</Button>
```

## TypeScript 支持

Arco Design 使用 TypeScript 编写，内置完整类型定义，无需额外安装 `@types`。

```tsx
import type { ButtonProps, SelectProps, TableProps } from '@arco-design/web-react';
```

所有组件 Props 类型均可通过 `import type { XxxProps }` 导入。

## 浏览器兼容性

支持所有现代浏览器及 IE11+（需 polyfill）。

| 浏览器 | 版本 |
|--------|------|
| Chrome | 最新 2 个版本 |
| Firefox | 最新 2 个版本 |
| Safari | 最新 2 个版本 |
| Edge | 最新 2 个版本 |
| IE | 11 (需 polyfill) |

## 关键依赖

| 依赖 | 用途 |
|------|------|
| `dayjs` | 日期时间处理（替代 Moment.js，体积更小） |
| `lodash` | 工具函数库 |
| `react-transition-group` | CSS 过渡动画 |
| `b-validate` | 表单校验引擎 |
| `react-focus-lock` | 焦点锁定（Modal/Drawer） |

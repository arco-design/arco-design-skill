---
name: arco-design
description: Arco Design React 组件库完整参考。当用户使用 @arco-design/web-react 进行开发时，根据需要加载对应的组件、模式或 Hooks 参考文件。
---

# Arco Design React 组件库 Skills

`@arco-design/web-react` — 字节跳动 ArcoDesign 团队出品的企业级 React UI 组件库。

## 关键规范

- **导入**: `import { Button, Table, Form } from '@arco-design/web-react'`
- **图标**: `import { IconXxx } from '@arco-design/web-react/icon'`
- **类型**: `import type { ButtonProps } from '@arco-design/web-react'`
- **样式**: 全量 `import '@arco-design/web-react/dist/css/arco.css'` 或按需加载
- **日期库**: dayjs（非 moment）
- **受控模式**: `value` + `onChange`；非受控模式: `defaultValue`
- **子组件**: 通过 `Component.SubComponent` 访问，如 `Form.Item`、`Select.Option`、`Menu.SubMenu`

## 如何使用此 Skill 集

当需要使用 Arco Design 组件时，根据具体需求加载对应的参考文件：

### 项目初始化时
- [快速开始](overview/getting-started.md) — 安装、引入、按需加载配置
- [全局配置 ConfigProvider](overview/config-provider.md) — 统一设置尺寸、主题、语言
- [主题定制](overview/theming.md) — CSS 变量、Less 变量、暗色模式
- [国际化 i18n](overview/internationalization.md) — 多语言切换

### 需要理解组件机制时
- [架构与设计模式](overview/architecture.md) — 受控/非受控、Props 合并、Ref 转发、CSS 命名

### 使用具体组件时

加载对应组件文件获取完整 API 和示例：

| 分类 | 组件 |
|------|------|
| **通用** | [Button](components/general/button.md), [Icon](components/general/icon.md), [Typography](components/general/typography.md), [Link](components/general/link.md), [Divider](components/general/divider.md) |
| **布局** | [Grid](components/layout/grid.md), [Layout](components/layout/layout.md), [Space](components/layout/space.md) |
| **导航** | [Menu](components/navigation/menu.md), [Tabs](components/navigation/tabs.md), [Dropdown](components/navigation/dropdown.md), [Breadcrumb](components/navigation/breadcrumb.md), [Pagination](components/navigation/pagination.md), [Steps](components/navigation/steps.md), [Affix](components/navigation/affix.md), [Anchor](components/navigation/anchor.md), [PageHeader](components/navigation/page-header.md) |
| **数据录入** | [Form](components/data-entry/form.md), [Input](components/data-entry/input.md), [Select](components/data-entry/select.md), [DatePicker](components/data-entry/date-picker.md), [TimePicker](components/data-entry/time-picker.md), [InputNumber](components/data-entry/input-number.md), [Checkbox](components/data-entry/checkbox.md), [Radio](components/data-entry/radio.md), [Switch](components/data-entry/switch.md), [Slider](components/data-entry/slider.md), [Rate](components/data-entry/rate.md), [Cascader](components/data-entry/cascader.md), [TreeSelect](components/data-entry/tree-select.md), [Transfer](components/data-entry/transfer.md), [AutoComplete](components/data-entry/auto-complete.md), [Mentions](components/data-entry/mentions.md), [InputTag](components/data-entry/input-tag.md), [Upload](components/data-entry/upload.md), [ColorPicker](components/data-entry/color-picker.md), [VerificationCode](components/data-entry/verification-code.md) |
| **数据展示** | [Table](components/data-display/table.md), [List](components/data-display/list.md), [Card](components/data-display/card.md), [Tree](components/data-display/tree.md), [Tooltip](components/data-display/tooltip.md), [Popover](components/data-display/popover.md), [Avatar](components/data-display/avatar.md), [Badge](components/data-display/badge.md), [Tag](components/data-display/tag.md), [Carousel](components/data-display/carousel.md), [Collapse](components/data-display/collapse.md), [Descriptions](components/data-display/descriptions.md), [Calendar](components/data-display/calendar.md), [Comment](components/data-display/comment.md), [Empty](components/data-display/empty.md), [Image](components/data-display/image.md), [Statistic](components/data-display/statistic.md), [Timeline](components/data-display/timeline.md) |
| **反馈** | [Modal](components/feedback/modal.md), [Message](components/feedback/message.md), [Notification](components/feedback/notification.md), [Drawer](components/feedback/drawer.md), [Alert](components/feedback/alert.md), [Progress](components/feedback/progress.md), [Popconfirm](components/feedback/popconfirm.md), [Result](components/feedback/result.md), [Skeleton](components/feedback/skeleton.md), [Spin](components/feedback/spin.md) |
| **其他** | [BackTop](components/other/back-top.md), [Portal](components/other/portal.md), [ResizeBox](components/other/resize-box.md), [Trigger](components/other/trigger.md), [Watermark](components/other/watermark.md) |

### 实现复杂场景时
- [表单模式](patterns/form-patterns.md) — 动态表单、联动校验、嵌套表单、异步提交
- [表格模式](patterns/table-patterns.md) — 远程数据、可编辑行、虚拟滚动、自定义筛选
- [弹层模式](patterns/modal-patterns.md) — 表单弹窗、确认流程、嵌套抽屉
- [受控与非受控](patterns/controlled-uncontrolled.md) — 如何选择和切换两种模式
- [响应式设计](patterns/responsive-design.md) — Grid 断点、自适应布局

### 使用 Hooks 时
- [Hooks 参考](hooks/hooks.md) — 当需要使用验证码组件 useVerificationCode 用法、水印组件 useWatermark 用法时使用。

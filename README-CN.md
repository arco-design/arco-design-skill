[English](README.md) | **中文**

# Arco Design React Skills

> 基于 `@arco-design/web-react` 的完整组件库技能集，帮助 AI 准确使用 Arco Design 进行 React 开发。

## 这是什么

这是一套 **skills 文件集合**，覆盖了 [Arco Design](https://arco.design) React 组件库的：

- **70 个组件**的用法、API 参数、代码示例与最佳实践
- **5 篇概览文档**：安装、全局配置、主题定制、国际化、架构模式
- **5 篇模式指南**：表单、表格、弹窗、受控/非受控、响应式设计
- **2 篇 Hooks 参考**：useVerificationCode、useWatermark

AI 在编写使用 Arco Design 的代码时会自动加载相关 skill，获得准确的 API 信息和最佳实践指导。

## 目录结构

```
.skills/
├── README.md                          # 本文件
└── skills/
    └── arco-design/                   # Skill 主目录
        ├── SKILL.md                   #   入口文件（自动加载）
        ├── overview/                  #   概览与全局配置
        │   ├── getting-started.md     #     安装、引入、按需加载
        │   ├── config-provider.md     #     ConfigProvider 全局配置
        │   ├── theming.md             #     CSS 变量、Less 变量、暗色模式
        │   ├── internationalization.md #    多语言支持
        │   └── architecture.md        #     组件结构、受控/非受控、命名约定
        ├── components/                #   组件 Skills（按分类）
        │   ├── general/               #     通用：Button, Icon, Typography, Link, Divider
        │   ├── layout/                #     布局：Grid, Layout, Space
        │   ├── navigation/            #     导航：Menu, Tabs, Breadcrumb, Dropdown, Pagination...
        │   ├── data-entry/            #     数据录入：Form, Input, Select, DatePicker, Upload...
        │   ├── data-display/          #     数据展示：Table, List, Card, Tree, Tooltip...
        │   ├── feedback/              #     反馈：Modal, Message, Notification, Drawer...
        │   └── other/                 #     其他：Portal, Trigger, BackTop, Watermark, ResizeBox
        ├── patterns/                  #   常见模式
        │   ├── form-patterns.md       #     表单：动态表单、联动、自定义校验...
        │   ├── table-patterns.md      #     表格：远程数据、可编辑、虚拟滚动...
        │   ├── modal-patterns.md      #     弹窗：确认框、表单弹窗、抽屉...
        │   ├── controlled-uncontrolled.md # 受控与非受控模式
        │   └── responsive-design.md   #     响应式布局
        └── hooks/
            ├── use-verification-code.md #   useVerificationCode Hook
            └── use-watermark.md       #     useWatermark Hook
```

## 每个 Skill 文件包含

每个组件 skill 文件遵循统一结构：

1. **YAML Frontmatter** — `name`、`description`（场景触发型）、`user-invocable: false`
2. **基本用法** — 可直接运行的 TSX 代码示例
3. **API 表格** — 完整的 Props、Events、Methods 参考
4. **常用模式** — 真实场景下的代码片段
5. **最佳实践** — 使用建议与避坑指南

## Skill 入口

[skills/arco-design/SKILL.md](skills/arco-design/SKILL.md) 是主入口 skill，Claude Code 会自动加载。它包含：

- **关键编码规范**（import 模式、受控模式、子组件访问）
- **组件分类导航表**（按使用场景索引到各子 skill）
- **何时应引用哪个 skill** 的指引

所有子 skill 设置了 `user-invocable: false`，Claude 会根据 description 自动判断何时加载。

## 组件索引

### 通用 General
| 组件 | Skill 文件 | 说明 |
|------|-----------|------|
| Button | [button.md](skills/arco-design/components/general/button.md) | 按钮 |
| Icon | [icon.md](skills/arco-design/components/general/icon.md) | 图标 |
| Typography | [typography.md](skills/arco-design/components/general/typography.md) | 排版 |
| Link | [link.md](skills/arco-design/components/general/link.md) | 链接 |
| Divider | [divider.md](skills/arco-design/components/general/divider.md) | 分割线 |

### 布局 Layout
| 组件 | Skill 文件 | 说明 |
|------|-----------|------|
| Grid | [grid.md](skills/arco-design/components/layout/grid.md) | 栅格 |
| Layout | [layout.md](skills/arco-design/components/layout/layout.md) | 布局 |
| Space | [space.md](skills/arco-design/components/layout/space.md) | 间距 |

### 导航 Navigation
| 组件 | Skill 文件 | 说明 |
|------|-----------|------|
| Menu | [menu.md](skills/arco-design/components/navigation/menu.md) | 导航菜单 |
| Tabs | [tabs.md](skills/arco-design/components/navigation/tabs.md) | 标签页 |
| Dropdown | [dropdown.md](skills/arco-design/components/navigation/dropdown.md) | 下拉菜单 |
| Breadcrumb | [breadcrumb.md](skills/arco-design/components/navigation/breadcrumb.md) | 面包屑 |
| Pagination | [pagination.md](skills/arco-design/components/navigation/pagination.md) | 分页 |
| Steps | [steps.md](skills/arco-design/components/navigation/steps.md) | 步骤条 |
| Affix | [affix.md](skills/arco-design/components/navigation/affix.md) | 固钉 |
| Anchor | [anchor.md](skills/arco-design/components/navigation/anchor.md) | 锚点 |
| PageHeader | [page-header.md](skills/arco-design/components/navigation/page-header.md) | 页头 |

### 数据录入 Data Entry
| 组件 | Skill 文件 | 说明 |
|------|-----------|------|
| Form | [form.md](skills/arco-design/components/data-entry/form.md) | 表单 |
| Input | [input.md](skills/arco-design/components/data-entry/input.md) | 输入框 |
| Select | [select.md](skills/arco-design/components/data-entry/select.md) | 选择器 |
| DatePicker | [date-picker.md](skills/arco-design/components/data-entry/date-picker.md) | 日期选择 |
| TimePicker | [time-picker.md](skills/arco-design/components/data-entry/time-picker.md) | 时间选择 |
| InputNumber | [input-number.md](skills/arco-design/components/data-entry/input-number.md) | 数字输入 |
| Checkbox | [checkbox.md](skills/arco-design/components/data-entry/checkbox.md) | 复选框 |
| Radio | [radio.md](skills/arco-design/components/data-entry/radio.md) | 单选框 |
| Switch | [switch.md](skills/arco-design/components/data-entry/switch.md) | 开关 |
| Slider | [slider.md](skills/arco-design/components/data-entry/slider.md) | 滑动条 |
| Rate | [rate.md](skills/arco-design/components/data-entry/rate.md) | 评分 |
| Cascader | [cascader.md](skills/arco-design/components/data-entry/cascader.md) | 级联选择 |
| TreeSelect | [tree-select.md](skills/arco-design/components/data-entry/tree-select.md) | 树选择 |
| Transfer | [transfer.md](skills/arco-design/components/data-entry/transfer.md) | 穿梭框 |
| AutoComplete | [auto-complete.md](skills/arco-design/components/data-entry/auto-complete.md) | 自动补全 |
| Mentions | [mentions.md](skills/arco-design/components/data-entry/mentions.md) | 提及 |
| InputTag | [input-tag.md](skills/arco-design/components/data-entry/input-tag.md) | 标签输入 |
| Upload | [upload.md](skills/arco-design/components/data-entry/upload.md) | 上传 |
| ColorPicker | [color-picker.md](skills/arco-design/components/data-entry/color-picker.md) | 颜色选择 |
| VerificationCode | [verification-code.md](skills/arco-design/components/data-entry/verification-code.md) | 验证码 |

### 数据展示 Data Display
| 组件 | Skill 文件 | 说明 |
|------|-----------|------|
| Table | [table.md](skills/arco-design/components/data-display/table.md) | 表格 |
| List | [list.md](skills/arco-design/components/data-display/list.md) | 列表 |
| Card | [card.md](skills/arco-design/components/data-display/card.md) | 卡片 |
| Tree | [tree.md](skills/arco-design/components/data-display/tree.md) | 树 |
| Tooltip | [tooltip.md](skills/arco-design/components/data-display/tooltip.md) | 文字提示 |
| Popover | [popover.md](skills/arco-design/components/data-display/popover.md) | 气泡卡片 |
| Avatar | [avatar.md](skills/arco-design/components/data-display/avatar.md) | 头像 |
| Badge | [badge.md](skills/arco-design/components/data-display/badge.md) | 徽标 |
| Tag | [tag.md](skills/arco-design/components/data-display/tag.md) | 标签 |
| Carousel | [carousel.md](skills/arco-design/components/data-display/carousel.md) | 走马灯 |
| Collapse | [collapse.md](skills/arco-design/components/data-display/collapse.md) | 折叠面板 |
| Descriptions | [descriptions.md](skills/arco-design/components/data-display/descriptions.md) | 描述列表 |
| Calendar | [calendar.md](skills/arco-design/components/data-display/calendar.md) | 日历 |
| Comment | [comment.md](skills/arco-design/components/data-display/comment.md) | 评论 |
| Empty | [empty.md](skills/arco-design/components/data-display/empty.md) | 空状态 |
| Image | [image.md](skills/arco-design/components/data-display/image.md) | 图片 |
| Statistic | [statistic.md](skills/arco-design/components/data-display/statistic.md) | 统计数值 |
| Timeline | [timeline.md](skills/arco-design/components/data-display/timeline.md) | 时间线 |

### 反馈 Feedback
| 组件 | Skill 文件 | 说明 |
|------|-----------|------|
| Modal | [modal.md](skills/arco-design/components/feedback/modal.md) | 对话框 |
| Message | [message.md](skills/arco-design/components/feedback/message.md) | 全局消息 |
| Notification | [notification.md](skills/arco-design/components/feedback/notification.md) | 通知 |
| Drawer | [drawer.md](skills/arco-design/components/feedback/drawer.md) | 抽屉 |
| Alert | [alert.md](skills/arco-design/components/feedback/alert.md) | 警告 |
| Progress | [progress.md](skills/arco-design/components/feedback/progress.md) | 进度条 |
| Popconfirm | [popconfirm.md](skills/arco-design/components/feedback/popconfirm.md) | 气泡确认 |
| Result | [result.md](skills/arco-design/components/feedback/result.md) | 结果页 |
| Skeleton | [skeleton.md](skills/arco-design/components/feedback/skeleton.md) | 骨架屏 |
| Spin | [spin.md](skills/arco-design/components/feedback/spin.md) | 加载中 |

### 其他 Other
| 组件 | Skill 文件 | 说明 |
|------|-----------|------|
| BackTop | [back-top.md](skills/arco-design/components/other/back-top.md) | 回到顶部 |
| Portal | [portal.md](skills/arco-design/components/other/portal.md) | 传送门 |
| ResizeBox | [resize-box.md](skills/arco-design/components/other/resize-box.md) | 伸缩框 |
| Trigger | [trigger.md](skills/arco-design/components/other/trigger.md) | 触发器 |
| Watermark | [watermark.md](skills/arco-design/components/other/watermark.md) | 水印 |

### 模式与 Hooks
| 主题 | Skill 文件 | 说明 |
|------|-----------|------|
| 表单模式 | [form-patterns.md](skills/arco-design/patterns/form-patterns.md) | 动态表单、联动校验、异步提交 |
| 表格模式 | [table-patterns.md](skills/arco-design/patterns/table-patterns.md) | 远程数据、可编辑行、虚拟滚动 |
| 弹窗模式 | [modal-patterns.md](skills/arco-design/patterns/modal-patterns.md) | 确认框、表单弹窗、嵌套抽屉 |
| 受控与非受控 | [controlled-uncontrolled.md](skills/arco-design/patterns/controlled-uncontrolled.md) | 两种模式的选择与实现 |
| 响应式设计 | [responsive-design.md](skills/arco-design/patterns/responsive-design.md) | Grid 断点、自适应布局 |
| useVerificationCode | [use-verification-code.md](skills/arco-design/hooks/use-verification-code.md) | 自定义验证码输入 Hook |
| useWatermark | [use-watermark.md](skills/arco-design/hooks/use-watermark.md) | 动态水印 Hook |

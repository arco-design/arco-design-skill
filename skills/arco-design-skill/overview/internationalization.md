---
name: arco-internationalization
description: Arco Design 国际化（i18n）指南。当需要切换语言、添加多语言支持或自定义 locale 文案时使用。
user-invocable: false
---

# 国际化 i18n

Arco Design 内置多语言支持，通过 `ConfigProvider` 的 `locale` 属性切换语言。

## 支持的语言

| 语言包 | 语言 | 导入路径 |
|--------|------|----------|
| `zh-CN` | 简体中文（默认） | `@arco-design/web-react/es/locale/zh-CN` |
| `zh-TW` | 繁体中文（台湾） | `@arco-design/web-react/es/locale/zh-TW` |
| `zh-HK` | 繁体中文（香港） | `@arco-design/web-react/es/locale/zh-HK` |
| `en-US` | 英语 | `@arco-design/web-react/es/locale/en-US` |
| `ja-JP` | 日语 | `@arco-design/web-react/es/locale/ja-JP` |
| `ko-KR` | 韩语 | `@arco-design/web-react/es/locale/ko-KR` |
| `de-DE` | 德语 | `@arco-design/web-react/es/locale/de-DE` |
| `fr-FR` | 法语 | `@arco-design/web-react/es/locale/fr-FR` |
| `es-ES` | 西班牙语 | `@arco-design/web-react/es/locale/es-ES` |
| `it-IT` | 意大利语 | `@arco-design/web-react/es/locale/it-IT` |
| `pt-BR` | 葡萄牙语（巴西） | `@arco-design/web-react/es/locale/pt-BR` |
| `pt-PT` | 葡萄牙语（葡萄牙） | `@arco-design/web-react/es/locale/pt-PT` |
| `ru-RU` | 俄语 | `@arco-design/web-react/es/locale/ru-RU` |
| `ar-EG` | 阿拉伯语 | `@arco-design/web-react/es/locale/ar-EG` |
| `th-TH` | 泰语 | `@arco-design/web-react/es/locale/th-TH` |
| `tr-TR` | 土耳其语 | `@arco-design/web-react/es/locale/tr-TR` |
| `ms-MY` | 马来语 | `@arco-design/web-react/es/locale/ms-MY` |
| `vi-VN` | 越南语 | `@arco-design/web-react/es/locale/vi-VN` |
| `id-ID` | 印尼语 | `@arco-design/web-react/es/locale/id-ID` |

## 基本用法

```tsx
import { ConfigProvider } from '@arco-design/web-react';
import enUS from '@arco-design/web-react/es/locale/en-US';

function App() {
  return (
    <ConfigProvider locale={enUS}>
      <MyApp />
    </ConfigProvider>
  );
}
```

## 动态切换语言

```tsx
import { useState } from 'react';
import { ConfigProvider, Select } from '@arco-design/web-react';
import zhCN from '@arco-design/web-react/es/locale/zh-CN';
import enUS from '@arco-design/web-react/es/locale/en-US';
import jaJP from '@arco-design/web-react/es/locale/ja-JP';

const locales = { 'zh-CN': zhCN, 'en-US': enUS, 'ja-JP': jaJP };

function App() {
  const [locale, setLocale] = useState('zh-CN');

  return (
    <ConfigProvider locale={locales[locale]}>
      <Select value={locale} onChange={setLocale} style={{ width: 200 }}>
        <Select.Option value="zh-CN">简体中文</Select.Option>
        <Select.Option value="en-US">English</Select.Option>
        <Select.Option value="ja-JP">日本語</Select.Option>
      </Select>
      <MyApp />
    </ConfigProvider>
  );
}
```

## Locale 数据结构

每个 locale 包含以下组件的文案：

```ts
interface Locale {
  locale: string;           // 语言标识 e.g. 'en-US'
  dayjsLocale?: string;     // dayjs 对应语言包名

  Calendar: { ... };        // 日历：月份名、星期名
  DatePicker: { ... };      // 日期选择器：占位符、今天、确认等
  Drawer: { okText, cancelText };
  Empty: { noData };
  Modal: { okText, cancelText };
  Pagination: { ... };      // 分页：前一页、后一页、每页条数等
  Popconfirm: { okText, cancelText };
  Table: { ... };           // 表格：筛选、排序、空数据等
  TimePicker: { ... };
  Upload: { ... };          // 上传：开始、删除、预览等
  Progress: { ... };
  Typography: { ... };      // 排版：复制、已复制、展开、折叠
  Transfer: { ... };        // 穿梭框：全选、搜索等
  ImagePreview: { ... };
  Form: { ... };            // 表单：校验消息模板
  ColorPicker: { ... };
}
```

## 自定义语言包

可以基于已有语言包扩展或创建新的：

```tsx
import enUS from '@arco-design/web-react/es/locale/en-US';

const customLocale = {
  ...enUS,
  Table: {
    ...enUS.Table,
    noData: 'Nothing here yet',
  },
  Empty: {
    noData: 'No results found',
  },
};

<ConfigProvider locale={customLocale}>
  <App />
</ConfigProvider>
```

## 与 dayjs 语言同步

每个 locale 文件会自动导入对应的 dayjs 语言包：

```ts
// 例如 ja-JP.tsx 内部
import 'dayjs/locale/ja';
```

DatePicker、TimePicker、Calendar 等日期相关组件会自动使用对应语言的日期格式。

## 最佳实践

1. **在应用入口处设置一次 locale**，不要在组件内部重复设置
2. **配合 RTL 使用阿拉伯语** 时设置 `rtl={true}`
3. **动态加载语言包** 避免打包体积过大——使用 `import()` 动态导入
4. **自定义文案优先覆盖** 而非创建全新语言包，减少维护成本
5. **dayjs locale 会自动注册**，无需手动 `dayjs.locale()`

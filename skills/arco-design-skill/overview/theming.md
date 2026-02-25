---
name: arco-theming
description: Arco Design 主题定制指南。当需要自定义主题色、CSS 变量覆盖、Less 变量修改或实现暗色模式切换时使用。
user-invocable: false
---

# 主题定制

Arco Design 支持通过 Less 变量进行主题定制。

## Less 变量配置

如果使用 Less，可以在构建工具中覆盖变量：

```less
// custom-theme.less
@arcoblue-6: #165DFF;  // 主色
@green-6: #00B42A;     // 成功色
@gold-6: #FF7D00;      // 警告色
@red-6: #F53F3F;       // 危险色

@border-radius-small: 2px;
@border-radius-medium: 4px;

@font-size-body-1: 14px;
```

### Webpack 配置

```js
// webpack.config.js
module.exports = {
  module: {
    rules: [{
      test: /\.less$/,
      use: [{
        loader: 'less-loader',
        options: {
          lessOptions: {
            modifyVars: {
              'arcoblue-6': '#165DFF',
            },
            javascriptEnabled: true,
          },
        },
      }],
    }],
  },
};
```

## 暗色模式

### 方式一：引入暗色 CSS

```tsx
// 替换默认 CSS
import '@arco-design/web-react/dist/css/arco.dark.css';
```

### 方式二：通过 body 属性切换

```tsx
// 动态切换
document.body.setAttribute('arco-theme', 'dark');

// 切回亮色
document.body.removeAttribute('arco-theme');
```

### 响应系统暗色模式

```tsx
import { useEffect, useState } from 'react';

function useTheme() {
  const [dark, setDark] = useState(false);

  useEffect(() => {
    const media = window.matchMedia('(prefers-color-scheme: dark)');
    setDark(media.matches);
    const handler = (e) => setDark(e.matches);
    media.addEventListener('change', handler);
    return () => media.removeEventListener('change', handler);
  }, []);

  useEffect(() => {
    if (dark) {
      document.body.setAttribute('arco-theme', 'dark');
    } else {
      document.body.removeAttribute('arco-theme');
    }
  }, [dark]);

  return { dark, setDark };
}
```

## CSS 前缀定制

当页面中存在多套 Arco Design 或与其他库冲突时，可自定义前缀：

```tsx
<ConfigProvider prefixCls="my-app">
  <Button>自定义前缀</Button>
</ConfigProvider>
```

生成的类名将从 `arco-btn` 变为 `my-app-btn`。

同时需要配合 Less 变量：

```less
@prefix: my-app;
```

## 最佳实践

2. **暗色模式使用 `arco-theme` 属性方案**，方便动态切换
3. **只覆盖需要修改的变量**，其余继承默认值
5. **自定义 prefixCls 时注意一致性**，Less 变量和 ConfigProvider 要同步设置

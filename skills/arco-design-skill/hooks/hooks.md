---
name: arco-hooks
description: Arco Design 公共 Hooks 与内部 Hooks 参考。当需要使用 useResponsive、useFocusEffect 等 Hooks 或了解组件内部 Hook 实现时使用。
user-invocable: false
---

# Hooks 参考

## 公开 Hooks

从 `@arco-design/web-react/hooks` 导入，可用于构建自定义组件。

### useVerificationCode

无头验证码输入 Hook，管理多个单字符输入框的值、焦点、粘贴和键盘导航。

```ts
import { useVerificationCode } from '@arco-design/web-react/hooks';
```

**参数 (Options)**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `length` | `number` | `6` | 验证码位数 |
| `defaultValue` | `string` | — | 非受控初始值 |
| `value` | `string` | — | 受控值 |
| `onChange` | `(value: string) => void` | — | 值变化回调 |
| `onFinish` | `(value: string) => void` | — | 所有位填满时回调 |
| `getInputRefList` | `() => HTMLInputElement[]` | — | 返回输入框 DOM 列表 |

**返回值**

| 属性 | 类型 | 说明 |
|------|------|------|
| `filledValue` | `string[]` | 每一位的值数组 |
| `value` | `string` | 当前拼接后的完整值 |
| `setValue` | `(value: string) => void` | 命令式设置值 |
| `getInputProps` | `(index: number) => InputProps` | 获取第 N 个输入框的 props |

**示例**

```tsx
import { useVerificationCode } from '@arco-design/web-react/hooks';

const CustomOTP = () => {
  const inputRefList = React.useRef<HTMLInputElement[]>([]);

  const { filledValue, getInputProps } = useVerificationCode({
    length: 6,
    getInputRefList: () => inputRefList.current || [],
    onFinish: (value) => {
      console.log('验证码:', value);
    },
  });

  return (
    <div style={{ display: 'flex', gap: 8 }}>
      {filledValue.map((v, index) => {
        const inputProps = { ...getInputProps(index) };
        return (
          <input
            key={index}
            ref={(node) => { inputRefList.current[index] = node; }}
            style={{ width: 40, height: 40, textAlign: 'center', fontSize: 18 }}
            {...inputProps}
            onChange={(e) => inputProps.onChange?.(e.target.value)}
          />
        );
      })}
    </div>
  );
};
```

---

### useWatermark

无头水印 Hook，通过 Canvas 渲染水印层，支持文字/图片、旋转、自定义字体，使用 MutationObserver 防止水印被篡改。

```ts
import { useWatermark } from '@arco-design/web-react/hooks';
```

**参数 (Options)**

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `zIndex` | `number` | `1` | 水印 z-index |
| `width` | `number \| string` | `100`(图片) | 单个水印宽度 |
| `height` | `number \| string` | — | 单个水印高度 |
| `rotate` | `number` | `-20` | 旋转角度 |
| `image` | `string` | — | 图片 URL（优先级高于 content） |
| `content` | `string \| string[]` | — | 文字内容（数组支持多行） |
| `fontStyle` | `object` | — | 字体样式 |
| `gap` | `[number, number]` | `[100, 100]` | 水印间距 |
| `offset` | `[number, number]` | — | 偏移量 |
| `getContainer` | `() => HTMLElement` | — | 容器元素 |

**返回值**

| 属性 | 类型 | 说明 |
|------|------|------|
| `destroy` | `() => void` | 移除水印并清理 observer |
| `setWatermark` | `(options) => void` | 应用或更新水印 |

**示例**

```tsx
import { useWatermark } from '@arco-design/web-react/hooks';

const CustomWatermark = ({ children, content }) => {
  const containerRef = React.useRef<HTMLDivElement>(null);
  const { setWatermark, destroy } = useWatermark({});

  React.useEffect(() => {
    if (containerRef.current) {
      setWatermark({
        content,
        fontStyle: { color: 'rgba(0, 0, 0, 0.1)', fontSize: 16 },
        getContainer: () => containerRef.current!,
      });
    }
    return () => destroy();
  }, [content]);

  return (
    <div ref={containerRef} style={{ position: 'relative' }}>
      {children}
    </div>
  );
};
```

---

## 架构说明

- **公开 Hooks** 独立于组件，可用于无头模式自定义 UI
- `@arco-design/web-react/hooks` 路径指向 `hooks/` 包的编译产物

---
name: arco-use-verification-code
description: "Arco Design useVerificationCode hook API. Use for building custom OTP / verification code input with multi-character input management, focus control, paste handling, and keyboard navigation."
user-invocable: false
---

# useVerificationCode

Headless hook for verification code / OTP input. Manages multiple single-character input values, focus, paste, and keyboard navigation.

```ts
import { useVerificationCode } from '@arco-design/web-react/hooks';
```

## Options

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `length` | `number` | `6` | Number of digits |
| `defaultValue` | `string` | — | Uncontrolled initial value |
| `value` | `string` | — | Controlled value |
| `onChange` | `(value: string) => void` | — | Called when value changes |
| `onFinish` | `(value: string) => void` | — | Called when all digits are filled |
| `getInputRefList` | `() => HTMLInputElement[]` | — | Returns the list of input DOM elements |

## Return Value

| Property | Type | Description |
|----------|------|-------------|
| `filledValue` | `string[]` | Array of each digit's value |
| `value` | `string` | Current concatenated full value |
| `setValue` | `(value: string) => void` | Imperatively set value |
| `getInputProps` | `(index: number) => InputProps` | Get props for the Nth input element |

## Example

```tsx
import { useVerificationCode } from '@arco-design/web-react/hooks';

const CustomOTP = () => {
  const inputRefList = React.useRef<HTMLInputElement[]>([]);

  const { filledValue, getInputProps } = useVerificationCode({
    length: 6,
    getInputRefList: () => inputRefList.current || [],
    onFinish: (value) => {
      console.log('Code:', value);
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

## Best Practices

1. **Prefer the `VerificationCode` component** for standard use — use this hook only when you need a fully custom UI
2. **Always provide `getInputRefList`** — the hook needs DOM refs for focus management
3. **Use `onFinish` for auto-submit** — trigger verification API call when all digits are filled

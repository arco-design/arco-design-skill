---
name: arco-use-watermark
description: "Arco Design useWatermark hook API. Use for rendering dynamic canvas-based watermarks with text/image support, rotation, custom fonts, and MutationObserver tamper protection."
user-invocable: false
---

# useWatermark

Headless watermark hook. Renders a watermark layer via Canvas, supports text/image, rotation, custom fonts. Uses MutationObserver to prevent watermark tampering.

```ts
import { useWatermark } from '@arco-design/web-react/hooks';
```

## Options

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `zIndex` | `number` | `1` | Watermark z-index |
| `width` | `number \| string` | `100` (image) | Single watermark width |
| `height` | `number \| string` | — | Single watermark height |
| `rotate` | `number` | `-20` | Rotation angle in degrees |
| `image` | `string` | — | Image URL (takes priority over content) |
| `content` | `string \| string[]` | — | Text content (array for multiple lines) |
| `fontStyle` | `object` | — | Font style: `{ color, fontSize, fontFamily, fontWeight }` |
| `gap` | `[number, number]` | `[100, 100]` | Spacing between watermarks `[horizontal, vertical]` |
| `offset` | `[number, number]` | — | Offset from origin |
| `getContainer` | `() => HTMLElement` | — | Container element to attach watermark to |

## Return Value

| Property | Type | Description |
|----------|------|-------------|
| `destroy` | `() => void` | Remove watermark and clean up MutationObserver |
| `setWatermark` | `(options) => void` | Apply or update watermark with new options |

## Example

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

## Best Practices

1. **Prefer the `Watermark` component** for standard use — use this hook only when you need programmatic watermark control
2. **Always call `destroy()` in cleanup** — prevents memory leaks from MutationObserver
3. **Use `setWatermark` to update dynamically** — e.g., change watermark text when user info changes
4. **Container must have `position: relative`** — watermark is absolutely positioned inside it

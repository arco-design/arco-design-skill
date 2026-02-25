---
name: arco-image
description: Arco Image 图片组件用法与 API。当需要图片展示、预览、懒加载或图片组预览时使用。
user-invocable: false
---

# Image 图片

```tsx
import { Image } from '@arco-design/web-react';

<Image src="/photo.jpg" width={200} alt="photo" />

// 图片组（支持预览切换）
<Image.PreviewGroup>
  <Image src="/1.jpg" width={200} />
  <Image src="/2.jpg" width={200} />
  <Image src="/3.jpg" width={200} />
</Image.PreviewGroup>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `src` | `string` | 图片地址 |
| `width` / `height` | `number \| string` | 尺寸 |
| `title` / `description` | `string` | 标题/描述 |
| `preview` | `boolean` | 可预览（默认 true） |
| `previewProps` | `ImagePreviewProps` | 预览配置 |
| `error` | `ReactNode` | 加载失败内容 |
| `loader` | `boolean \| ReactNode` | 加载中 |
| `lazyload` | `boolean \| IntersectionObserverInit` | 懒加载 |
| `footerPosition` | `'inner' \| 'outer'` | 底部信息位置 |
| `actions` | `ReactNode[]` | 预览操作 |

## 常用模式

```tsx
// 图片预览
<Image width={200} src="/photo.jpg" alt="图片" />

// 图片组预览
<Image.PreviewGroup>
  <Image src="/1.jpg" width={100} />
  <Image src="/2.jpg" width={100} />
  <Image src="/3.jpg" width={100} />
</Image.PreviewGroup>

// 懒加载
<Image lazyload src="/large-image.jpg" />

// 加载失败占位
<Image
  src="/broken.jpg"
  width={200}
  height={200}
  error={<div style={{ background: '#f5f5f5', display: 'flex', alignItems: 'center', justifyContent: 'center', height: '100%' }}>加载失败</div>}
/>

// 额外操作
<Image
  src="/photo.jpg"
  width={300}
  actions={[
    <button key="download" onClick={() => download(src)}>下载</button>,
  ]}
/>
```

## 最佳实践

1. **始终设置 alt** —— 图片可访问性必备
2. **大量图片使用 lazyload** —— 减少首屏加载时间
3. **PreviewGroup 用于图片列表** —— 自动支持左右切换预览
4. **设置 width/height 防止布局抖动** —— 图片加载前就确定占位大小

---
name: arco-image
description: "Arco Design Image component API. Use for image display, preview, lazy loading, Image.PreviewGroup for galleries, and error fallback."
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

### ImageProps

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

### Image.Preview

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `src` | `string` | — | 预览图地址 |
| `visible` | `boolean` | — | 受控显示 |
| `defaultVisible` | `boolean` | — | 默认显示 |
| `onVisibleChange` | `(visible, prev) => void` | — | 显隐回调 |
| `imgAttributes` | `Omit<ImgHTMLAttributes, 'src'>` | — | 透传到 `<img>` 的属性（2.39.0） |
| `actions` | `ImagePreviewActionProps[]` | — | 操作栏 |
| `actionsLayout` | `string[]` | `['fullScreen','rotateRight','rotateLeft','zoomIn','zoomOut','originalSize','extra']` | 操作栏布局 |
| `scales` | `number[]` | `[25,33,50,67,75,80,90,100,110,125,150,175,200,250,300,400,500]` | 可用缩放百分比（不含 100 时会自动加入；2.30.0） |
| `breakPoint` | `number` | `316` | 切换 simple 工具栏的阈值宽度 |
| `closable` | `boolean` | `true` | 显示关闭按钮（2.16.0） |
| `maskClosable` | `boolean` | `true` | 点击遮罩关闭 |
| `escToExit` | `boolean` | `true` | 按 ESC 关闭（2.24.0） |
| `getPopupContainer` | `() => HTMLElement` | `() => document.body` | 弹出层挂载节点（2.16.0） |
| `extra` | `ReactNode` | — | 预览区域额外节点（2.53.0） |

### Image.PreviewGroup

| 属性 | 类型 | 说明 |
|------|------|------|
| `srcList` | `string[]` | 图片列表 |
| `current` | `number` | 当前索引 |
| `defaultCurrent` | `number` | 默认索引 |
| `onChange` | `(index) => void` | 切换回调 |
| `visible` | `boolean` | 受控显示 |
| `onVisibleChange` | `(visible) => void` | 显隐回调 |
| `infinite` | `boolean` | 无限循环切换 |

> `Image.PreviewGroup` 继承除 `src` 之外的所有 `Image.Preview` 属性（`imgAttributes`、`actions`、`actionsLayout`、`scales`、`maskClosable`、`escToExit`、`closable`、`extra` 等都可在 PreviewGroup 上传入）。

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

// 预览时添加额外内容 (2.53.0)
<Image
  src="/photo.jpg"
  width={200}
  previewProps={{
    extra: <div style={{ position: 'absolute', bottom: 20, color: '#fff' }}>图片说明</div>,
  }}
/>

// 加载失败占位
<Image
  src="/broken.jpg"
  width={200}
  height={200}
  error={<div style={{ background: '#f5f5f5', display: 'flex', alignItems: 'center', justifyContent: 'center', height: '100%' }}>加载失败</div>}
/>
```

## 最佳实践

1. **始终设置 alt** —— 图片可访问性必备
2. **大量图片使用 lazyload** —— 减少首屏加载时间
3. **PreviewGroup 用于图片列表** —— 自动支持左右切换预览
4. **设置 width/height 防止布局抖动** —— 图片加载前就确定占位大小

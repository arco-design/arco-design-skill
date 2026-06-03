---
name: arco-upload
description: "Arco Design Upload component API. Use for file upload, drag-and-drop upload, image upload with preview, custom upload logic, and upload list management."
user-invocable: false
---

# Upload 上传

```tsx
import { Upload } from '@arco-design/web-react';

// 基本上传
<Upload action="/api/upload" />

// 拖拽上传
<Upload drag action="/api/upload" tip="支持拖拽上传" />

// 图片上传
<Upload
  listType="picture-card"
  action="/api/upload"
  limit={3}
/>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `action` | `string` | 上传地址 |
| `fileList` / `defaultFileList` | `UploadItem[]` | 受控 / 默认文件列表 |
| `accept` | `string \| { type: string; strict?: boolean }` | 接受文件类型。传对象时 `strict` 默认 true，严格匹配后缀名；设为 false 则与浏览器原生行为一致 (2.53.0) |
| `multiple` | `boolean` | 多选 |
| `limit` | `number \| { maxCount: number; hideOnExceedLimit?: boolean }` | 最大文件数，对象类型自 2.28.0 支持 |
| `listType` | `'text' \| 'picture-list' \| 'picture-card'` | 列表样式 |
| `autoUpload` | `boolean` | 自动上传，默认 true |
| `drag` | `boolean` | 拖拽上传 |
| `directory` | `boolean` | 文件夹上传 (2.11.0) |
| `headers` | `object` | 请求头 |
| `data` | `object \| (file) => object` | 附加数据 |
| `name` | `string \| (file) => string` | 文件参数名 |
| `withCredentials` | `boolean` | 携带 cookie |
| `customRequest` | `(options) => UploadRequestReturn` | 自定义上传 |
| `beforeUpload` | `(file, fileList) => boolean \| Promise` | 上传前校验 |
| `onChange` | `(fileList, file) => void` | 文件变化 |
| `onPreview` | `(file) => void` | 预览回调 |
| `onRemove` | `(file, fileList) => void \| boolean \| Promise` | 删除回调，返回 false 或 reject 阻止删除 |
| `onProgress` | `(file, e?) => void` | 上传进度回调 |
| `onReupload` | `(file) => void` | 重新上传回调 |
| `onExceedLimit` | `(files, fileList) => void` | 超出数量限制回调 |
| `onDrop` | `(e: DragEvent) => void` | 拖拽上传回调 (2.37.0) |
| `onDragOver` | `(e: DragEvent) => void` | 拖入回调 (2.41.0) |
| `onDragLeave` | `(e: DragEvent) => void` | 拖出回调 (2.41.0) |
| `imagePreview` | `boolean` | 内置图片预览，仅 listType='picture-card' 生效 (2.41.0) |
| `showUploadList` | `boolean \| CustomIconType` | 是否展示文件列表，可传对象自定义图标 |
| `renderUploadItem` | `(originNode, file, fileList) => ReactNode` | 自定义列表项 |
| `renderUploadList` | `(fileList, uploadListProps) => ReactNode` | 自定义文件列表 |
| `progressProps` | `Partial<ProgressProps>` | 进度条属性 |
| `tip` | `string \| ReactNode` | 提示文字 |
| `disabled` | `boolean` | 禁用 |

### UploadItem

| 属性 | 类型 | 说明 |
|------|------|------|
| `uid` | `string` | 唯一标识 |
| `status` | `'init' \| 'uploading' \| 'done' \| 'error'` | 上传状态 |
| `originFile` | `File` | 文件对象 |
| `percent` | `number` | 上传进度 |
| `response` | `object` | 上传响应 |
| `url` | `string` | 文件 URL |
| `name` | `string` | 文件名 |

### UploadInstance (Ref)

| 方法 | 说明 |
|------|------|
| `submit(file?)` | 手动上传，不传参默认上传所有 init 状态文件 |
| `abort(file)` | 中止上传 |
| `reupload(file)` | 重新上传 |

## 常用模式

```tsx
// 上传前校验
<Upload
  action="/api/upload"
  beforeUpload={(file) => {
    if (file.size > 5 * 1024 * 1024) {
      Message.error('文件不能超过 5MB');
      return false;
    }
    return true;
  }}
/>

// accept 严格模式 (2.53.0)
<Upload
  action="/api/upload"
  accept={{ type: '.jpg,.png,.gif', strict: true }}
/>
// accept 原生模式
<Upload
  action="/api/upload"
  accept={{ type: 'image/*', strict: false }}
/>

// 自定义请求
<Upload
  customRequest={(option) => {
    const { onProgress, onError, onSuccess, file } = option;
    const formData = new FormData();
    formData.append('file', file);
    axios.post('/api/upload', formData, {
      onUploadProgress: (e) => onProgress(parseInt(String((e.loaded / e.total) * 100))),
    }).then((res) => onSuccess(res)).catch(onError);
    return { abort: () => {} };
  }}
/>

// 在 Form 中使用
<Form.Item field="files" triggerPropName="fileList">
  <Upload action="/api/upload" />
</Form.Item>
```

## 最佳实践

1. **使用 `accept` 限制文件类型**，减少用户误传
2. **`beforeUpload` 校验文件大小**，避免大文件阻塞
3. **Form 中使用 `triggerPropName="fileList"`**
4. **自定义上传用 `customRequest`**，返回 `{ abort }` 支持取消
5. **`onRemove` 返回 false/reject** 可拦截删除操作

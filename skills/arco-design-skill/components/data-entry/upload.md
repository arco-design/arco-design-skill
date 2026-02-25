---
name: arco-upload
description: Arco Upload 上传组件用法与 API。当需要文件上传、拖拽上传、图片上传或自定义上传逻辑时使用。
user-invocable: false
---

# Upload 上传

```tsx
import { Upload } from '@arco-design/web-react';

// 基本上传
<Upload action="/api/upload" />

// 拖拽上传
<Upload.Dragger action="/api/upload" tip="支持拖拽上传" />

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
| `accept` | `string` | 接受文件类型 |
| `multiple` | `boolean` | 多选 |
| `limit` | `number` | 最大文件数 |
| `listType` | `'text' \| 'picture-list' \| 'picture-card'` | 列表样式 |
| `autoUpload` | `boolean` | 自动上传 |
| `drag` | `boolean` | 拖拽上传 |
| `headers` | `object` | 请求头 |
| `data` | `object \| (file) => object` | 附加数据 |
| `withCredentials` | `boolean` | 携带 cookie |
| `customRequest` | `(options) => UploadRequestReturn` | 自定义上传 |
| `beforeUpload` | `(file, fileList) => boolean \| Promise` | 上传前校验 |
| `onChange` | `(fileList, file) => void` | 文件变化 |
| `onPreview` | `(file) => void` | 预览回调 |
| `onRemove` | `(file, fileList) => void` | 删除回调 |

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

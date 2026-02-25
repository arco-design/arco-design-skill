---
name: arco-comment
description: Arco Comment 评论组件用法与 API。当需要展示评论内容、嵌套回复或评论列表时使用。
user-invocable: false
---

# Comment 评论

```tsx
import { Comment, Avatar } from '@arco-design/web-react';

<Comment
  author="张三"
  avatar={<Avatar>张</Avatar>}
  content="这是一条评论"
  datetime="2 小时前"
  actions={[<span key="reply">回复</span>, <span key="like">点赞</span>]}
/>

// 嵌套评论
<Comment author="张三" avatar={<Avatar>张</Avatar>} content="第一层评论">
  <Comment author="李四" avatar={<Avatar>李</Avatar>} content="回复评论" />
</Comment>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `author` | `ReactNode` | 作者名 |
| `avatar` | `ReactNode` | 头像 |
| `content` | `ReactNode` | 评论内容 |
| `datetime` | `ReactNode` | 时间 |
| `actions` | `ReactNode[]` | 操作列表 |
| `align` | `{ datetime, actions }` | 对齐方式 |

## 常用模式

```tsx
// 嵌套评论
<Comment
  author="张三"
  avatar={<Avatar>张</Avatar>}
  content="这是一条评论"
  datetime="2024-01-01"
  actions={[<span key="reply" onClick={handleReply}>回复</span>]}
>
  <Comment
    author="李四"
    avatar={<Avatar>李</Avatar>}
    content="这是一条回复"
    datetime="2024-01-02"
  />
</Comment>

// 带点赞操作
<Comment
  actions={[
    <span key="like" onClick={toggleLike}>
      {liked ? <IconHeartFill /> : <IconHeart />} {likeCount}
    </span>,
    <span key="reply">回复</span>,
  ]}
  author="用户名"
  content="评论内容"
/>
```

## 最佳实践

1. **嵌套层级不宜过深** —— 一般不超过 3 层，超出可用「查看更多回复」
2. **actions 放交互操作** —— 点赞、回复、举报等
3. **配合 List 展示评论列表** —— `<List dataSource={comments} renderItem={item => <Comment ... />} />`

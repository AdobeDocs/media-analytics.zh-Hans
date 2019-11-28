---
title: 在播放器中设置 HTTP 请求类型
description: null
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 设置 HTTP 请求类型 {#setting-the-http-request-type}

所有媒体收集 API 请求的请求正文必须采用 JSON 格式，因此您应该在播放器中设置内容请求类型。例如，在 JavaScript 中，您将设置 `Content-Type` 请求标头，如下所示：

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```


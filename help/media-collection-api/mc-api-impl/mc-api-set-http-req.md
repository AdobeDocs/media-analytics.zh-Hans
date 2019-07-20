---
seo-title: 在播放器中设置 HTTP 请求类型
title: 在播放器中设置 HTTP 请求类型
uuid: b8fa7233-e654-4acf-a9 d7-14158ced13 e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Setting the HTTP request type {#setting-the-http-request-type}

所有媒体收集 API 请求的请求正文必须采用 JSON 格式，因此您应该在播放器中设置内容请求类型。例如，在 JavaScript 中，您将设置 `Content-Type` 请求标头，如下所示：

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```


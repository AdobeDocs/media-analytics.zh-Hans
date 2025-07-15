---
title: 在播放器中设置 HTTP 请求类型
description: 所有媒体收集API请求的请求正文必须采用JSON格式。 了解如何在播放器中设置内容请求类型。
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 81%

---

# 设置 HTTP 请求类型 {#setting-the-http-request-type}

所有媒体收集 API 请求的请求正文必须采用 JSON 格式，因此您应该在播放器中设置内容请求类型。例如，在 JavaScript 中，您将设置 `Content-Type` 请求标头，如下所示：

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

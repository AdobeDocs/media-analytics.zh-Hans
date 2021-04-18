---
title: 实施事件请求
description: 实施事件请求
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 100%

---

# 实施事件请求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

在使用以下操作获得会话 ID 后，使用[事件请求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)进行所有后续跟踪调用：[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)获取会话 ID 后。在请求的 JSON 正文中指定播放头位置和时间戳、事件类型以及要包括的任何可选参数。

[事件请求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)的 JSON 请求正文具有与会话请求相同的结构，但请查看 [JSON 验证架构](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)以了解参数要求和类型。

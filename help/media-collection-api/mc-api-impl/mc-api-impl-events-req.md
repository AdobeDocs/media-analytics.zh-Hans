---
seo-title: 实施事件请求
title: 实施事件请求
uuid: 3bfa313c-ff74-4e2 e-bbde-6f4 a6221 d85 b
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 实施事件请求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](../../media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) 在请求的JSON正文中指定播放头位置和时间戳、事件类型以及要包括的任何可选参数。

[Events请求的JSON请求主体](../../media-collection-api/mc-api-ref/mc-api-events-req.md) 与Sessions请求的结构相同，但检查 [JSON验证架构](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) 是否为参数要求和类型。

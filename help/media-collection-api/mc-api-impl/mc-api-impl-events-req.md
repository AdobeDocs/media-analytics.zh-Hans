---
seo-title: 实施事件请求
title: 实施事件请求
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 实施事件请求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) 在请求的JSON主体中指定播放头位置和时间戳、事件类型以及要包括的任何可选参数。

The JSON request body for the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the Sessions request, however check the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for parameter requirements and types.

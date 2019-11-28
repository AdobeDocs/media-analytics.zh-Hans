---
title: 实施事件请求
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 实施事件请求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

在以下操作后，使用[事件请求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)进行所有后续跟踪调用：使用[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)获取会话 ID 后。在请求的 JSON 正文中指定播放头位置和时间戳、事件类型以及要包括的任何可选参数。

[事件请求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)的 JSON 请求正文具有与会话请求相同的结构，但请查看 [JSON 验证架构](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)以了解参数要求和类型。

---
title: 实施事件请求
description: 了解在获得会话 ID 后，如何使用事件请求端点进行所有后续跟踪调用
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '99'
ht-degree: 100%

---

# 实施事件请求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

在使用以下操作获得会话 ID 后，使用[事件请求](../mc-api-ref/mc-api-events-req.md)进行所有后续跟踪调用：[会话请求](../mc-api-ref/mc-api-sessions-req.md)获取会话 ID 后。在请求的 JSON 正文中指定播放头位置和时间戳、事件类型以及要包括的任何可选参数。

[事件请求](../mc-api-ref/mc-api-events-req.md)的 JSON 请求正文具有与会话请求相同的结构，但请查看 [JSON 验证架构](../mc-api-ref/mc-api-json-validation.md)以了解参数要求和类型。

---
title: 实施事件请求
description: 了解在获得会话 ID 后，如何使用事件请求端点进行所有后续跟踪调用
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/xJntEcDm5sCGoCeuCjl9x51EOaYcOO2FzFAtK8mbt38
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 99
ht-degree: 56%

---

# 实施事件请求{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

在使用[会话请求](../mc-api-ref/mc-api-sessions-req.md)获取会话ID后，请将[事件请求](../mc-api-ref/mc-api-events-req.md)用于所有后续跟踪调用。 在请求的JSON正文中指定播放头位置和时间戳、事件类型以及要包括的任何可选参数。

[事件请求](../mc-api-ref/mc-api-events-req.md)的 JSON 请求正文具有与会话请求相同的结构，但请查看 [JSON 验证架构](../mc-api-ref/mc-api-json-validation.md)以了解参数要求和类型。

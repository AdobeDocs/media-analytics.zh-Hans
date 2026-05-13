---
title: 流媒体服务JSON验证架构
description: 什么是流媒体 JSON 验证架构以及如何使用它们为每种类型的事件确定正确的请求正文参数。
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ZWKv1LJKc8qLkZYpcNdDFEs8Er70toRCoufarMcgVKQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 84
ht-degree: 71%

---

# JSON 验证架构{#json-validation-schemas}

流媒体收集后端使用JSON验证架构验证每个事件类型的请求参数。 您可以使用这些架构作为当前在 MA API 中使用的参数类型的权威。

`GET https://{uri}/api/v1/schemas/{event-type}`

有关使用 JSON 验证架构的更多信息，请参阅[验证事件请求](../mc-api-impl/mc-api-validate-reqs.md)。

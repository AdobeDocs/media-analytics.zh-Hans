---
title: 流媒体分析JSON验证架构
description: 什么是Staming Media JSON验证架构，如何使用它们为每个事件类型确定正确的请求正文参数。
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 64%

---

# JSON 验证架构{#json-validation-schemas}

Media Analytics 后端使用 JSON 验证架构来验证每个事件类型的请求参数。您可以使用这些架构作为当前在 MA API 中使用的参数类型的权威。

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

有关使用 JSON 验证架构的更多信息，请参阅[验证事件请求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)。

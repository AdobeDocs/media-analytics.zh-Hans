---
title: JSON 验证架构
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 72fd9b359d778c912ae6439aa0438ed467ebeef1
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 100%

---


# JSON 验证架构{#json-validation-schemas}

Media Analytics 后端使用 JSON 验证架构来验证每个事件类型的请求参数。您可以使用这些架构作为当前在 MA API 中使用的参数类型的权威。

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

有关使用 JSON 验证架构的更多信息，请参阅[验证事件请求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)。

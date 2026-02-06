---
title: 流媒体服务JSON验证架构
description: 什么是流媒体 JSON 验证架构以及如何使用它们为每种类型的事件确定正确的请求正文参数。
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 72%

---

# JSON 验证架构{#json-validation-schemas}

流媒体收集后端使用JSON验证架构验证每个事件类型的请求参数。 您可以使用这些架构作为当前在 MA API 中使用的参数类型的权威。

`GET https://{uri}/api/v1/schemas/{event-type}`

有关使用 JSON 验证架构的更多信息，请参阅[验证事件请求](../mc-api-impl/mc-api-validate-reqs.md)。

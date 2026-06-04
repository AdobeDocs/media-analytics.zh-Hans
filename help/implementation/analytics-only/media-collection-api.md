---
title: 设置适用于流媒体的媒体收集API
description: 使用媒体收集API通过RESTful HTTP调用将流媒体数据直接发送到Adobe Analytics。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# 设置适用于流媒体的媒体收集API

媒体收集API使用RESTful HTTP调用将流媒体数据直接发送到Adobe Analytics。 由于是完全可自定义的，因此它支持SDK未涵盖的自定义跟踪和设备。 当SDK不适合您的平台时，使用此选项。

* **先决条件**：完成[仅限Analytics的实施概述](overview.md)。

## 实施API

打开一个带有`sessionStart`请求的会话，然后将后续事件发送到它返回的会话。 有关完整的请求/响应格式、参数、验证架构和实施指南，请参阅[媒体收集API引用](../media-collection-api/mc-api-overview.md)。

## 跟踪媒体事件

查看每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**媒体收集API**&#x200B;选项卡，了解确切负载。

## 下一步

实施完成后，您可以[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [媒体收集API引用](../media-collection-api/mc-api-overview.md)
>* [事件概述](/help/implementation/events/overview.md)
>* [变量概述](/help/implementation/variables/overview.md)

---
title: 了解流媒体的先决条件
description: 开始使用 Adobe Analytics 流媒体。了解实施适用于流媒体的 Adobe Analytics 所需的工具。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 50%

---

# 前提条件{#prerequisites}

要实施适用于流媒体的Adobe Analytics，请完成以下任务：

1. **确认流媒体定价模型**<br>
当前的定价模型基于视频流。 如有必要，请联系您的销售代表或客户经理以签署新的销售订单，因为流媒体分析与Adobe Analytics分开销售。

1. **确认您正在实施Adobe Analytics**<br>
Adobe Analytics的流媒体还需要Adobe Analytics基本实施。 请参阅 [实施Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans) 以了解更多信息。

1. **获取媒体跟踪服务器URL**<br>
有关媒体跟踪服务器URL，请咨询Adobe Analytics代表。 这是 
`collection-api-server` 适用于Roku的Mobile SDK、JavaScript SDK和非收集API跟踪服务器的URL。 API实施的域名为： `[your_namespace].hb-api.omtrdc.net`.

1. **下载当前Media SDK或实施所需的扩展**<br>
根据实施路径， [下载当前SDK](download-sdks.md) 适用于web、移动或顶部平台。 必须实施所需的扩展才能启用适用于流媒体的Adobe Analytics。 有关所需扩展的信息，请参阅 [Adobe扩展](download-sdks.md#media-extension). （需要阐明是下载Media SDK还是获取扩展）

1. **启用Adobe Analytics报表**<br>
要启用Analytics中的报表并查看您正在收集的内容和广告数据，您必须在Analytics中启用报表。 请参阅 [媒体报表启用。](/help/reporting/media-reports-enable.md).

1. **启用Experience Cloud**<br>


## 实施 Adobe Experience Platform Identity Service. {#implement-id}

的 **Identity Service** 为Experience Cloud核心服务、解决方案和客户属性以及人员核心服务中的受众启用了通用识别框架。 Identity Service 通过向网站访客分配一个唯一的永久性 ID 来工作。当您的组织实施 ID 服务时，此 ID 允许您在不同的 Experience Cloud 解决方案中识别同一站点访客及其数据。

![ID服务图](assets/mc_id_service_graphic.png)

ID 服务还可以替换解决方案特定的不同 ID（例如，Analytics AID）。通过[客户 ID 和身份验证状态](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hans)功能，ID 服务允许您将自己的客户 ID 传递到 Experience Cloud。但是，请记住，ID 服务仅适用于您已订阅的解决方案。如果您未注册访问其他产品，则 ID 服务不提供访问权限。

ID服务是许多Experience Cloud功能、增强功能和服务的必备组件。 当前，ID 服务支持 [Analytics](https://www.adobe.com/cn/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/cn/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/cn/marketing-cloud/testing-targeting.html)。

如果您还没有实施 ID 服务，现在是时候开始考虑迁移策略了。有关 ID 服务的重要性和角色的更多信息，请参阅[为什么您应考虑使用 Identity Service](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

有关 Experience Cloud ID 的其他信息，请参阅 [Experience Cloud ID 概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)和 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)。

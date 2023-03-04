---
title: 了解流媒体的先决条件
description: 开始使用 Adobe Analytics 流媒体。了解实施 Adobe Analytics for Streaming Media 所需的工具。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 0c1382c9c4f1488fba81575097d154301a9b8e70
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 94%

---

# 先决条件{#prerequisites}

要实施 Adobe Analytics for Streaming Media，请完成以下任务：

1. **确认您的流媒体定价模型**<br>
当前的定价模型基于视频流。如有必要，请联系您的销售代表或Adobe客户团队以签署新的销售订单，因为Streaming Media Analytics与Adobe Analytics是分开销售。

1. **确认您正在实施 Adobe Analytics**<br>
Streaming Media for Adobe Analytics 还需要 Adobe Analytics 基本实施。有关更多信息，请参阅[实施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans)。

1. **获取媒体跟踪服务器 URL**<br>
请向您的 Adobe Analytics 代表询问媒体跟踪服务器 URL。这是 
`collection-api-server`移动 SDK 的 URL、JavaScript SDK 和 Roku 的非收藏集 API 跟踪服务器。API 实施的域名是：`[your_namespace].hb-api.omtrdc.net`。

1. **下载当前的 Media SDK 或实施所需的扩展**<br>
根据实施路径的不同，为 Web、移动或过顶平台[下载当前 SDK](download-sdks.md)。必须实施所需的扩展才能启用适用于流媒体的 Adobe Analytics 扩展路径。

1. **启用 Adobe Analytics 报告**<br>
要在 Analytics 中启用报告，并查看所收集的内容和广告数据，您必须在 Analytics 中启用报告。请参阅[媒体报告启用](/help/reporting/media-reports-enable.md)。

1. **启用 Experience Cloud**<br>


## 实施 Adobe Experience Platform Identity Service. {#implement-id}

通过 **Identity Service**，可实现 Experience Cloud 核心服务、解决方案和客户属性以及人员核心服务中的受众通用的识别框架。Identity Service 通过向网站访客分配一个唯一的永久性 ID 来工作。当您的组织实施 ID 服务时，此 ID 允许您在不同的 Experience Cloud 解决方案中识别同一站点访客及其数据。

![ID 服务图形](assets/mc_id_service_graphic.png)

ID 服务还可以替换解决方案特定的不同 ID（例如，Analytics AID）。通过[客户 ID 和身份验证状态](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hans)功能，ID 服务允许您将自己的客户 ID 传递到 Experience Cloud。但是，请记住，ID 服务仅适用于您已订阅的解决方案。如果您未注册访问其他产品，则 ID 服务不提供访问权限。

ID 服务是许多 Experience Cloud 功能、增强和服务中必不可少的组件。当前，ID 服务支持 [Analytics](https://www.adobe.com/cn/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/cn/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/cn/marketing-cloud/testing-targeting.html)。

如果您还没有实施 ID 服务，现在是时候开始考虑迁移策略了。有关 ID 服务的重要性和角色的更多信息，请参阅[为什么您应考虑使用 Identity Service](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

有关 Experience Cloud ID 的其他信息，请参阅 [Experience Cloud ID 概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)和 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)。

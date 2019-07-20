---
seo-title: 先决条件
title: 先决条件
uuid: 4c0b37f3-8615-4cc0-b9 c9-eeb029067064
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# 先决条件{#prerequisites}

## Decisions {#decision}

在开始实施跟踪之前，您需要事先确定哪种实施最适用于您的具体情况：

* **Media Analytics -**&#x200B;使用最新的 Media SDK（标准、推荐实施）和/或媒体收集 API (RESTful)
* **里程碑 -**&#x200B;旧版 Adobe 跟踪实施
* **Data Insertion API -**&#x200B;在不使用 Media SDK 的情况下实施跟踪

## 任务 {#prereq-tasks}

*对于Media Analytics* 实施，在开始之前必须完成以下任务：

1. **启用 Experience Cloud。**

   您需要实施Adobe Experience Platform Identity Service。

   Identity Service为Experience Cloud核心服务、解决方案以及People核心服务中的客户属性和受众提供通用标识框架。它通过向网站访客分配一个唯一的永久性 ID 来工作。在您的组织实施 ID 服务后，您可以通过此 ID 在不同的 Experience Cloud 解决方案中识别同一网站访客及其数据。

   ![](assets/mc_id_service_graphic.png)

   ID 服务还可以取代不同的解决方案特定 ID（例如，Analytics AID）。利用[客户 ID 和身份验证状态](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html)功能，ID 服务允许您将自己的客户 ID 传递到 Experience Cloud。但是，请谨记，ID 服务仅可在您已经订阅的解决方案中使用。如果您没有注册以访问其他产品，ID 服务并不会提供该访问权限。

   今后，ID 服务将成为许多当前和将来推出的 Experience Cloud 功能、增强功能和服务中的必备组件。Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >要参加Adobe Experience Cloud Device Co-op，需要Experience Cloud ID服务。

   如果您还没有实施 ID 服务，现在是时候开始考虑迁移策略了。For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **启用 Adobe Analytics 报表。**

   To enable reports in Analytics and see the content and ad data you are collecting, see [Media reports enablement.](../media-reports/media-reports-enable.md)


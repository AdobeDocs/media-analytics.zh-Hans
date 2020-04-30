---
title: 先决条件
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# 先决条件{#prerequisites}

## 确定适当的实施 {#decision}

在开始实施跟踪之前，您需要事先确定哪种实施最适用于您的具体情况：

* **Media Analytics -**&#x200B;使用最新的 Media SDK（标准、推荐实施）和/或媒体收集 API (RESTful)
* **里程碑 -**&#x200B;旧版 Adobe 跟踪实施
* **Data Insertion API -**&#x200B;在不使用 Media SDK 的情况下实施跟踪

## 任务 {#prereq-tasks}

对于 *Media Analytics* 实施，以下是您在开始之前必须完成的任务：

1. **启用 Experience Cloud。**

   您需要实施 Adobe Experience Platform Identity Service。

   Identity Service 允许将通用识别框架用于 Experience Cloud 核心服务、解决方案和客户属性，以及人员核心服务中的受众。它通过向网站访客分配一个唯一的永久性 ID 来工作。在您的组织实施 ID 服务后，您可以通过此 ID 在不同的 Experience Cloud 解决方案中识别同一网站访客及其数据。

   ![](assets/mc_id_service_graphic.png)

   ID 服务还可以取代不同的解决方案特定 ID（例如，Analytics AID）。利用[客户 ID 和身份验证状态](https://docs.adobe.com/content/help/zh-Hans/id-service/using/reference/authenticated-state.html)功能，ID 服务允许您将自己的客户 ID 传递到 Experience Cloud。但是，请谨记，ID 服务仅可在您已经订阅的解决方案中使用。如果您没有注册以访问其他产品，ID 服务并不会提供该访问权限。

   今后，ID 服务将成为许多当前和将来推出的 Experience Cloud 功能、增强功能和服务中的必备组件。当前，ID 服务支持 [Analytics](https://www.adobe.com/cn/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/cn/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/cn/marketing-cloud/testing-targeting.html)。

   >[!IMPORTANT]
   >
   >要参与 Adobe Experience Cloud 设备协作，需要使用 Experience Cloud ID 服务。

   如果您还没有实施 ID 服务，现在是时候开始考虑迁移策略了。有关 ID 服务的重要性和角色的更多信息，请参阅[为什么您应考虑使用 Identity Service](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

   >[!IMPORTANT]
   >
   >如果特定于媒体的调用中缺少任何用户 ID 信息，则将应用默认的 Analytics [回退 ID 方法](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html)。

   有关 Experience Cloud ID 的更多信息，请参阅 [Experience Cloud ID 概述](https://docs.adobe.com/content/help/zh-Hans/id-service/using/intro/overview.html)和 [Adobe Experience Platform Identity Service](https://docs.adobe.com/content/help/zh-Hans/id-service/using/home.html)。

1. **启用 Adobe Analytics 报表。**

   要启用 Analytics 中的报表并查看您正在收集的内容和广告数据，请参阅[媒体报表启用](/help/media-reports/media-reports-enable.md)。


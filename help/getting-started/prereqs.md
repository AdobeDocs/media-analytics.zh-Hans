---
title: 了解Adobe流媒体服务的先决条件
description: 流媒体服务入门。 了解实施所需的内容。
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 490
ht-degree: 43%

---

# 先决条件 {#prerequisites}

在开始实施Adobe流媒体服务之前，请完成以下任务：

1. **查看Adobe流媒体服务概述**<br>
在开始实施流媒体服务之前，请查看[Adobe流媒体服务概述](/help/media-overview.md)，确保它满足您的需求。

1. **确认您的定价模型**<br>
Customer Journey Analytics流媒体收集加载项和Adobe Analytics for Streaming Media加载项的当前定价模型基于视频流。 如有必要，请联系您的销售代表或Adobe客户团队，因为此加载项是针对Adobe Analytics和Adobe Experience Platform单独销售的。

1. **启用Adobe Analytics报表**<br>
要在Analytics或Customer Journey Analytics中启用报表，并查看所收集的内容和广告数据，您必须启用报表。 请参阅[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

1. **在CX Enterprise中实施Adobe Experience Platform Identity服务**

   **Identity服务**&#x200B;为CX Enterprise核心服务、解决方案以及People核心服务中的客户属性和受众启用通用识别框架。 身份标识服务通过向网站访客分配一个唯一的永久性 ID 来工作。 当您的组织实施ID服务时，此ID允许您在不同的CX企业解决方案中识别同一站点访客及其数据。

   ![ID 服务图形](assets/mc_id_service_graphic.png)

   ID 服务还可以替换解决方案特定的不同 ID（例如，Analytics AID）。 通过[客户ID和身份验证状态](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=zh-Hans)功能，ID服务允许您将自己的客户ID传递到CX Enterprise。 但是，请记住，ID 服务仅适用于您已订阅的解决方案。 如果您未注册访问其他产品，则 ID 服务不提供访问权限。

   ID服务是许多CX Enterprise功能、增强功能和服务中必不可少的组件。 当前，ID 服务支持 [Analytics](https://www.adobe.com/cn/marketing-cloud/web-analytics.html)、[Audience Manager](https://www.adobe.com/cn/marketing-cloud/data-management-platform.html) 和 [Target](https://www.adobe.com/cn/marketing-cloud/testing-targeting.html)。

   如果您还没有实施 ID 服务，现在是时候开始考虑迁移策略了。 有关 ID 服务的重要性和角色的更多信息，请参阅[为什么您应考虑使用身份标识服务](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)。

   有关 Experience Cloud ID 的其他信息，请参阅 [Experience Cloud ID 概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hans)和 [Adobe Experience Platform 身份标识服务](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)。

1. **查看实施方法的其他先决条件**

   根据您计划实施流媒体服务的方式，查看以下任一实施方法的先决条件：

   * [仅限Analytics的实施概述](/help/implementation/analytics-only/overview.md)

   * [Edge实施概述](/help/implementation/edge/overview.md)

   使用[实施概述](/help/implementation/overview.md)确定何种实施方法适合您。

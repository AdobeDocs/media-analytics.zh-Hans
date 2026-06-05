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
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 10%

---

# 先决条件 {#prerequisites}

在开始实施Adobe流媒体服务之前，请完成以下任务：

1. **确认您的定价模型**<br>
Customer Journey Analytics流媒体收集加载项和Adobe Analytics for Streaming Media加载项的当前定价模型基于视频流。 如有必要，请联系您的销售代表或Adobe客户团队，因为此加载项是针对Adobe Analytics和Adobe Experience Platform单独销售的。

1. **启用Adobe Analytics报表** *（仅限Analytics的实施）*<br>
要在Analytics中启用报表并查看所收集的内容和广告数据，您必须启用报表。 请参阅[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

1. **配置身份**<br>

   身份配置要求因实施方法而异：

   * **Edge实施**：身份通过Adobe Experience Platform身份命名空间配置进行处理。 无需设置单独的Identity Service。 有关详细信息，请参阅[Edge实施概述](/help/implementation/edge/overview.md)。

   * **仅限Analytics的实施**：必须启用Adobe Experience Platform Identity Service，才能在CX Enterprise解决方案中一致地识别访客。 Identity Service为每个站点访客分配一个唯一的永久性ID ，并允许在您订阅的所有CX Enterprise解决方案之间共享该ID 。

     有关详细信息，请参阅[Adobe Experience Platform Identity Service文档](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)。

1. **查看实施方法的其他先决条件**

   根据您计划实施流媒体服务的方式，查看以下任一实施方法的先决条件：

   * [仅限Analytics的实施概述](/help/implementation/analytics-only/overview.md)

   * [Edge实施概述](/help/implementation/edge/overview.md)

   使用[实施概述](/help/implementation/overview.md)确定何种实施方法适合您。

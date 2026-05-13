---
title: 如何使用适用于流媒体服务的标记设置移动SDK
description: 了解如何为移动应用程序实施Adobe流媒体服务。
feature: Streaming Media
role: User, Admin, Developer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
TQID: https://experienceleague.adobe.com/IfnXB76Qycsic-ezOzZX4X-5RakbTQ0tlt7va6q2fZ8
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 70%

---

# 安装移动 SDK {#install-mobile-sdks}

要在Android或iOS上实施适用于移动应用程序的Adobe流媒体服务，请安装和配置以下内容：

* **Adobe Experience Platform Mobile SDK**

  要收集数据，请使用以下任一选项：
   * Adobe Experience Platform中的标记。 Adobe Experience Platform 中的标记是一款标记管理解决方案，可让您在满足其他标记要求的同时部署 Analytics 代码。
   * Adobe Experience Platform Edge

* **适用于 Android 的 Media SDK** 或&#x200B;**适用于 iOS 的 Media SDK**

* **Adobe Media Analytics for Audio and Video 扩展**

要下载 SDK 和其他文档资源，请参阅[获取 Media SDK、使用标记的扩展和 OTT SDK](/help/getting-started/download-sdks.md)

* **获取有效的配置参数**

  在设置分析帐户后，这些参数可以从 Adobe 代表获取。

* **在媒体播放器中包含以下 API**

   * *用于订阅播放器事件的 API* – Media SDK 要求在播放器中发生事件时调用一组简单的 API。

   * *提供播放器信息的 API* – 这包括有关当前播放的信息，例如媒体名称、播放头位置、广告或章节。

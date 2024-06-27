---
title: 如何使用适用于流媒体的标记设置移动 SDK
description: 了解如何实施适用于移动应用程序的 Adobe Streaming Media。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 81%

---

# 安装移动 SDK {#install-mobile-sdks}

要在Android或iOS上实施适用于移动应用程序的流媒体收集加载项，请安装和配置以下内容：

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

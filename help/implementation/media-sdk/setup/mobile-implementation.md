---
title: 如何使用适用于流媒体的标记设置移动 SDK
description: 了解如何实施适用于移动应用程序的 Adobe Streaming Media。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: a7d897c6f6fbc6ed0d5b71f5801ab18ee21f0411
workflow-type: ht
source-wordcount: '187'
ht-degree: 100%

---

# 安装移动 SDK {#install-mobile-sdks}

要在 Android 或 iOS 上实施适用于移动应用程序的流媒体，请安装和配置：

* **Adobe Experience Platform Mobile SDK**

   要收集数据，请使用 Adobe Experience Platform 中的标记。Adobe Experience Platform 中的标记是一款标记管理解决方案，可让您在满足其他标记要求的同时部署 Analytics 代码。

* **适用于 Android 的 Media SDK** 或&#x200B;**适用于 iOS 的 Media SDK**

* **Adobe Media Analytics for Audio and Video 扩展**

要下载 SDK 和其他文档资源，请参阅[获取 Media SDK、使用标记的扩展和 OTT SDK](/help/getting-started/download-sdks.md)

* **获取有效的配置参数**

   在设置分析帐户后，这些参数可以从 Adobe 代表获取。

* **在媒体播放器中包含以下 API**

   * *用于订阅播放器事件的 API* – Media SDK 要求在播放器中发生事件时调用一组简单的 API。

   * *提供播放器信息的 API* – 这包括有关当前播放的信息，例如媒体名称、播放头位置、广告或章节。

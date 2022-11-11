---
title: 如何使用适用于流媒体的标记设置Mobile SDK
description: 了解如何为移动设备应用程序实施Adobe流媒体。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 28%

---

# 安装Mobile SDK {#install-mobile-sdks}

要在Android或iOS上为移动设备应用程序实施流媒体，请安装和配置以下内容：

* **Adobe Experience Platform Mobile SDK**

   要收集数据，请使用Adobe Experience Platform中的标记。 Adobe Experience Platform 中的标记是一款标记管理解决方案，可让您在满足其他标记要求的同时部署 Analytics 代码。

* **适用于Android的Media SDK** 或 **适用于iOS的Media SDK**

* **Adobe Media Analytics for Audio and Video 扩展**

要下载SDK和其他文档资源，请参阅 [获取Media SDK、使用标记的扩展以及OTT SDK](/help/getting-started/download-sdks.md)

* **获取有效的配置参数**

   在设置Analytics帐户后，您可以从Adobe代表处获取这些参数。

* **在媒体播放器中包含以下API**

   * *用于订阅播放器事件的 API* - Media SDK 要求在播放器中发生事件时调用一组简单的 API。

   * *提供播放器信息的API*  — 这包括有关当前播放的信息，如媒体名称、播放头位置、广告或章节。

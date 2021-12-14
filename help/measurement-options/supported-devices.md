---
title: 了解支持的设备和平台
description: “了解适用于流媒体的 Adobe Analytics 支持的主要设备，例如 iOS、Android、OTT 设备和 JavaScript 浏览器。”
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f0abffb48a6c0babb37f16aff2e3302bf5dd0cb4
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 98%

---

# 支持的设备和平台 {#devices-supported}

>[!IMPORTANT]
>
>Adobe 将于 2021 年 8 月 31 日终止支持版本 4 Mobile SDK，届时还将终止对适用于 iOS 和 Android 的 Media Analytics SDK 的支持。有关更多信息，请参阅 [Media Analytics SDK 支持终止常见问题解答](/help/sdk-implement/end-of-support-faqs.md)。

适用于流媒体的 Adobe Analytics 支持所有主要设备，包括：

* iOS 和 Android 智能手机和平板电脑
* 适用于 ROKU、AppleTV、FireTV 和 Android TV 的 OTT 设备
* 适用于台式机和笔记本电脑的 JavaScript 浏览器

当设备有新版本发布时，Adobe 会对 Media SDK 进行定期更新，您可以使用相应的 SDK 与当今的主流媒体播放器进行集成，包括 Brightcove 和 Ooyala。

对于当前不支持 SDK 的设备或平台，或者如果您不想使用 SDK，则可以实施媒体收集 API。媒体收集 API 允许您直接从设备或平台向 Media Analytics 后端发起 RESTful API 调用。

下表列出了当前支持的设备和平台。要下载最新版本的 SDK，请参阅[下载 SDK](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/download-sdks.html?lang=zh-Hans)。对于表中未列出的设备，请联系客户关怀团队或解决方案顾问以了解该设备的状态。

| 流平台和设备 |  | 使用AEP Mobile SDK收集数据 | Media SDK | 媒体收集 API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/移动 Web |  |  |  |  |
|  | JavaScript 浏览器 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| 移动设备应用程序 |  |  |  |  |
|  | iOS 设备 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android 设备 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows 设备 |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV  (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>（本机） |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | 游戏机（例如 Xbox ONE、Sony PS3/PS4） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 机顶盒（例如 xfinity X1） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 智能电视（例如，Samsung、LG、Sony、Vizio） |  | ![](/help/assets/icon-blue-check.png)   <br>（基于 Web）    | ![](/help/assets/icon-blue-check.png) |
| 其他 |  |  |  |  |
|  | 新型互联设备 |  |  | ![](/help/assets/icon-blue-check.png) |

1. 将于 2021 年 8 月 31 日终止对这些 SDK 的支持。有关更多信息，请参阅 [Media Analytics SDK 支持终止常见问题解答](/help/sdk-implement/end-of-support-faqs.md)。

有关每个 SDK 支持的最低平台版本的更多信息，请参阅[最低平台版本支持](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-overview.html?lang=zh-Hans)

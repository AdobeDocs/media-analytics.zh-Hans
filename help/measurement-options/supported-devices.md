---
title: 支持的设备和平台
description: Adobe Analytics for Audio and Video确保在所有设备上收集和报告每个媒体流。
translation-type: tm+mt
source-git-commit: a8fec1747e688473af7a5eabbc4f9968772b5db3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 15%

---


# 支持的设备和平台 {#devices-supported}

>[!IMPORTANT]
>
>随着2021年8月31日停止对版本4 Mobile SDK的支持，Adobe还将结束对适用于iOS和Android的Media Analytics SDK的支持。  有关其他信息，请 [参阅Media Analytics SDK支持终止常见问题解答](/help/sdk-implement/end-of-support-faqs.md)。

Adobe Analytics for Audio and Video支持所有主要设备，包括：

* iOS 和 Android 智能手机和平板电脑
* 适用于 ROKU、AppleTV、FireTV 和 Android TV 的 OTT 设备
* 适用于台式机和笔记本电脑的 JavaScript 浏览器

当发布新版本的设备时，Media SDK会例行更新，您可以使用SDK与当今最大的媒体播放器（包括Brightcove和Ooyala）集成。

对于当前不支持SDK的设备或平台，或者在您不想使用SDK的情况下，您可以实施Media Collection API。 Media Collection API允许您直接从设备或平台向Media Analytics后端进行REST风格的API调用。

下表列出了列表当前支持的设备和平台。 要下载最新版本的 SDK，请参阅[下载 SDK](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html)。如果未列出设备，请联系客户关怀或解决方案顾问以了解该设备的状态。

| 流平台和设备 |  | 带有AEP SDK的Media Launch Extension | Media SDK | 媒体收集 API |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/移动Web |  |  |  |  |
|  | JavaScript浏览器 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| 移动设备应用程序 |  |  |  |  |
|  | iOS 设备 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android 设备 | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Windows设备 |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV(tvOS) | 计划2020年 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | 罗库 |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>（本机） |
|  | Fire TV(Fire OS) | 计划2020年 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | 计划2020年 | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | 游戏控制台（例如Xbox ONE、Sony PS3/PS4） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 设置顶部框（如xfinity X1） |  |  | ![](/help/assets/icon-blue-check.png) |
|  | 智能电视（例如，Samsung、LG、Sony、Vizio） |  | ![](/help/assets/icon-blue-check.png)   <br>（基于Web）    | ![](/help/assets/icon-blue-check.png) |
| 其他 |  |  |  |  |
|  | 新的连接设备 |  |  | ![](/help/assets/icon-blue-check.png) |

1. 对这些SDK的支持将于2021年8月31日终止。 有关其他信息，请 [参阅Media Analytics SDK支持终止常见问题解答](/help/sdk-implement/end-of-support-faqs.md)。

有关每个SDK支持的最低平台版本的更多信息，请参 [阅最低平台版本支持](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/setup/setup-overview.html)

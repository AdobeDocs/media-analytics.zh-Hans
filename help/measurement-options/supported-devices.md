---
title: 支持的设备
description: null
uuid: null
translation-type: tm+mt
source-git-commit: c86c7932f932af0a121e0b757921973d6f4084e8

---


# 支持的设备 {#devices-supported}

Adobe Analytics for Audio and Video确保在所有设备上收集和报告每个媒体流。

Adobe Analytics for Audio and Video支持所有主要设备，包括：

* iOS 和 Android 智能手机和平板电脑
* 适用于 ROKU、AppleTV、FireTV 和 Android TV 的 OTT 设备
* 适用于台式机和笔记本电脑的 JavaScript 浏览器

当发布新版本的设备时，Media SDK会例行更新，您可以使用SDK与当今最大的媒体播放器（包括Brightcove和Ooyala）集成。

对于当前不支持SDK的设备或平台，或者在您不想使用SDK的情况下，您可以实施Media Collection API。 Media Collection API允许您直接从设备或平台向Media Analytics后端进行REST风格的API调用。

下表列表了当前支持的设备。 要下载最新版本的 SDK，请参阅[下载 SDK](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/download-sdks.html)。如果未列出设备，请联系客户关怀或解决方案顾问以了解该设备的状态。


| 流平台／设备 |  | 带有AEP SDK的Media Launch Extension | Media SDK | 媒体收集 API |
|---------------------------|-----------------------------------------------|:----------------------------:|:-------------------:|:--------------------:|
| Web/移动Web |  |  |  |  |
|  | JavaScript浏览器 | X | X | X |
| 移动设备应用程序 |  |  |  |  |
|  | iOS 设备 | X | X | X |
|  | Android 设备 | X | X | X |
|  | Windows设备 |  |  | X |
| OTT |  |  |  |  |
|  | Apple TV（传统、TVOS） |  | X | X |
|  | 罗库 |  | X<br>(BrightScript) | X<br>（本机） |
|  | Fire TV(Fire OS) |  | X | X |
|  | Android TV |  | X | X |
|  | Chromecast |  | X | X |
|  | 游戏控制台（例如Xbox ONE、Sony PS3/PS4） |  |  | X |
|  | 设置顶部框（如xfinity X1） |  |  | X |
|  | 智能电视（例如，Samsung、LG、Sony、Vizio） |  | X<br>（基于Web） | X |
| 其他 |  |  |  |  |
|  | 新的连接设备 |  |  | X |


有关 Media SDK 的信息，另请参阅[最低平台版本支持](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

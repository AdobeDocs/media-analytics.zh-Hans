---
title: 了解支持的设备和平台
description: “了解 Adobe Analytics for Streaming Media 支持的主要设备，例如 iOS、Android、OTT 设备和 JavaScript 浏览器。”
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin
source-git-commit: 7eeee7f035e5d9e7e327e60910c78bbdf02abff8
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 59%

---

# 支持的设备和平台 {#devices-supported}

适用于流媒体的Adobe Analytics支持所有主要设备，包括：

* iOS 和 Android 智能手机和平板电脑
* 适用于 Roku、Fire TV 和 Android TV 的 OTT 设备
* 适用于台式机和笔记本电脑的 JavaScript 浏览器

当发布设备的新版本时，SDK会定期更新，您可以使用SDK与每个平台的原生播放器或任何其他可用的媒体播放器集成。

对于当前不支持SDK的设备，或者在您可能需要自定义实施的情况下，您可以使用媒体收集API或媒体边缘API。 这些API允许您直接从设备向Media Analytics后端进行RESTful API调用。

下表列出当前支持的设备。如果未列出某个设备，请联系客户关怀团队或解决方案顾问以了解该设备的状态。

有关在Edge上实施Media的更多信息，请参阅 [安装Media Analytics和Experience Platform边缘](/help/implementation/edge/implementation-edge.md).

| 流平台和设备 | | Media for Edge Network SDK/扩展 | Media Edge API | 包含标记或AEP Mobile SDK的Media扩展 | Media SDK | 媒体收集 API |
|:---|:---|:---:|:---:|:---:|:---:|:---:|
| Web/移动 Web | | | | | |
| | JavaScript 浏览器 | （即将推出） | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) |
| 移动设备应用程序 | | | | | |
| | iOS 设备 | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | | ![支持](/help/assets/icon-blue-check.png) | |
| | Android 设备 | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | | ![支持](/help/assets/icon-blue-check.png) |
| | Windows 设备 | | ![支持](/help/assets/icon-blue-check.png) | | | ![支持](/help/assets/icon-blue-check.png) |
| OTT | | | | | | |
| | Apple TV  (tvOS) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | | ![支持](/help/assets/icon-blue-check.png) |
| | Roku | （正在计划） | ![支持](/help/assets/icon-blue-check.png) | | ![支持](/help/assets/icon-blue-check.png)<br>（BrightScript） | ![支持](/help/assets/icon-blue-check.png)<br>（本地） |
| | Fire TV (Fire OS) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | | ![支持](/help/assets/icon-blue-check.png) |
| | Android TV | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) | | ![支持](/help/assets/icon-blue-check.png) |
| | Chromecast | | ![支持](/help/assets/icon-blue-check.png) | | ![支持](/help/assets/icon-blue-check.png) | ![支持](/help/assets/icon-blue-check.png) |
| | 游戏机（例如 Xbox ONE、Sony PS3/PS4） | | ![支持](/help/assets/icon-blue-check.png) | | | ![支持](/help/assets/icon-blue-check.png) |
| | 机顶盒（例如 xfinity X1） | | ![支持](/help/assets/icon-blue-check.png) | | | ![支持](/help/assets/icon-blue-check.png) |
| | 智能电视（例如，Samsung、LG、Sony、Vizio） | | ![支持](/help/assets/icon-blue-check.png) | | | ![支持](/help/assets/icon-blue-check.png) |
| 其他 | | | | | | |
| | 新型互联设备 | | ![支持](/help/assets/icon-blue-check.png) | | | ![支持](/help/assets/icon-blue-check.png) |

{style="table-layout:auto"}

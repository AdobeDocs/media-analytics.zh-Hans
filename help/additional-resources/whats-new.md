---
title: Media Analytics 的新增功能
description: 新增功能包括有关新功能和声明的信息。
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '607'
ht-degree: 100%

---


# Media Analytics 的新增功能{#whats-new}

![横幅](assets/media_analytics_banner.png)


此页面介绍了 Media Analytics 中的新功能、修复和重要声明。此外，还重点提供了可帮助您充分利用 Media Analytics 的新文档、培训课程和视频教程。


## 发行说明

Adobe Experience Cloud 发行说明

《Adobe Experience Cloud 发行说明》介绍了 Adobe Experience Cloud 中的新功能、修复和重要声明，其中包括对 Media Analytics 的最新更改。此外，还重点提供了可帮助您充分利用 Experience Cloud 的新文档、培训课程和视频教程。

## 新增功能

| 功能 | [正式发布](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html?lang=zh-Hans) — 目标日期 | 描述 |
| ----------- | ---------- | ---------- |
| [“媒体并行查看者”面板](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 2020 年 9 月 17 日 | 通过工作区中的“媒体并行查看者”面板，您可以了解出现并发峰值或发生锐减的位置。它为内容质量和查看者参与度提供了有价值的分析，同时有助于对批量/规模进行疑难问题解答或规划。 |
| [支持的设备和平台](../getting-started/supported-devices.md) | 2020 年 6 月 18 日 | 包含 AEP Mobile SDK 的 [!UICONTROL Media Launch 扩展]现在支持以下 OTT 设备：<ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul> |
| [播放器状态跟踪](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/player-state-overview.html?lang=zh-Hans) | 2020 年 5 月 29 日 | [!UICONTROL Media Analytics] 客户可以运用一组适用于全屏、隐藏式字幕、静音、画中画和聚焦的标准解决方案变量，捕获视频播放期间观看者的交互信息。您还可以灵活地创建自定义播放器状态。[!UICONTROL 播放器状态跟踪]变量现在可以在 [!UICONTROL Analysis Workspace] 中进行报告。此功能需要以下任一项： <ul><li>Media [!DNL JavaScript] SDK 3.0 或更高版本</li><li>与 [!DNL Adobe Experience Platform] (AEP) SDK 一起使用时：</li><li>[!UICONTROL Media Analytics 扩展]（用于 Web）：[!UICONTROL Adobe Media Analytics] (3.x SDK) for Audio and Video v1.0 或更高版本</li><li>[!UICONTROL Media Analytics 扩展]（用于移动设备）：[!UICONTROL Adobe Media Analytics for Audio] and Video v2.0 或更高版本</li><li>[!UICONTROL 媒体收集]</li></ul> |


## 重要声明

| 功能 | [正式发布](https://experienceleague.adobe.com/docs/analytics/landing/an-releases.html?lang=zh-Hans) — 目标日期 | 描述 |
| ----------- | ---------- | ---------- |
| [支持的设备和平台](../getting-started/supported-devices.md) | 2021 年 8 月 31 日 | Adobe 将于 2021 年 8 月 31 日终止支持版本 4 Mobile SDK，届时还将终止对适用于 iOS 和 Android 的 Media Analytics SDK 的支持。有关更多信息，请参阅 Media Analytics SDK 支持终止常见问题解答。 |
| [Media Analytics SDK 终止支持常见问题解答](sdk-implement/end-of-support-faqs.md) | Fall 2019 | 已终止适用于 iOS 和 Android 的 Media Analytics SDK 的功能开发。从 2019 年秋季开始引入的新功能均通过 Media Analytics 扩展和媒体收集 API 启用。 |
| [媒体概览](media-overview.md) | 2019 年 2 月 20 日 | Adobe 仅支持 TLS 1.1 或更高版本。伴随这项变化，对于使用部署了 TLS 1.0 的较旧设备或 Web 浏览器的最终用户，Adobe 将不再收集他们的数据。 |
| [支持的设备和平台](../getting-started/supported-devices.md) | 2019 年 2 月 19 日 | 下面列出了每个 SDK 支持的最低平台版本。<br>- iOS：iOS 6 及更高版本<br>- Android：Android 5.0 及更高版本 - Lollipop <br>- Chrome：v22 及更高版本<br>- Mozilla：v27 及更高版本<br>- Safari：v7 及更高版本<br>- IE：v1 及更高版本 |
| [音频和视频参数](metrics-and-metadata/audio-video-parameters.md) | 2019 年 2 月 7 日 | Adobe Analytics for Video and Audio 发布了一项量度名称变更。“媒体启动”<i></i>现在将更名为“媒体开始”<i></i>。此名称变更是为了遵循量度和报表的行业标准，并使该量度可在报表中轻松识别。 |
| [音频和视频参数](metrics-and-metadata/audio-video-parameters.md) | 2018 年 9 月 13 日 | 一些维度、量度和报表的标签发生了更改，以便允许对视频和音频分析进行跨内容跟踪。已更改的标签包括：*视频初始化*&#x200B;改为&#x200B;*媒体初始化*、*视频长度*&#x200B;改为&#x200B;*内容时长*、*视频名称*&#x200B;改为&#x200B;*内容名称*。Reports and Analytics 中的视频报表均已更新为使用“媒体”名称而非“视频”。标签更改不会更改数据收集或历史数据。如果您在 Report Builder 中或任何其他可能受此更改影响的外部自动数据提取中使用这些标签，请注意这些更改。 |




<!-- | title | date | description | -->

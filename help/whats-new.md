---
title: 媒体分析的新增功能
description: 新增功能包括有关新增功能和通知的信息。
translation-type: tm+mt
source-git-commit: dfffcf1e1d815ca178e0bdba881d973d60fe1631
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 66%

---


# 媒体分析的新增功能{#whats-new}

![横幅](assets/media_analytics_banner.png)


本页介绍Media Analytics的新增功能、修复和重要注意事项。 它还重点介绍新文档、培训课程和视频教程，帮助您充分利用媒体分析。


## 发行说明

Adobe Experience Cloud 发行说明

《Adobe Experience Cloud发行说明》描述了Adobe Experience Cloud的新功能、修复和重要注意事项。 这包括对Media Analytics的最新更改。 此外，还重点提供了可帮助您充分利用 Experience Cloud 的新文档、培训课程和视频教程。

## 新增功能

| 功能 | [正式发布](https://docs.adobe.com/content/help/zh-Hans/analytics/landing/an-releases.html) - 目标日期 | 描述 |
| ----------- | ---------- | ---------- |
| [“媒体并发查看器”面板](media-reports/media-workspace-panels/media-concurrent-viewers.md) | 2020 年 9 月 17 日 | 使用工作区中的“媒体并发查看器”面板，您可以了解高峰期并发发生的位置或中断发生的位置。 它为内容质量和查看者参与度提供了有价值的分析，同时有助于对批量/规模进行疑难问题解答或规划。 |
| [支持的设备和平台](https://docs.adobe.com/content/help/zh-Hans/media-analytics/using/supported-devices.html) | 2020 年 6 月 18 日 | 带有AEP Mobile SDK的[!UICONTROL 媒体启动扩展]现在支持以下OTT设备：<ul><li>Apple TV  (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul> |
| [播放器状态跟踪](https://docs.adobe.com/content/help/zh-Hans/media-analytics/using/player-state-tracking/player-state-overview.html) | 2020 年 5 月 29 日 | [!UICONTROL Media Analytics] 客户可以运用一组适用于全屏、隐藏式字幕、静音、画中画和聚焦的标准解决方案变量，捕获视频播放期间观看者的交互信息。您还可以灵活地创建自定义播放器状态。[!UICONTROL 播放器状态跟踪]变量现在可以在 [!UICONTROL Analysis Workspace] 中进行报告。此功能需要以下任一项： <ul><li>Media [!DNL JavaScript] SDK 3.0 或更高版本</li><li>与 [!DNL Adobe Experience Platform] (AEP) SDK 一起使用时：</li><li>[!UICONTROL Media Analytics 扩展]（用于 Web）：[!UICONTROL Adobe Media Analytics] (3.x SDK) for Audio and Video v1.0 或更高版本</li><li>[!UICONTROL Media Analytics 扩展]（用于移动设备）：[!UICONTROL Adobe Media Analytics for Audio] and Video v2.0 或更高版本</li><li>[!UICONTROL 媒体收集]</li></ul> |


## 重要通知

| 功能 | [正式发布](https://docs.adobe.com/content/help/en/analytics/landing/an-releases.html) - 目标日期 | 描述 |
| ----------- | ---------- | ---------- |
| [支持的设备和平台](https://docs.adobe.com/content/help/en/media-analytics/using/supported-devices.html) | 2021年8月31日 | Adobe 将于 2021 年 8 月 31 日终止支持版本 4 Mobile SDK，届时还将终止对适用于 iOS 和 Android 的 Media Analytics SDK 的支持。有关更多信息，请参阅 Media Analytics SDK 支持终止常见问题解答。 |
| [Media Analytics SDK 终止支持常见问题解答](sdk-implement/end-of-support-faqs.md) | Fall 2019 | 针对iOS和Android的Media Analytics SDK的功能开发已结束。  从 2019 年秋季开始引入的新功能均通过 Media Analytics 扩展和媒体收集 API 启用。 |
| [媒体概览](media-overview.md) | 2019 年 2 月 20 日 | Adobe仅支持TLS 1.1或更高版本。 通过此更改，Adobe将不再使用部署TLS 1.0的较旧设备或Web浏览器从最终用户收集数据。 |
| [支持的设备和平台](https://docs.adobe.com/content/help/en/media-analytics/using/supported-devices.html) | 2019 年 2 月 19 日 | 下面列出了每个SDK支持的最低平台版本。 <br>- iOS:iOS 6+  <br>- Android:Android 5.0+ —— 棒棒糖- <br>铬黄：v22+<br>- Mozilla:v27+<br>- Safari:v7+<br>- IE:v1+ |
| [音频和视频参数](metrics-and-metadata/audio-video-parameters.md) | 2019 年 2 月 7 日 | Adobe Analytics的视频和音频部门发布了度量名称更改。 “媒体启动”<i></i>现在将更名为“媒体开始”<i></i>。此名称变更是为了遵循量度和报表的行业标准，并使该量度可在报表中轻松识别。 |
| [音频和视频参数](metrics-and-metadata/audio-video-parameters.md) | 2018 年 9 月 13 日 | 对某些维度、指标和报告的标签进行了更改，以允许跨内容跟踪视频和音频分析。 已更改的标签包括：*视频初始化*&#x200B;改为&#x200B;*媒体初始化*、*视频长度*&#x200B;改为&#x200B;*内容时长*、*视频名称*&#x200B;改为&#x200B;*内容名称*。Reports and Analytics 中的视频报表均已更新为使用“媒体”名称而非“视频”。标签更改不会更改数据收集或历史数据。如果您在 Report Builder 中或任何其他可能受此更改影响的外部自动数据提取中使用这些标签，请注意这些更改。 |




<!-- | title | date | description | -->

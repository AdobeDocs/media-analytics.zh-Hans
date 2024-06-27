---
title: 流媒体收集加载项发行说明
description: 查看流媒体收集加载项发行说明。
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 75%

---

# 流媒体收集附加组件发行说明（2023年5月）

**上次更新**：2024年5月29日

## 相关资源

有关新功能和修复的信息以及面向管理员的重要信息，请参阅以下资源。

* [Adobe Analytics 发行说明](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=en)
* [Customer Journey Analytics 发行说明](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html)
* [Adobe Experience Cloud 产品](https://business.adobe.com/products/adobe-experience-cloud-products.html)的最新版本更新

* [Adobe Analytics 教程](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en)

## *最新发行说明*

## Adobe流媒体收集加载项中的新增功能和更新功能 {#cja-features}

| 功能 | 描述 | 预定日期 |
| ----------- | ---------- | ------- |
| 使用Web SDK将Web数据发送到Adobe Experience PlatformEdge Network | 您现在可以 [使用Adobe Experience Platform Web SDK将流媒体Web数据发送到Adobe Experience PlatformEdge Network](/help/implementation/edge/edge-web-sdk.md)，可让您构建更个性化的促销活动并提供更个性化的内容，从而产生要报告的更多跟踪数据。<p>此增强功能为所有平台解决方案（例如 Customer Journey Analytics、RT-CDP、AJO 和事件转发）的 Web 实现提供了统一的收集方法。以前，将流媒体Web数据发送到Edge Network的唯一方法是使用Media Edge API。 | 2024 年 5 月 29 日 |
| 将Roku数据发送到Adobe Experience Platform Edge | 现在，当 [使用Experience PlatformEdge安装流媒体收集加载项](/help/implementation/edge/implementation-edge.md)中，您可以使用Adobe Experience Platform Roku SDK将流媒体数据发送到Adobe Experience Platform。 | 2024 年 4 月 12 日 |
| 媒体收集：与Experience Edge （API和移动SDK）的集成 | 您现在可以使用Experience Edge API和Mobile SDK实施Adobe流媒体收集加载项，从而构建更个性化的促销活动并提供更个性化的内容，从而产生要报告的更多跟踪数据。<p>此增强功能提供了跨所有解决方案(如Customer Journey Analytics报告、RT-CDP、AJO和事件转发)的统一收集方法。  [了解详情](/help/implementation/edge/implementation-edge.md) | 2023年5月12日 |
| “媒体并行查看者”面板 | 了解同时观看的人数在哪里达到峰值或在哪里发生下降。获得关于内容质量和观众参与情况的宝贵洞察，并帮助进行故障排除或规划数量和规模。 [了解详情](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=en) | 2022 年 8 月 9 日 |
| “Media Playback 耗时”面板 | Media Playback 耗时提供有关查看者参与情况的宝贵洞察，并使媒体组织能够通过具备时段分割功能的高级耗时分析，利用以分钟计的用户参与获得更深入、更精细的洞察。 您可以观察在特定时间点查看媒体流的耗时。您可以按不同的粒度分割播放时长，包括新的 5 分钟、15 分钟和 30 分钟粒度。[了解详情](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html) | 2022 年 8 月 9 日 |
| 在移动记分卡中共享批注 | 您可以在移动记分卡中显示在工作区中创建的批注。这允许您直接在移动记分卡项目中共享有关您的组织和活动的上下文数据细微差别和见解，可在 Analytics 功能板移动应用程序中查看。[了解详情](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=en) | 2022 年 6 月 15 日 |
| Customer Journey Analytics更新Report Builder | 包括调度和数据块管理器等功能。[了解详情](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html) | 2022 年 5 月 18 日 |
| 工作区批注 | 工作区批注使您能够有效地将上下文数据的细微差别和见解传达给您的组织。[了解详情](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html) | 将于 2022 年 3 月 23 日开始逐步推出 |
| 移动记分卡项目预览模式 | 直接从记分卡生成器中预览您的移动记分卡在 Analytics 功能板应用程序中的外观。预览模式允许用户以与在该应用程序中相同的方式与过滤器和图表进行交互，使用户可以在保存和共享记分卡之前预览体验。用户还可以在预览模式下使用设备选择器来查看自己的记分卡在不同设备上的外观。[了解详情](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html#preview) | 2022 年 2 月 16 日 |


## Adobe流媒体收集加载项中的新增功能和更新功能 {#sm-features}

| 功能 | 描述 | 预定日期 |
| ----------- | ---------- | ------- |
| 多个播放器状态跟踪 | 使用媒体收集 API 实施多个播放器状态跟踪。[了解详情](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html) | 2022 年 9 月 |
| 重命名的 XDM 字段 | 已重命名 XDM 字段名称以保持一致性：<br>*音频和视频参数<br>*广告参数<br>*章节参数<br>*播放器状态参数<br>*质量参数 | 2022 年 9 月 |
| 设备协作参考 | 已移除 Adobe Experience Cloud 设备协作参考和 Experience Cloud ID 服务要求。 | 2022 年 8 月 |
| 已更新用于收集和报告的字段名称和 XDM 路径 | 已更新以下内容：<br>*音频和视频参数<br>*广告参数<br>*章节参数<br>*播放器状态参数<br>*质量参数 | 2022 年 8 月 |
| 平均受众访问分钟数 | Media Analytics 客户可以使用“平均受众访问分钟数”面板来更好地了解内容平均使用情况。<br>平均受众访问分钟数可以比较任何长度或类型的编程。此外，您可以将此数字平均受众访问分钟数与线性电视平均访问分钟数指标进行比较或附加到其上。此面板提供了更大的灵活性来衡量自定义时间段的平均受众访问，以及持续时间分类更新的时间。[了解详情](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=en) | 2022 年 3 月 16 日 |
| “Media Playback 耗时”面板 | 了解“Media Playback 耗时”面板如何使媒体用户能够通过一天中所选粒度的观看时间量来了解他们的收视率。<br>[“Media Playback 耗时”面板（教程）](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=zh-Hans) | 2022 年 1 月 |


## *以前的发行说明*

| 功能 | 描述 | 预定或更新日期 |
| ----------- | ---------- | -------------- |
| Media Playback 耗时 | Adobe 流媒体播放耗时提供有关观众参与情况的宝贵见解，并使媒体组织能够通过具备时段分割功能的高级耗时分析，利用以分钟计的用户参与获得更深入、更精细的见解。您可以观察在特定时间点查看媒体流的耗时。可按多种不同的粒度分割播放时长，包括新的 5 分钟、15 分钟和 30 分钟粒度。[了解详情...](/help/reporting/workspace/media-playback-time-spent.md) | 2021 年 9 月 |
| Analytics Workspace 中的“媒体并行查看者”面板 | 了解同时观看的人数在哪里达到峰值或在哪里发生下降。获得关于内容质量和观众参与情况的宝贵洞察，并帮助进行故障排除或规划数量和规模。 [了解详情…](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Analytics Workspace 中的“媒体并行查看者”面板（教程）](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=zh-Hans#analysis-workspace) | 2020 年 9 月<br><br><br>2021 年 1 月 |
| 支持的设备和平台 | Media Launch Extension w/ AEP SDK 现在支持以下 OTT 设备： <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | 2020 年 6 月 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->

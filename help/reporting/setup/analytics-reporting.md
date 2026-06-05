---
title: 为仅限Analytics的实施设置报表
description: 在Adobe Analytics中启用媒体报表包模块，以便收集和报告流媒体数据。
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 11%

---

# 为仅限Analytics的实施设置报表

在仅限于Analytics的实施可以收集流媒体数据之前，必须将接收该数据的每个报表包配置为启用相应的媒体模块。 本页介绍如何启用这些模块以及在何处查找生成的报表。

* **先决条件**： Adobe Analytics实施。 查看[仅限Analytics的实施概述](/help/implementation/analytics-only/overview.md)以及您选择的实施方法。

## 在报表包中启用媒体报告

收集媒体量度的每个报表包必须在发送媒体数据之前进行配置。

1. 在[Adobe Analytics](https://experience.adobe.com/analytics)中，导航到&#x200B;**[!UICONTROL 管理员]** → **[!UICONTROL 报表包]**。
1. 选择收集媒体数据的报表包。 选择&#x200B;**[!UICONTROL 编辑设置]** → **[!UICONTROL 媒体管理]** → **[!UICONTROL 媒体报告]**。

   ![报表包管理器菜单屏幕截图](assets/media-reporting.png)

1. 在&#x200B;**[!UICONTROL 媒体报表]**&#x200B;页面上，启用所需的流媒体模块（请参阅下文）。

1. 选择&#x200B;**[!UICONTROL 保存].**

   如果此报表包已配置为收集媒体数据，则在选择&#x200B;**[!UICONTROL 保存]**&#x200B;后，将显示额外的配置页面。 如果您看到&#x200B;**[!UICONTROL “媒体核心”测量]**&#x200B;页面，请继续执行下一步。

## 可用的流媒体模块

媒体测量包括以下模块：

* **[!UICONTROL 媒体核心]**：所有流媒体跟踪均需要。 它保留用于内容播放和会话数据的解决方案变量。

  +++选择以查看维度和量度

   * **维度：**
      * [[!UICONTROL 内容]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL 内容渠道]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL 内容长度（变量）]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL 内容名称（变量）]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL 内容播放器名称]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL 内容区段]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL 内容类型]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL 媒体路径]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL 媒体会话ID]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL 流类型]](/help/reporting/dimensions/stream-type.md)
   * **量度：**
      * [[!UICONTROL 平均受众访问分钟数]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL 内容完成]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL 内容继续]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL 内容区段视图]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL 内容开始]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL 媒体开始]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL 暂停事件]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL 受暂停影响的流]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL 进度标记]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL 总暂停持续时间]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL 唯一播放时间]](/help/reporting/metrics/unique-time-played.md)

  +++

* **[!UICONTROL 媒体广告]**：启用媒体内容中的广告跟踪。

  +++选择以查看维度、分类和量度

   * **维度：**
      * [[!UICONTROL 广告]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL 面板中的广告位置]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL 广告长度（变量）]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL 广告名称（变量）]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL 广告播放器名称]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL 广告Pod]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL 广告商]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL 营销活动 ID]](/help/reporting/dimensions/campaign-id.md)
   * **分类维度：**
      * [[!UICONTROL 资产ID]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL 内容评级]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL 首次播放日期]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL 第一个数字日期]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL 面板名称]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Pod位置]](/help/reporting/dimensions/pod-position.md)
   * **量度：**
      * [[!UICONTROL 广告完成]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL 广告开始]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL 广告逗留时间]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL 媒体逗留时间]](/help/reporting/metrics/media-time-spent.md)

  +++

* **[!UICONTROL 媒体章节]**：启用媒体内容中章节的跟踪。

  +++选择以查看维度、分类和量度

   * **Dimension：**
      * [[!UICONTROL 章节]](/help/reporting/dimensions/chapter.md)
   * **分类维度：**
      * [[!UICONTROL 章节长度]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL 章节名称]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL 章节偏移]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL 章节位置]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL 发起人]](/help/reporting/dimensions/originator.md)
   * **量度：**
      * [[!UICONTROL 章节完成]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL 章节开始]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL 章节逗留时间]](/help/reporting/metrics/chapter-time-spent.md)

  +++

* **[!UICONTROL 媒体质量]**：启用播放质量数据跟踪，包括缓冲、比特率和错误事件。

  +++选择以查看维度和量度

   * **维度：**
      * [[!UICONTROL 平均比特率]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL 比特率更改]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL 缓冲事件]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL 丢帧]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL 个错误]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL 外部错误ID]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL 播放器SDK错误ID]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL 开始时间]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL 总缓冲持续时间]](/help/reporting/dimensions/total-buffer-duration.md)
   * **量度：**
      * [[!UICONTROL 平均比特率]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL 受比特率更改影响的流]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL 比特率更改]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL 缓冲事件]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL 受缓冲影响的流]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL 受丢帧影响的流]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL 丢帧]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL 开始前丢弃]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL 错误事件]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL 错误影响的流]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL 开始时间]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL 总缓冲持续时间]](/help/reporting/metrics/total-buffer-duration.md)

  +++

* **[!UICONTROL 视频元数据]**：启用对标准视频内容属性（如节目、季度和流派）的跟踪。

  +++选择以查看维度和量度

   * **维度：**
      * [[!UICONTROL 个广告加载]](/help/reporting/dimensions/ad-load-type.md)
      * [[!UICONTROL 天部分]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL 集]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL 流派]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL 媒体馈送类型]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL 网络]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL 季]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL 节目]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL 显示类型]](/help/reporting/dimensions/show-type.md)
   * **指标：**
      * [[!UICONTROL 已授权]](/help/reporting/metrics/authorized.md)

  +++

* **[!UICONTROL 音频元数据]**：启用对标准音频内容属性的跟踪，例如演出者、专辑和电台。

  +++选择以查看维度

   * **维度：**
      * [[!UICONTROL 相册]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL 艺人]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL 作者]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Label]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL 发布者]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL 工作站]](/help/reporting/dimensions/station.md)

  +++

* **[!UICONTROL 播放器状态跟踪]**：启用标准播放器UI状态的测量，如全屏、隐藏式字幕和画中画。

  +++选择以查看指标

   * **量度：**
      * [[!UICONTROL 隐藏式字幕计数]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL 隐藏式字幕总时长]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL 全屏计数]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL 全屏总时长]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL 聚焦计数]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL 观看中总持续时间]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL 静音计数]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL 静音总持续时间]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL 画中画计数]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL 画中画总持续时间]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL 受隐藏式字幕影响的流数量]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL 受全屏影响的流数量]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL 受聚焦影响的流数量]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL 受静音影响的流数量]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL 受画中画影响的流数量]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)

  +++

## Adobe Analytics中的可用媒体面板

Analysis Workspace包括三个专用媒体面板，面向具有Adobe Analytics for Streaming Media加载项的客户。 这些面板提供了预建的可视化图表，可满足最常见的流媒体报表需求。

* **[媒体平均受众访问分钟数](https://experienceleague.adobe.com/zh-hans/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel)**：比较任意长度或类型的程序的平均内容使用量。 支持特定内容（基于持续时间）和自定义时段模式，并允许事后更新持续时间分类。
* **[媒体并行查看者](https://experienceleague.adobe.com/zh-hans/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers)**：分析一段时间内的并行查看者，以确定并发峰值和流失点。 支持可配置的粒度和按区段、维度或日期范围划分的系列。
* **[媒体播放耗时](https://experienceleague.adobe.com/zh-hans/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent)**：分析一段时间的播放持续时间，提供关于高峰期和低谷期的详细信息。 支持可配置的粒度和输出格式（小时或分钟）。

>[!MORELIKETHIS]
>
>* [维度概述](/help/reporting/dimensions/overview.md)
>* [量度概述](/help/reporting/metrics/overview.md)

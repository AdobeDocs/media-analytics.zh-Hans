---
title: Adobe Experience Platform和Customer Journey Analytics的Media Analytics参数映射
description: 与Analytics Source Connector和Customer Journey Analytics一起使用的Media Analytics参数的XDM字段路径映射。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 1331
ht-degree: 19%

---

# Adobe Experience Platform和Customer Journey Analytics的Media Analytics参数映射

本文档全面列出了Adobe Experience Platform和Customer Journey Analytics中使用的所有Media Analytics参数。 它旨在支持将通过[Analytics Source Connector](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/analytics)或[Analytics Source Connector for Classifications](https://experienceleague.adobe.com/cn/docs/experience-platform/sources/connectors/adobe-applications/classifications)从Adobe Analytics导入的数据集成到Platform，并将每个参数映射到其相应的XDM字段路径。

>[!NOTE]
>
>此参考适用于使用[Analytics Source Connector](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/analytics)将流媒体数据从Adobe Analytics引入Adobe Experience Platform以用于Customer Journey Analytics报表或其他Platform服务的组织。 这些更改不会影响作为独立应用程序的Adobe Analytics，包括数据收集、处理和报表。

## Media Analytics保留变量

自2025年10月起，Analytics源连接器使用的`media.mediaTimed` XDM字段路径已完全弃用，并替换为`mediaReporting`。 2025年10月之后摄取的数据仅包含`mediaReporting`字段。 旧版字段路径下仍提供早期数据，反映在&#x200B;**旧版XDM字段**&#x200B;下的表中。

### 保持活动呼叫行为

借助适用于流媒体的Analytics Source Connector，来自Adobe Analytics的保持活动调用现在会引入到Adobe Experience Platform中。 这可能会影响Customer Journey Analytics报表：

* **会话计数**：保持活动呼叫有助于保持活动用户会话，即使没有直接媒体交互也是如此。 每个媒体播放的这些调用是在最后一个事件后每20分钟生成一次。 为确保优化会话跟踪，请在数据视图中配置访问过期时间（30分钟）。

* **事件计数**：保持活动状态调用现在计入Customer Journey Analytics Events量度。 要排除这些事件，请创建排除事件类型为`media.keepalive`的事件的过滤器。

## 流媒体参数

| 字段名称 | 旧版XDM字段 | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 流类型]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | 维度 | [[!UICONTROL 流类型]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL 内容ID]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | 维度 | [[!UICONTROL 内容ID]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL 内容长度]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | 维度 | [[!UICONTROL 内容长度]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL 内容类型]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | 维度 | [[!UICONTROL 内容类型]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL 媒体会话ID]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | 维度 | [[!UICONTROL 媒体会话ID]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL 内容播放器名称]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | 维度 | [[!UICONTROL 内容播放器名称]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL 内容渠道]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | 维度 | [[!UICONTROL 内容渠道]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL 内容区段]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | 维度 | [[!UICONTROL 内容区段]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL 内容名称]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | 维度 | [[!UICONTROL 内容名称]](/help/reporting/dimensions/content-name.md) | |
| 视频路径 | *未在AEP/CJA中使用* | | | | Adobe Analytics特定资产 |
| [[!UICONTROL 节目]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | 维度 | [[!UICONTROL 节目]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL 季]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | 维度 | [[!UICONTROL 季]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL 集]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | 维度 | [[!UICONTROL 集]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL 流派]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | 维度 | 不支持 | 使用`mediaReporting`字段 |
| [[!UICONTROL 网络]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | 维度 | [[!UICONTROL 网络]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL 显示类型]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | 维度 | [[!UICONTROL 显示类型]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | 维度 | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL 已授权]](/help/reporting/metrics/authorized.md) | 不受支持 | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | 维度 | [[!UICONTROL 已授权]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL 天部分]](/help/reporting/dimensions/day-part.md) | 不受支持 | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | 维度 | [[!UICONTROL 天部分]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL 媒体馈送类型]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | 维度 | [[!UICONTROL 媒体馈送类型]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL 艺人]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | 维度 | [[!UICONTROL 艺人]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL 相册]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | 维度 | [[!UICONTROL 相册]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL Label]](/help/reporting/dimensions/label.md) | 不受支持 | `xdm.mediaReporting.`<br>`sessionDetails.label` | 维度 | [[!UICONTROL Label]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL 作者]](/help/reporting/dimensions/author.md) | 不受支持 | `xdm.mediaReporting.`<br>`sessionDetails.author` | 维度 | [[!UICONTROL 作者]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL 工作站]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | 维度 | [[!UICONTROL 工作站]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL 发布者]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | 维度 | [[!UICONTROL 发布者]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL 媒体开始]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | 量度 | [[!UICONTROL 媒体开始]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL 内容开始]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | 量度 | [[!UICONTROL 内容开始]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL 内容完成]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | 量度 | [[!UICONTROL 内容完成]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | 量度 | [[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL 媒体逗留时间]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | 量度 | [[!UICONTROL 媒体逗留时间]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL 唯一播放时间]](/help/reporting/metrics/unique-time-played.md) | 不受支持 | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | 量度 | [[!UICONTROL 唯一播放时间]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL 10%进度标记]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | 量度 | [[!UICONTROL 10%进度标记]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 25%进度标记]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | 量度 | [[!UICONTROL 25%进度标记]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 50%进度标记]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | 量度 | [[!UICONTROL 50%进度标记]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 75%进度标记]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | 量度 | [[!UICONTROL 75%进度标记]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 95%进度标记]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | 量度 | [[!UICONTROL 95%进度标记]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL 平均受众访问分钟数]](/help/reporting/metrics/average-minute-audience.md) | 不受支持 | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | 量度 | [[!UICONTROL 平均受众访问分钟数]](/help/reporting/metrics/average-minute-audience.md) | |
| 自上次调用以后经过的秒数 | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | 量度 | 自上次调用以后经过的秒数 | |
| [[!UICONTROL 受暂停影响的流]](/help/reporting/metrics/paused-impacted-streams.md) | 不受支持 | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | 量度 | [[!UICONTROL 受暂停影响的流]](/help/reporting/metrics/paused-impacted-streams.md) | 我们通过从其他事件中计算此值来涵盖mediaTimed |
| [[!UICONTROL 暂停事件]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | 量度 | [[!UICONTROL 暂停事件]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL 总暂停持续时间]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | 量度 | [[!UICONTROL 总暂停持续时间]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL 内容继续]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | 量度 | [[!UICONTROL 内容继续]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL 内容区段视图]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | 量度 | [[!UICONTROL 内容区段视图]](/help/reporting/metrics/content-segment-views.md) | |

## 播放器状态参数更新

| 字段名称 | 旧版XDM字段 | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
| --- | --- | --- | --- | --- | --- |
| 受播放器状态影响的流数量 | 不支持 | `xdm.mediaReporting.`<br>`states.isSet` | 量度 | 不支持 | 使用`mediaReporting`字段 |
| 播放器状态计数 | 不支持 | `xdm.mediaReporting.`<br>`states.count` | 量度 | 不支持 | 使用`mediaReporting`字段 |
| 播放器状态总时长 | 不支持 | `xdm.mediaReporting.`<br>`states.time` | 量度 | 不支持 | 使用`mediaReporting`字段 |
| 播放器状态名称 | 不支持 | `xdm.mediaReporting.`<br>`states.name` | 维度 | 不支持 | 使用`mediaReporting`字段 |

## 章节参数

| 字段名称 | 旧版XDM字段 | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 章节]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | 维度 | [[!UICONTROL 章节]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL 章节开始]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | 量度 | [[!UICONTROL 章节开始]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL 章节结束]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | 量度 | [[!UICONTROL 章节结束]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL 章节逗留时间]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | 量度 | [[!UICONTROL 章节逗留时间]](/help/reporting/metrics/chapter-time-spent.md) | |

## 广告参数

| 字段名称 | 旧版XDM字段 | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 广告ID]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | 维度 | [[!UICONTROL 广告ID]](/help/reporting/dimensions/ad.md) | |
| [[!UICONTROL 面板中的广告位置]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | 维度 | [[!UICONTROL 面板中的广告位置]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL 广告长度]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | 量度 | [[!UICONTROL 广告长度]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL 广告播放器名称]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | 维度 | [[!UICONTROL 广告播放器名称]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL 广告时间ID]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | 维度 | [[!UICONTROL 广告时间ID]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL 广告名称]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | 维度 | [[!UICONTROL 广告名称]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL 广告商]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | 维度 | [[!UICONTROL 广告商]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL 营销活动 ID]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | 维度 | [[!UICONTROL 营销活动 ID]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL 广告开始]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | 量度 | [[!UICONTROL 广告开始]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL 广告结束]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | 量度 | [[!UICONTROL 广告结束]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL 广告逗留时间]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | 量度 | [[!UICONTROL 广告逗留时间]](/help/reporting/metrics/ad-time-spent.md) | |

## 质量参数

| 字段名称 | 旧版XDM字段 | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL 平均比特率]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | 两者 | [[!UICONTROL 平均比特率]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL 开始时间]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | 两者 | [[!UICONTROL 开始时间]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL 丢帧]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | 两者 | [[!UICONTROL 丢帧]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL 缓冲事件]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | 两者 | [[!UICONTROL 缓冲事件]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL 缓冲总持续时间]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | 两者 | [[!UICONTROL 缓冲总持续时间]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL 比特率更改]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | 两者 | [[!UICONTROL 比特率更改]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL 错误/错误事件]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | 两者 | [[!UICONTROL 错误/错误事件]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL 播放器SDK错误ID]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | 维度 | 不支持 | 使用`mediaReporting`字段 |
| [[!UICONTROL 外部错误ID]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | 维度 | 不支持 | 使用`mediaReporting`字段 |
| [[!UICONTROL 开始前丢帧]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | 量度 | [[!UICONTROL 开始前丢帧]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL 受缓冲影响的流]](/help/reporting/metrics/buffer-impacted-streams.md) | 不受支持 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | 量度 | [[!UICONTROL 受缓冲影响的流]](/help/reporting/metrics/buffer-impacted-streams.md) | 通过其他事件计算 |
| [[!UICONTROL 受比特率更改影响的流]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | 不受支持 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | 量度 | [[!UICONTROL 受比特率更改影响的流]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | 通过其他事件计算 |
| [[!UICONTROL 错误影响的流]](/help/reporting/metrics/error-impacted-streams.md) | 不受支持 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | 量度 | [[!UICONTROL 错误影响的流]](/help/reporting/metrics/error-impacted-streams.md) | 通过其他事件计算 |
| [[!UICONTROL 受丢帧影响的流]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | 不受支持 | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | 量度 | [[!UICONTROL 受丢帧影响的流]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | 通过其他事件计算 |

## Media Analytics分类

Media Analytics分类通过名为ACDC的单独流程引入AEP。 下表列出的每个分类组都与AEP中的一个唯一数据集相对应。 在CJA中，需要在Media Analytics事件数据集和每个分类数据集之间建立连接。

### 在Customer Journey Analytics中连接数据集

要在Customer Journey Analytics中设置连接，请执行以下操作：

* 导航到&#x200B;**连接**&#x200B;选项卡，然后选择&#x200B;**新建连接**。
* 在“连接”界面中，选择&#x200B;**添加数据集**，并找到Media Analytics事件数据集（用于通过ADC导入媒体数据）以及四个相关的分类数据集。

### 配置详情

对于每个查找数据集（分类数据集），请如下配置：

* **视频数据集**：
   * 键： `_sandbox.key`
   * 匹配键： `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * 数据源类型： `Web Data`

* **视频数据集**：
   * 键： `_sandbox.key`
   * 匹配键： `Ad ID (advertising.adAssetReference._id)`
   * 数据源类型： `Web Data`

* **videoadpod数据集**：
   * 键： `_sandbox.key`
   * 匹配键： `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * 数据源类型： `Web Data`

* **videochapter数据集**：
   * 键： `_sandbox.key`
   * 匹配键： `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * 数据源类型： `Web Data`

### 报表注意事项

在报告期间使用分类数据集时，请确保引用特定于分类的字段路径(`ACDC XDM Path`)，而不是标准Media Analytics XDM字段。

## 分类表

| 分类名称（组） | 字段名称 | ACDC XDM路径 |
| --- | --- | --- |
| video | 密钥/资产ID | `xdm.<_sandbox>.key` |
| video | 视频长度 | `xdm.<_sandbox>.video_length` |
| video | 视频名称 | `xdm.<_sandbox>.video_name` |
| video | [[!UICONTROL 资产ID]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| video | [[!UICONTROL 首次播放日期]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| video | [[!UICONTROL 首次数字化日期]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| video | [[!UICONTROL 内容评级]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| video | [[!UICONTROL 发起人]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | 密钥/广告ID | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL 广告长度]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL 广告名称]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | 键/广告面板ID | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL 面板位置]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL 面板名称]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | 键/章节 | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL 章节长度]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL 章节偏移]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL 章节位置]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL 章节名称]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Media Analytics自定义变量

在Adobe Analytics中，自定义变量会根据每个报表包中定义的实施规则分配给不同的事件或eVar。 因此，当将这些自定义变量导入Adobe Experience Platform (AEP)时，它们会映射到不同的XDM路径。

* 事件存储在路径下：

  `_experience.analytics.event<x>to<y>.event<number>.value`

* eVar存储在路径下：

  `_experience.analytics.customDimensions.eVars.eVar<number>`

在这两种情况下，`<number>`都对应于原始Adobe Analytics报表包配置中使用的特定事件或eVar编号。

### 自定义变量

| 字段名称 | XDM路径 | 数据类型 |
| --- | --- | --- |
| [[!UICONTROL 媒体下载标志]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| SDK 版本 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| 媒体库版本 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| [[!UICONTROL 流格式]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| [[!UICONTROL 首次播放日期]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| [[!UICONTROL 首次数字化日期]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| [[!UICONTROL 联合数据]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>和<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 两者 |
| [[!UICONTROL 预计的流]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 广告计数]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 章节计数]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| [[!UICONTROL 站点ID]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| [[!UICONTROL Creative URL]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| [[!UICONTROL 版面ID]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | 维度 |
| 每秒帧数 | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>和<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 两者 |
| Media SDK 错误 ID | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 受停滞影响的流]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 停滞事件]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |
| [[!UICONTROL 总停滞持续时间]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | 量度 |

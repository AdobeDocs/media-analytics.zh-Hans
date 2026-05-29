---
title: 媒体报表启用
description: 了解收集媒体量度的媒体报表包。  在发送媒体数据之前，请执行以下步骤来配置媒体报表。
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 20%

---

# 媒体报表启用

收集媒体量度的每个报表包必须在发送媒体数据之前进行配置。

1. 在[Adobe Analytics](https://experience.adobe.com/analytics)中，导航到&#x200B;**[!UICONTROL 管理员]** → **[!UICONTROL 报表包]**。
1. 选择收集媒体数据的报表包。 选择&#x200B;**[!UICONTROL 编辑设置]** → **[!UICONTROL 媒体管理]** → **[!UICONTROL 媒体报告]**。

   ![报表包管理器菜单屏幕截图](assets/media-reporting.png)

1. 在&#x200B;**[!UICONTROL 媒体报表]**&#x200B;页面上，启用所需的流媒体组件（请参阅下文）。

1. 选择&#x200B;**[!UICONTROL 保存].**

   如果此报表包已配置为收集媒体数据，则单击&#x200B;**[!UICONTROL 保存]**&#x200B;后，会显示额外的配置页面。 如果您看到&#x200B;**[!UICONTROL “媒体核心”测量]**&#x200B;页面，请继续执行下一步。

## 可用的流媒体模块

媒体测量包括以下模块：

* **[!UICONTROL 媒体核心]**：所有流媒体跟踪均需要。 它保留用于内容播放和会话数据的解决方案变量。
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
* **[!UICONTROL 媒体广告]**：启用媒体内容中的广告跟踪。
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
* **[!UICONTROL 媒体章节]**：启用媒体内容中章节的跟踪。
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
* **[!UICONTROL 媒体质量]**：启用播放质量数据跟踪，包括缓冲、比特率和错误事件。
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
* **[!UICONTROL 视频元数据]**：启用对标准视频内容属性（如节目、季度和流派）的跟踪。
   * **维度：**
      * [!UICONTROL 个广告加载]
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
* **[!UICONTROL 音频元数据]**：启用对标准音频内容属性的跟踪，例如演出者、专辑和电台。
   * **维度：**
      * [[!UICONTROL 相册]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL 艺人]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL 作者]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Label]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL 发布者]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL 工作站]](/help/reporting/dimensions/station.md)
* **[!UICONTROL 播放器状态跟踪]**：启用标准播放器UI状态的测量，如全屏、隐藏式字幕和画中画。
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

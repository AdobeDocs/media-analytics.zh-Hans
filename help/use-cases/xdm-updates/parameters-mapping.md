---
title: 将受众迁移到新的Adobe Analytics for Streaming Media数据类型
description: 了解如何将受众迁移到新的Adobe Analytics for Streaming Media数据类型
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 3056a384535b3f5f2a9bc2d950bd5ee3410ec0a5
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 44%

---

# Adobe Experience Platform和Customer Journey Analytics的Media Analytics参数映射

本文档全面列出了Adobe Experience Platform和Customer Journey Analytics中使用的所有Media Analytics参数。 它旨在支持将通过[Analytics Source Connector](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/analytics)或[Analytics Source Connector for Classifications](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/classifications)从Adobe Analytics导入的数据集成到Platform，并将每个参数映射到其相应的XDM字段路径。

## Media Analytics保留变量

对于所有Media Analytics保留变量，可以在“当前XDM字段路径”下找到2025年5月之前从Adobe Analytics摄取到AEP（并包括）的数据，如下表所示。

由于Media Analytics和ADC团队目前正致力于完全迁移到“报告XDM字段路径”，在此迁移完成并且“报告XDM字段路径”可供使用后，将共享正式通信。

## 流媒体参数

| 字段名称 | 当前XDM字段路径（已弃用） | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| 流类型 | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | 维度 | 流类型 |                                                                       |
| 内容 ID | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | 维度 | 内容 ID |                                                                       |
| 内容时长 | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | 维度 | 内容时长 |                                                                       |
| 内容类型 | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | 维度 | 内容类型 |                                                                       |
| 媒体会话 ID | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | 维度 | 媒体会话 ID |                                                                       |
| 内容播放器名称 | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | 维度 | 内容播放器名称 |                                                                       |
| 内容渠道 | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | 维度 | 内容渠道 |                                                                       |
| 内容区段 | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | 维度 | 内容区段 |                                                                       |
| 内容名称 | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | 维度 | 内容名称 |                                                                       |
| 视频路径 | *未在AEP/CJA中使用* |                                                   |           |                   | Adobe Analytics特定资产 |
| 节目 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | 维度 | 节目 |                                                                       |
| 季 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | 维度 | 季 |                                                                       |
| 剧集 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | 维度 | 剧集 |                                                                       |
| 流派 | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | 维度 | 不支持 | 使用mediaReporting字段 |
| 网络 | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | 维度 | 网络 |                                                                       |
| 节目类型 | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | 维度 | 节目类型 |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | 维度 | MVPD |                                                                       |
| 已授权 | 不支持 | mediaReporting.sessionDetails.authorized | 维度 | 已授权 |                                                                       |
| 播出时段 | 不支持 | mediaReporting.sessionDetails.dayPart | 维度 | 播出时段 |                                                                       |
| 媒体馈送类型 | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | 维度 | 媒体馈送类型 |                                                                       |
| 艺人 | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | 维度 | 艺人 |                                                                       |
| 专辑 | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | 维度 | 专辑 |                                                                       |
| 标签 | 不支持 | mediaReporting.sessionDetails.label | 维度 | 标签 |                                                                       |
| 作者 | 不支持 | mediaReporting.sessionDetails.author | 维度 | 作者 |                                                                       |
| 电台/电视台 | media.mediaTimed.primaryAssetReference._id3.音频。_id3.TRSN | mediaReporting.sessionDetails.station | 维度 | 电台/电视台 |                                                                       |
| 发布者 | media.mediaTimed.primaryAssetReference._id3.音频。_id3.TPUB | mediaReporting.sessionDetails.publisher | 维度 | 发布者 |                                                                       |
| 媒体开始 | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | 量度 | 媒体开始 |                                                                       |
| 内容开始 | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | 量度 | 内容开始 |                                                                       |
| 内容结束 | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | 量度 | 内容结束 |                                                                       |
| 内容逗留时间 | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | 量度 | 内容逗留时间 |                                                                       |
| 平均逗留时间 | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | 量度 | 平均逗留时间 |                                                                       |
| 不重复播放时间 | 不支持 | mediaReporting.sessionDetails.uniqueTimePlayed | 量度 | 不重复播放时间 |                                                                       |
| 10% 进度标记 | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | 量度 | 10% 进度标记 |                                                                       |
| 25% 进度标记 | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | 量度 | 25% 进度标记 |                                                                       |
| 50% 进度标记 | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | 量度 | 50% 进度标记 |                                                                       |
| 75% 进度标记 | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | 量度 | 75% 进度标记 |                                                                       |
| 95% 进度标记 | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | 量度 | 95% 进度标记 |                                                                       |
| 平均受众访问分钟数 | 不支持 | mediaReporting.sessionDetails.averageMinuteAudience | 量度 | 平均受众访问分钟数 |                                                                  |
| 自上次调用以后经过的秒数 | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | 量度 | 自上次调用以后经过的秒数 |                                                              |
| 受暂停影响的流 | 不支持 | mediaReporting.sessionDetails.hasPauseImpactedStreams | 量度 | 受暂停影响的流 | 我们通过从其他事件中计算此值来涵盖mediaTimed |
| 暂停事件 | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | 量度 | 暂停事件 |                                                                       |
| 暂停总持续时间 | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | 量度 | 暂停总持续时间 |                                                                       |
| 内容继续 | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | 量度 | 内容继续 |                                                                       |
| 内容区段查看 | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | 量度 | 内容区段查看 |                                                                     |

{style="table-layout:auto"}

## 播放器状态参数更新

| 字段名称 | 当前XDM字段路径（已弃用） | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| 受播放器状态影响的流数量 | 不支持 | mediaReporting.states.isSet | 量度 | 不支持 | 使用mediaReporting字段 |
| 播放器状态计数 | 不支持 | mediaReporting.states.count | 量度 | 不支持 | 使用mediaReporting字段 |
| 播放器状态总时长 | 不支持 | mediaReporting.states.time | 量度 | 不支持 | 使用mediaReporting字段 |
| 播放器状态名称 | 不支持 | mediaReporting.states.name | 维度 | 不支持 | 使用mediaReporting字段 |

{style="table-layout:auto"}

## 章节参数

| 字段名称 | 当前XDM字段路径（已弃用） | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| 章节 | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | 维度 | 章节 |           |
| 章节开始 | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | 量度 | 章节开始 |           |
| 章节结束 | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | 量度 | 章节结束 |          |
| 章节逗留时间 | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | 量度 | 章节逗留时间 |        |

{style="table-layout:auto"}

## 广告参数

| 字段名称 | 当前XDM字段路径（已弃用） | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 广告 ID | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | 维度 | 广告 ID |           |
| 面板中的广告位置 | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | 维度 | 面板中的广告位置 |     |
| 广告长度 | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | 量度 | 广告长度 |           |
| 广告播放器名称 | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | 维度 | 广告播放器名称 |           |
| 广告时间 ID | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | 维度 | 广告时间 ID |           |
| 广告名称 | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | 维度 | 广告名称 |           |
| 广告商 | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | 维度 | 广告商 |           |
| 促销活动 ID | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | 维度 | 营销活动 ID |           |
| 广告开始 | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | 量度 | 广告开始 |           |
| 广告结束 | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | 量度 | 广告结束 |           |
| 平均逗留时间 | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | 量度 | 平均逗留时间 |           |

{style="table-layout:auto"}

## 质量参数

| 字段名称 | 当前XDM字段路径（已弃用） | 报告XDM字段路径 | 数据类型 | 派生字段 | 注释 |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| 平均比特率 | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Both | 平均比特率 |           |
| 开始时间 | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Both | 开始时间 |           |
| 丢帧 | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Both | 丢帧 |           |
| 缓冲事件 | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Both | 缓冲事件 |           |
| 缓冲总持续时间 | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Both | 缓冲总持续时间 |     |
| 比特率更改 | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Both | 比特率更改 |         |
| 错误/错误事件 | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Both | 错误/错误事件 |  |
| 播放器 SDK 错误 ID | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | 维度 | 不支持 | 使用mediaReporting字段 |
| 外部错误 ID | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | 维度 | 不支持 | 使用mediaReporting字段 |
| 开始前丢帧 | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | 量度 | 开始前丢帧 |     |
| 受缓冲影响的流 | 不支持 | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | 量度 | 受缓冲影响的流 | 通过其他事件计算 |
| 受比特率更改影响的流 | 不支持 | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | 量度 | 受比特率更改影响的流 | 通过其他事件计算 |
| 受错误影响的流 | 不支持 | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | 量度 | 受错误影响的流 | 通过其他事件计算 |
| 受丢帧影响的流 | 不支持 | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | 量度 | 受丢帧影响的流 | 通过其他事件计算 |

{style="table-layout:auto"}

## Media Analytics分类

Media Analytics分类通过名为ACDC的单独流程引入AEP。 下表列出的每个分类组都与AEP中的一个唯一数据集相对应。 在CJA中，需要在Media Analytics事件数据集和每个分类数据集之间建立连接。

### 在Customer Journey Analytics中连接数据集

要在Customer Journey Analytics中设置连接，请执行以下操作：

- 导航到&#x200B;**连接**&#x200B;选项卡，然后选择&#x200B;**新建连接**。
- 在“连接”界面中，选择&#x200B;**添加数据集**，并找到Media Analytics事件数据集（用于通过ADC导入媒体数据）以及四个相关的分类数据集。

### 配置详细信息

对于每个查找数据集（分类数据集），请如下配置：

- **视频数据集**：
   - 键： `_sandbox.key`
   - 匹配键： `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - 数据源类型： `Web Data`

- **视频数据集**：
   - 键： `_sandbox.key`
   - 匹配键： `Ad ID (advertising.adAssetReference._id)`
   - 数据源类型： `Web Data`

- **videoadpod数据集**：
   - 键： `_sandbox.key`
   - 匹配键： `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - 数据源类型： `Web Data`

- **videochapter数据集**：
   - 键： `_sandbox.key`
   - 匹配键： `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - 数据源类型： `Web Data`

### 报表注意事项

在报告期间使用分类数据集时，请确保引用特定于分类的字段路径(`ACDC XDM Path`)，而不是标准Media Analytics XDM字段。

## 分类表

| 分类名称（组） | 字段名称 | ACDC XDM路径 |
|------------|----------|-------------|
| video | 密钥/资产ID | `<_sandbox>.key` |
| video | 视频长度 | `<_sandbox>.video_length` |
| video | 视频名称 | `<_sandbox>.video_name` |
| video | 资产 ID | `<_sandbox>.asset_id` |
| video | 首次播放日期 | `<_sandbox>.first_air_date` |
| video | 首次数字化日期 | `<_sandbox>.first_digital_date` |
| video | 内容评级 | `<_sandbox>.content_rating` |
| video | 创作者 | `<_sandbox>.originator` |
| videoad | 密钥/广告ID | `<_sandbox>.key` |
| videoad | 广告长度 | `<_sandbox>.ad_length` |
| videoad | 广告名称 | `<_sandbox>.ad_name` |
| videoad | 创作 ID | `<_sandbox>.creative_id` |
| videoadpod | 键/广告面板ID | `<_sandbox>.key` |
| videoadpod | 面板位置 | `<_sandbox>.pod_position` |
| videoadpod | 面板名称 | `<_sandbox>.pod_name` |
| videochapter | 键/章节 | `<_sandbox>.key` |
| videochapter | 章节长度 | `<_sandbox>.chapter_length` |
| videochapter | 章节偏移 | `<_sandbox>.chapter_offset` |
| videochapter | 章节位置 | `<_sandbox>.chapter_position` |
| videochapter | 章节名称 | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Media Analytics自定义变量

在Adobe Analytics中，自定义变量会根据每个报表包中定义的实施规则分配给不同的事件或eVar。 因此，当将这些自定义变量导入Adobe Experience Platform (AEP)时，它们会映射到不同的XDM路径。

- 事件存储在路径下：

  `_experience.analytics.event<x>to<y>.event<number>.value`

- eVar存储在路径下：

  `_experience.analytics.customDimensions.eVars.eVar<number>`

在这两种情况下，`<number>`都对应于原始Adobe Analytics报表包配置中使用的特定事件或eVar编号。

### 自定义变量

| 字段名称 | XDM路径 | 数据类型 |
|-------------|-------------|-----------|
| 媒体下载标志 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| SDK 版本 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| VHL 版本 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 流格式 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 首次播放日期 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 首次数字化日期 | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 联合数据 | `_experience.analytics.customDimensions.eVars.eVar<number>` 和 `_experience.analytics.event<x>to<y>.event<number>.value` | Both |
| 预计的流 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 广告计数 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 章节计数 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 创作 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 网站 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 创作 URL | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 版面 ID | `_experience.analytics.customDimensions.eVars.eVar<number>` | 维度 |
| 每秒帧数 | `_experience.analytics.customDimensions.eVars.eVar<number>` 和 `_experience.analytics.event<x>to<y>.event<number>.value` | Both |
| Media SDK 错误 ID | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 受停滞影响的流 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 停滞事件 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |
| 停滞总持续时间 | `_experience.analytics.event<x>to<y>.event<number>.value` | 量度 |

{style="table-layout:auto"}







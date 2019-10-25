---
seo-title: Roku 元数据键
title: Roku 元数据键
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Roku 元数据键{#roku-metadata-keys}

可分别在媒体和广告信息对象上设置标准视频、音频和广告元数据。 调用跟踪 API 之前，使用视频/广告元数据的常量键设置包含信息对象中标准元数据的字典。有关标准元数据常量的完整列表，请参阅下表，随后是对应的示例。

## 视频元数据常量 {#video-metadata-constants}

| 元数据名称 | 上下文数据键 | 常量名称 |
| --- | --- | --- |
| 节目 | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| 季 | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| 剧集 | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| 资产 | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| 流派 | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| 首次播放日期 | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| 首次数字化播放日期 | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| 评级 | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| 创作者 | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| 网络 | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| 节目类型 | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| 广告载入 | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| 已授权 | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| 播出时段 | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| 信息源 | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| 流格式 | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## 音频元数据常量 {#audio-metadata-constants}

| 元数据名称 | 上下文数据键 | 常量名称 |
| --- | --- | --- |
| 艺人 | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| 专辑 | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| 标签 | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| 作者 | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| 电台/电视台 | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| 发布者 | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## 广告元数据常量 {#ad-metadata-constants}

| 元数据名称 | 上下文数据键 | 常量名称 |
| --- | --- | --- |
| 广告商 | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| 促销活动 ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| 创作 ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| 版面 ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| 网站 ID | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| 创作 URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## 常量 {#constants}

您可以使用以下常量来跟踪媒体事件：

### 其他常量

| 常量 | 描述   |
|---|---|
| `ERROR_SOURCE_PLAYER` | 用于错误源为播放器的常量 |

### MediaObjectkey 常量（在 MediaObject 实例中用作键）

| 常量 | 描述   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | 常数，用于在 `MediaInfo``trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | 常数，用于在 `EventData``trackEvent` |
| `MEDIA_RESUMED` | 用于发送视频恢复心率的常量。To resume video tracking of previously stopped content, you need to set the `MEDIA_RESUMED` property on the `mediaInfo` object when you call `mediaTrackLoad`. (`MEDIA_RESUMED` is not an event that you can track using the `mediaTrackEvent` API.) 当应用程序想要继续跟踪用户之前停止观看但现在打算继续观看的内容时，应将 `MEDIA_RESUMED` 设置为 true。<br/><br/>例如，假设一位用户只观看了 30% 的内容，然后关闭了应用程序。此操作将导致会话结束。Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they left off, then the application should set `MEDIA_RESUMED` to "true" while calling the `mediaTrackLoad` API. 其结果是，同一视频内容的这两个不同媒体会话可以链接在一起。以下是实施示例： <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)`<br/><br/>这将为视频创建一个新会话，但它也会导致 SDK 发送事件类型为“resume”的心率请求，该事件类型可用于进行报告，以将两个不同的媒体会话关联在一起。 |

### 内容类型常量

| 常量 | 描述   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | 表示流类型“实时”的常量 |
| `MEDIA_STREAM_TYPE_VOD` | 表示流类型“VOD”的常量 |

### 事件类型常量（用于 trackEvent 调用）

| 常量 | 描述   |
|---|---|
| `MEDIA_BUFFER_START` | 表示缓冲开始的事件类型 |
| `MEDIA_BUFFER_COMPLETE` | 表示缓冲结束的事件类型 |
| `MEDIA_SEEK_START` | 表示搜寻开始的事件类型 |
| `MEDIA_SEEK_COMPLETE` | 表示搜寻结束的事件类型 |
| `MEDIA_BITRATE_CHANGE` | 表示比特率更改的事件类型 |
| `MEDIA_CHAPTER_START` | 表示章节开始的事件类型 |
| `MEDIA_CHAPTER_COMPLETE` | 表示章节结束的事件类型 |
| `MEDIA_CHAPTER_SKIP` | 表示广告开始的事件类型 |
| `MEDIA_AD_BREAK_START` | 表示广告开始的事件类型 |
| `MEDIA_AD_BREAK_COMPLETE` | 表示 AdBreak 结束的事件类型 |
| `MEDIA_AD_BREAK_SKIP` | 表示 AdBreak 跳过的事件类型 |
| `MEDIA_AD_START` | 表示广告开始的事件类型 |
| `MEDIA_AD_COMPLETE` | 表示广告结束的事件类型 |
| `MEDIA_AD_SKIP` | 表示广告跳过的事件类型 |


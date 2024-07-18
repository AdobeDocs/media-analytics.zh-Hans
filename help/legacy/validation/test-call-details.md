---
title: 测试调用详细信息
description: 探究验证实施时必须发出的各种调用。
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 100%

---

# 测试调用详细信息{#test-call-details}

## 启动媒体播放器 {#start-the-media-player}

### Adobe Analytics (AppMeasurement) 开始调用 {#aa-start-call}

| 参数 | 值（示例） |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | 剧集标题 |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**自定义元数据字段**_ |
| _**`a.media.[value]`**_ | _**标准元数据字段**_ |

**注释：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 线性流的长度应设置为当前节目的最佳预计长度。

### Adobe Analytics (AppMeasurement) 开始调用中的标准元数据 {#std-metadata-aa}

| 参数 | 值（示例） |
|---|---|
| `a.media.show` | 节目标题 |
| `a.media.season` | 6 |
| `a.media.episode` | 剧集标题 |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics (AppMeasurement) 开始调用中的自定义元数据 {#custom-metadata-aa}

| 参数 | 值（示例） |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics（心跳）开始调用 {#ma-start-call}

| 参数 | 值（示例） |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | 剧集标题 |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**自定义元数据字段**_ |
| _**`s:meta:a.media.[value]`**_ | _**标准元数据字段**_ |

**注释：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 应将视频开始时线性流的播放头位置设置为自当前节目开始后所经过的秒数，而不是设置为 0。

### Media Analytics（心跳）开始调用中的标准元数据 {#std-metadata-ma}

| 参数 | 值（示例） |
|---|---|
| `s:meta:a.media.show` | 节目 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | 剧集标题 |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics（心跳）开始调用中的自定义元数据 {#custom-metadata-ma}

| 参数 | 值（示例） |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics（心跳）Adobe Analytics 开始调用 {#ma-aa-start}

| 参数 | 值（示例） |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | 剧集标题 |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**注释：**

* 此调用表示 Media SDK 已请求将 Adobe Analytics `pev2=ms_s` 调用发送到 Adobe Analytics (AppMeasurement) 服务器。
* 此调用不包含自定义元数据。

## 观看广告播放 {#view-ad-playback}

### Adobe Analytics (AppMeasurement) 广告开始调用 {#aa-ad-start-call}

| 参数 | 值（示例） |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**元数据字段**_ |
| _**`a.media.[value]`**_ | _**标准元数据字段**_ |

**注释：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 广告开始时，如果未提供广告长度，广告长度可能会被设置为 -1。

### Adobe Analytics (AppMeasurement) 广告开始调用中的标准元数据 {#std-metadata-aa-ad-start}

| 参数 | 值（示例） |
|---|---|
| `a.media.show` | 节目标题 |
| `a.media.season` | 6 |
| `a.media.episode` | 剧集标题 |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics (AppMeasurement) 广告开始调用中的自定义元数据 {#custom-metadata-aa-ad-start}

| 参数 | 值（示例） |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics（心跳）广告开始调用 {#ma-ad-start-call}

| 参数 | 值（示例） |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**广告**_ |
| _**`s:meta:custom.[value]`**_ | _**自定义元数据字段**_ |
| _**`s:meta:a.media.[value]`**_ | _**标准元数据字段**_ |

**注释：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 广告开始时，如果未提供广告长度，广告长度可能会被设置为 -1。

### Media Analytics（心跳）广告开始调用中的标准元数据 {#std-metadata-ma-ad-start}

| 参数 | 值（示例） |
|---|---|
| `s:meta:a.media.show` | 节目 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | 剧集标题 |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics（心跳）广告开始调用中的自定义元数据 {#custom-metadata-ma-ad-start}

| 参数 | 值（示例） |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics（心跳）Adobe Analytics 广告开始调用 {#ma-aa-ad-start-call}

| 参数 | 值（示例） |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | 广告 |

### Media Analytics（心跳）广告播放调用 {#ma-ad-play-call}

| 参数 | 值（示例） |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**广告**_ |

### Media Analytics（心跳）广告暂停调用 {#ma-ad-pause-call}

| 参数 | 值（示例） |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**广告**_ |

### Media Analytics（心跳）Adobe Analytics 广告结束调用 {#ma-aa-ad-complete-call}

| 参数 | 值（示例） |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**广告**_ |

## 播放主内容 {#play-main-content}

### Media Analytics（心跳）播放调用 {#ma-play-call}

| 参数 | 值（示例） |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | 剧集标题 |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**注释：**

* 每发起一次播放调用，播放头位置应增加 10 秒。
* `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

## 暂停主内容 {#pause-main-content}

### Media Analytics（心跳）暂停调用 {#ma-pause-call}

| 参数 | 值（示例） |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | 剧集标题 |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

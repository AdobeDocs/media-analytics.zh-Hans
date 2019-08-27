---
seo-title: 测试调用详细信息
title: 测试调用详细信息
uuid: d3a0e62f-2fc3-413d-ac56-adbhone9 b3 e983
translation-type: tm+mt
source-git-commit: d694ced982140c1f8020c0be304492aee0495cdc

---


# 测试调用详细信息{#test-call-details}

## 启动媒体播放器 {#start-the-media-player}

### Adobe Analytics(AppMeasurement)开始电话 {#aa-start-call}

| 参数 | 值(示例) |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | VOD |
| _**`custom.[value]`**_ | _**自定义元数据字段**_ |
| _**`a.media.[value]`**_ | _**标准元数据字段**_ |

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 线性流的长度应设置为当前节目的最佳预计长度。

### Adobe Analytics(AppMeasurement)开始电话的标准元数据 {#std-metadata-aa}

| 参数 | 值(示例) |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
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

### Adobe Analytics(AppMeasurement)开始电话的自定义元数据 {#custom-metadata-aa}

| 参数 | 值(示例) |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### 媒体分析(心跳)开始电话 {#ma-start-call}

| 参数 | 值(示例) |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**自定义元数据字段**_ |
| _**`s:meta:a.media.[value]`**_ | _**标准元数据字段**_ |

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 应将视频开始时线性流的播放头位置设置为自当前节目开始后所经过的秒数，而不是设置为 0。

### Media Analytics中的标准元数据(心跳)开始电话呼叫 {#std-metadata-ma}

| 参数 | 值(示例) |
|---|---|
| `s:meta:a.media.show` | 节目 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
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

### 媒体分析(心跳)中的自定义元数据开始电话联系 {#custom-metadata-ma}

| 参数 | 值(示例) |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics(Heartbeats) Adobe Analytics开始电话 {#ma-aa-start}

| 参数 | 值(示例) |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**注意：**

* 此调用指示媒体SDK已请求将Adobe Analytics `pev2=ms_s` 调用发送到Adobe Analytics(AppMeasurement)服务器。
* 此调用不包含自定义元数据。

## 观看广告播放 {#view-ad-playback}

### Adobe Analytics(AppMeasurement)广告开始电话 {#aa-ad-start-call}

| 参数 | 值(示例) |
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

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 广告开始时，如果未提供广告长度，广告长度可能会被设置为 -1。

### Standard metadata in Adobe Analytics (AppMeasurement) Ad Start call {#std-metadata-aa-ad-start}

| 参数 | 值(示例) |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
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

### Adobe Analytics(AppMeasurement)广告开始电话中的自定义元数据 {#custom-metadata-aa-ad-start}

| 参数 | 值(示例) |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics(Heartbeats)广告开始电话 {#ma-ad-start-call}

| 参数 | 值(示例) |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**自定义元数据字段**_ |
| _**`s:meta:a.media.[value]`**_ | _**标准元数据字段**_ |

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 广告开始时，如果未提供广告长度，广告长度可能会被设置为 -1。

### Standard metadata in Media Analytics (heartbeats) Ad Start call {#std-metadata-ma-ad-start}

| 参数 | 值(示例) |
|---|---|
| `s:meta:a.media.show` | 节目 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
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

### 媒体分析(心跳)广告开始电话中的自定义元数据 {#custom-metadata-ma-ad-start}

| 参数 | 值(示例) |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### 媒体分析(心跳) Adobe Analytics广告开始电话 {#ma-aa-ad-start-call}

| 参数 | 值(示例) |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |

### 媒体分析(心跳)广告播放电话 {#ma-ad-play-call}

| 参数 | 值(示例) |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics(Heartbeats)广告暂停电话 {#ma-ad-pause-call}

| 参数 | 值(示例) |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics(Heartbeats) Adobe Analytics Ad Complete电话 {#ma-aa-ad-complete-call}

| 参数 | 值(示例) |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| _**`s:asset:type`**_ | _**ad**_ |

## 播放主内容 {#play-main-content}

### 媒体分析(心跳)播放电话 {#ma-play-call}

| 参数 | 值(示例) |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**注意：**

* 播放头的位置应在每次播放时增加10秒。
* `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

## 暂停主要内容 {#pause-main-content}

### Media Analytics(Heartbeats)暂停电话联系 {#ma-pause-call}

| 参数 | 值(示例) |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |



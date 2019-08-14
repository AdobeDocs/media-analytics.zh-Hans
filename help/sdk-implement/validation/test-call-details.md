---
seo-title: 测试调用详细信息
title: 测试调用详细信息
uuid: d3a0e62f-2fc3-413d-ac56-adbhone9 b3 e983
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# 测试调用详细信息{#test-call-details}

## 启动视频播放器 {#section_qts_xff_f2b}

### 媒体分析开始电话

| 参数 | 值（示例）   |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | true |
| `a.contentType` | VOD |
| `custom.[value]` | 自定义元数据字段 |
| `a.media.[value]` | 标准元数据字段 |

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 线性流的长度应设置为当前节目的最佳预计长度。

### 媒体分析启动电话中的标准元数据

| 参数 | 值（示例）   |
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

### 心率开始调用

| 参数 | 值（示例）   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | 自定义元数据字段 |
| `s:meta:a.media.[value]` | 标准元数据字段 |

### 媒体分析启动电话中的媒体元数据

| 参数 | 值（示例）   |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 应将视频开始时线性流的播放头位置设置为自当前节目开始后所经过的秒数，而不是设置为 0。

### 心率分析开始调用

| 参数 | 值（示例）   |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

### 心跳开始呼叫中的媒体元数据

| 参数 | 值（示例）   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### 心率开始调用中的标准元数据

| 参数 | 值（示例）   |
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

**注意：**

* 此调用指示心率库已请求将 pev2=ms_s 分析调用发送至分析服务器。
* 此调用不包含自定义元数据。

## 观看广告播放 {#section_wz3_yff_f2b}

### Media Analytics广告开始电话

| 参数 | 值（示例）   |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| `a.media.ad.view` | true |
| `custom.[value]` | 元数据字段 |
| `a.media.[value]` | 标准元数据字段 |

**注意：**&#x200B;其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。

### 心率广告开始调用

| 参数 | 值（示例）   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | 自定义元数据字段 |
| `s:meta:a.media.[value]` | 标准元数据字段 |

### Media Analytics广告开始电话中的媒体元数据

| 参数 | 值（示例）   |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics广告开始电话中的标准元数据

| 参数 | 值（示例）   |
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

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 广告开始时，如果未提供广告长度，广告长度可能会被设置为 -1。

### 心率分析广告开始调用

| 参数 | 值（示例）   |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |

### 心跳广告开始电话中的媒体元数据

| 参数 | 值（示例）   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### 心率广告开始调用中的标准元数据

| 参数 | 值（示例）   |
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

**注意：**

* 其他上下文数据变量应该存在并包含元数据。请参阅下面的元数据详细信息。
* 广告开始时，如果未提供广告长度，广告长度可能会被设置为 -1。

### 心率广告结束调用

| 参数 | 值（示例）   |
|---|---|
| `s:event:type` | complete |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |

### 心率广告播放调用

| 参数 | 值（示例）   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | VOD |
| `s:asset:type` | ad |

## 播放主内容 {#section_u1l_1gf_f2b}

### 心率播放调用

| 参数 | 值（示例）   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | VOD |
| `s:asset:type` | main |

**注意：**

* 每发起一次播放调用，播放头位置应增加 10。
* `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。


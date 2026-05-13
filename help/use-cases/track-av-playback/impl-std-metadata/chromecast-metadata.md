---
title: 解释 Chromecast 元数据键
description: 了解如何在 Chromecast 中设置要与跟踪调用一起发送的标准视频和广告元数据。
uuid: c446ad41-51b8-46d6-9bc1-abfae866023f
exl-id: ccc717ae-d846-4349-8282-5e3511ddeb9b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/JfJR10sGyYW22zZX2RNSJRNL2R7wQXjQMB-PZNxxIPo
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 139
ht-degree: 55%

---

# Chromecast 元数据键{#chromecast-metadata-keys}

标准视频和广告元数据可以分别在媒体和广告信息对象中进行设置。 使用视频/广告元数据的常量键，在调用跟踪API之前设置包含信息对象上标准元数据的字典。 有关标准元数据常量的完整列表，请参阅下表，之后提供示例。

## 元数据常量 {#video-metadata-constants}

| 元数据名称 | 上下文数据键 | 常量名称 |
| --- | --- | --- |
| 节目 | `a.media.show` | `ADBMobile.media.VideoMetadataKeys.SHOW` |
| 季 | `a.media.season` | `ADBMobile.media.VideoMetadataKeys.SEASON` |
| 剧集 | `a.media.episode` | `ADBMobile.media.VideoMetadataKeys.EPISODE` |
| 资产 | `a.media.asset` | `ADBMobile.media.VideoMetadataKeys.TMS_ID` |
| 流派 | `a.media.genre` | `ADBMobile.media.VideoMetadataKeys.GENRE` |
| 首次播放日期 | `a.media.airDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` |
| 首次数字化播放日期 | `a.media.digitalDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE` |
| 评级 | `a.media.rating` | `ADBMobile.media.VideoMetadataKeys.RATING` |
| 创作者 | `a.media.originator` | `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` |
| 网络 | `a.media.network` | `ADBMobile.media.VideoMetadataKeys.NETWORK` |
| 节目类型 | `a.media.type` | `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` |
| 广告载入 | `a.media.adLoad` | `ADBMobile.media.VideoMetadataKeys.AD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `ADBMobile.media.VideoMetadataKeys.MVPD` |
| 已授权 | `a.media.pass.auth` | `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` |
| 播出时段 | `a.media.dayPart` | `ADBMobile.media.VideoMetadataKeys.DAY_PART` |
| 信息源 | `a.media.feed` | `ADBMobile.media.VideoMetadataKeys.FEED` |
| 流格式 | `a.media.format` | `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` |

## 广告元数据常量 {#ad-metadata-constants}

| 元数据名称 | 上下文数据键 | 常量名称 |
| --- | --- | --- |
| 广告商 | `a.media.ad.advertiser` | `ADBMobile.media.AdMetadataKeys.ADVERTISER` |
| 营销活动 ID | `a.media.ad.campaign` | `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` |
| 创作 ID | `a.media.ad.creative` | `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` |
| 版面 ID | `a.media.ad.placement` | `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` |
| 网站 ID | `a.media.ad.site` | `ADBMobile.media.AdMetadataKeys.SITE_ID` |
| 创作 URL | `a.media.ad.creativeURL` | `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` |

## Chromecast 实施示例 {#sample-implementations-for-chromecast}

### 视频

```js
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["videotype"] = "episode"; 
 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### 音频

```js
// setting Standard Audio Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["audiotype"] = "podcast"; 
var standardAudioMetadata = {}; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = "sample artist"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "sample album" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "sample label"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "sample author" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "sample station " ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "sample publisher"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType, content.mediaType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudiooMetadata] = standardAudiooMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### 广告

```js
// setting Standard Ad Metadata as context data on ad start event 
var standardAdMetadata = {}; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "sample campaign"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
 
var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
 
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
```

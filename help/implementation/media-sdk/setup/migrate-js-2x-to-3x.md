---
title: 从JavaScript SDK 2.x迁移到3.x
description: 有关从Media SDK JavaScript 2.x升级到3.x SDK的代码比较和迁移指南。
feature: Streaming Media
role: User, Admin, Developer
exl-id: b7e2d5a1-8c3f-4a9d-b6e7-2c1b4f0d8a3e
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 12%

---


# 从2.x JS SDK迁移到3.x JS SDK

## 新增功能

* 使用MediaCollection API
* 自定义状态跟踪

## 改进

* 为媒体库提供全局配置
* 创建简单的跟踪器
* 添加了API以提供播放头和QoE信息
* 用于销毁跟踪器实例的API
* 简化媒体和广告的标准/自定义元数据的设置

## API比较

### 媒体类

| 功能 | 2.x | 3.x |
| ------ | ------ | ------ |
| **命名空间** | `ADB.va.MediaHeartbeat` | **`ADB.Media`** |
| **配置** | `MediaHeartbeat`构造函数的参数 | **`configure(mediaConfig, appMeasurement)`** |
| **创建跟踪器** | `new MediaHeartbeat(...)` | **`getInstance()`** |
| **静态方法** | |  |
|  | `createMediaObject(...)` | `createMediaObject(...)` |
|  | `createAdBreakObject(...)` | `createAdBreakObject(...)` |
|  | `createAdObject(...)` | `createAdObject(...)` |
|  | `createChapterObject(...)` | `createChapterObject(...)` |
|  | `createQoSObject(...)` | **`createQoEObject(...)`** |
|  | 不适用 | **`createStateObject()`** |
| **实例方法** | |  |
|  | `trackSessionStart(...)` | `trackSessionStart(...)` |
|  | `trackPlay()` | `trackPlay()` |
|  | `trackPause()` | `trackPause()` |
|  | `trackComplete()` | `trackComplete()` |
|  | `trackSessionEnd()` | `trackSessionEnd()` |
|  | `trackEvent(...)` | `trackEvent(...)` |
|  | `trackError(...)` | `trackError(...)` |
|  | 不适用 | **`updatePlayhead(playhead)`** |
|  | 不适用 | **`updateQoEObject(qoeObject)`** |
| **销毁跟踪器** | 不适用 | **`destroy()`** |

### MediaConfig类

| 功能 | 2.x | 3.x |
| ------ | ------ | ------ |
| **命名空间** | ` ADB.va.MediaHeartbeatConfig` | **`ADB.MediaConfig`** |
| **构造函数** | `new MediaHeartbeatConfig()` | **`new MediaConfig()`** |
| **配置参数** | | |
| | `trackingServer` | `trackingServer` |
| | `channel` | `channel` |
| | `ovp` | 不适用 |
| | `appVersion` | `appVersion` |
| | `playerName` | `playerName` |
| | `ssl` | `ssl` |
| | `debugLogging` | `debugLogging` |

## 代码比较

### 配置和跟踪器创建

#### 2.x

```javascript
    var MediaHeartbeat = ADB.va.MediaHeartbeat;
    var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
    var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;

    // Create MediaHeartbeatConfig object
    var mediaConfig = new MediaHeartbeatConfig();
    mediaConfig.trackingServer = "tracking_server";
    mediaConfig.playerName = "player_name";
    mediaConfig.channel = "sample_channel";
    mediaConfig.ovp = "sample_ovp";
    mediaConfig.appVersion = "app_version";
    mediaConfig.debugLogging = true;
    mediaConfig.ssl = true;

    // Instance of MediaHeartbeatDelegate to return playhead and qosInfo to the tracker
    ADB.core.extend(SampleMediaHeartbeatDelegate.prototype,
                         MediaHeartbeatDelegate.prototype);
    function SampleMediaHeartbeatDelegate() { ... }
    SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
        // Returns the current playhead from the player.
    }
    SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
        // Returns the current QOS information if available from the player.
    }

    // Create tracker instance by passing mediaConfig, appMeasurement instancee and player delegate
    var tracker = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(),
                                      mediaConfig,
                                      appMeasurement);
```

#### 3.x

```javascript
    var Media = ADB.Media;
    var MediaConfig = ADB.MediaConfig;

    // Create MediaConfig object (same as above)
    var mediaConfig = new MediaConfig();
    mediaConfig.trackingServer = "tracking_server";
    mediaConfig.playerName = "player_name";
    mediaConfig.channel = "sample_channel";
    mediaConfig.appVersion = "app_version";
    mediaConfig.debugLogging = true;
    mediaConfig.ssl = true;

    // Configuration is only done once per page
    // and applies to all tracker instances created.
    Media.configure(mediaConfig, appMeasurement);

    // Tracker creation.
    var tracker = Media.getInstance();
```

### 向跟踪器提供播放头和QoE信息

#### 2.x

```javascript
    // Instance of MediaHeartbeatDelegate to return playhead and qosInfo to the tracker
    ADB.core.extend(SampleMediaHeartbeatDelegate.prototype,
                         MediaHeartbeatDelegate.prototype);
    function SampleMediaHeartbeatDelegate(player) { this.player = player }
    SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() {
        // Returns the current playhead from the player.
        return this.player.playhead;
    };
    SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() {
        // Returns the current QOS information if available from the player.
        var qosInfo = MediaHeartbeat.createQoSObject(this._player.bitrate,
                                                     this._player.startupTime,
                                                     this._player.fps,
                                                     this._player.droppedFrames);
        return qosInfo;
    };

    // Pass the delegate instance when creating the tracker.
    var tracker = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(),
                                      mediaConfig,
                                      appMeasurement);
```

#### 3.x

```javascript
        // When playhead changes, call
        tracker.updatePlayhead(this._player.playhead)

        // When new QoE information is available, call
        var qoeInfo = Media.createQoEObject(this._player.bitrate,
                                                     this._player.startupTime,
                                                     this._player.fps,
                                                     this._player.droppedFrames);
        tracker.updateQoEObject(qoeInfo)
```

### 媒体和广告的标准元数据和自定义元数据

#### 媒体

#### 2.x

```javascript
    var mediaObject = MediaHeartbeat.createMediaObject("name",
                                                       "id",
                                                       60.0,
                                                       MediaHeartbeat.StreamType.VOD,
                                                       MediaHeartbeat.MediaType.Video);
    // standard metadata
    var standardMetadata = {};
    standardMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "sample season";
    standardMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "sample show";
    // Set standard metadata on media object.
    mediaObject.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata,
                               standardMetadata);

    // custom metadata
    var customMetadata = {
        "customKey1" : "custom value",
        "customKey2" : "custom value"
    };

    mediaTracker.trackSessionStart(mediaObject, customMetadata);
```

#### 3.x

```javascript
    var mediaObject = Media.createMediaObject("name",
                                           "id",
                                           60.0,
                                           Media.StreamType.VOD,
                                           Media.MediaType.Video);

    var metadata = {};
    // standard metadata
    metadata[Media.VideoMetadataKeys.Season] = "sample season";
    metadata[Media.VideoMetadataKeys.Show] = "sample show";
    // custom metadata
    metadata["customKey1"] = "custom value";
    metadata["customKey2"] = "custom value";

    mediaTracker.trackSessionStart(mediaObject, metadata);
```

#### 广告

#### 2.x

```javascript
    var adObject = MediaHeartbeat.createAdObject("adName",
                                                 "adId",
                                                  1,
                                                  15.0);

    // standard metadata
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    // Set standard metadata on ad object.
    adObject.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata,
                               standardAdMetadata);

    // custom metadata
    var customMetadata = {
        "customKey1" : "custom value",
        "customKey2" : "custom value"
    };

    mediaTracker.trackEvent(MediaHeartbeat.Event.AdStart, adObject, customMetadata);
```

#### 3.x

```javascript
    var adObject = Media.createAdObject("adName",
                                                 "adId",
                                                  1,
                                                  15.0);


    var metadata = {};
    // standard metadata
    metadata[Media.AdMetadataKeys.Advertiser] = "Sample Advertiser";
    metadata[Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
    // custom metadata
    metadata["customKey1"] = "custom value";
    metadata["customKey2"] = "custom value";

    mediaTracker.trackEvent(Media.Event.AdStart, adObject, metadata);
```

---
title: 了解如何在 Android 中实施标准元数据
description: 了解如何在 Android 中设置要与跟踪调用一起发送的标准视频和广告元数据。
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 100%

---

# 在 Android 中实施标准元数据{#implement-standard-metadata-on-android}

## 标准元数据常量

| 常量名称 | 描述   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | 用于将标准元数据附加到 `MediaObject` 的常量。 |

## 元数据键 API 引用

* 创建标准元数据键值对的 `HashMap`。
   * [视频元数据键](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [音频元数据键](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* 在 `HashMap` 中使用元数据的标准元数据常量设置标准元数据 `MediaInfo`。
* 调用 `trackSessionStart()` API 时提供此 `MediaInfo` 对象。

## 实施示例

### 视频

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### 音频

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```

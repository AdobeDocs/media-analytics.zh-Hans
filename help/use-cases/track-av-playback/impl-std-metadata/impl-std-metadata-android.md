---
title: 了解如何在 Android 中实施标准元数据
description: 了解如何在 Android 中设置要与跟踪调用一起发送的标准视频和广告元数据。
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/BPJgzkr6dP7qSVYfhhkZOcz1uUzg2axuGRGgbjZ1n04
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 112
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

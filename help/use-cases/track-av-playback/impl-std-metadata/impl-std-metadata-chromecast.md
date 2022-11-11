---
title: 了解如何在Chromecast中实施标准元数据
description: 了解如何在Chromecast中设置标准视频和广告元数据。
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 67%

---

# 在 Chromecast 中实施标准元数据{#implement-standard-metadata-on-chromecast}

实例化一个标准元数据对象，填充所需变量，并在媒体心率对象中设置该元数据对象。例如：

```js
var standardVideoMetadata = {};
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show";
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season";

mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {};
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist";
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album";

mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

请在此处查看音频和视频元数据的完整列表：[音频和视频参数](/help/implementation/variables/audio-video-parameters.md)。

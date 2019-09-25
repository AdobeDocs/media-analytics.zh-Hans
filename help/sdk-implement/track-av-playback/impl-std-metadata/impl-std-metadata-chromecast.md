---
description: 'null'
seo-description: 'null'
seo-title: 在 Chromecast 中实施标准元数据
title: 在 Chromecast 中实施标准元数据
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

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

See the comprehensive list of audio and video metadata here: [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)

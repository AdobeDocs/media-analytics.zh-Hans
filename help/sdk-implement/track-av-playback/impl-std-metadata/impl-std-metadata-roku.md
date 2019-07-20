---
description: 'null'
seo-description: 'null'
seo-title: 在 Roku 中实施标准元数据
title: 在 Roku 中实施标准元数据
uuid: ae14d809-343f-452c-832a-f94 d3 d83 a90
translation-type: tm+mt
source-git-commit: c6c7afee72d21c832be77c723750ae0551793613

---


# 在 Roku 中实施标准元数据{#implement-standard-metadata-on-roku}

实例化一个标准元数据对象，填充所需变量，并在媒体心率对象中设置该元数据对象。

**视频:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**音频:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

请在此处查看视频元数据的完整列表：[音频和视频参数](../../../metrics-and-metadata/audio-video-parameters.md)


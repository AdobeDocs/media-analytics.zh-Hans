---
title: 了解如何在 Roku 中实施标准元数据
description: 了解如何在 Roku 中设置要与跟踪调用一起发送的标准视频和广告元数据。
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '63'
ht-degree: 100%

---

# 在 Roku 中实施标准元数据{#implement-standard-metadata-on-roku}

实例化一个标准元数据对象，填充所需变量，并在媒体心跳对象中设置该元数据对象。

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

请在此处查看视频元数据的完整列表：[音频和视频参数](/help/implementation/variables/audio-video-parameters.md)

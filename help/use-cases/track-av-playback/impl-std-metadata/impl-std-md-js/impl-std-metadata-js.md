---
title: 了解如何使用 JavaScript 2.x 实施标准元数据
description: 了解如何在浏览器应用程序 (JS 2.x) 中设置要与跟踪调用一起发送的标准视频和广告元数据。
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
exl-id: 889c294b-ac45-4e82-abb3-88ab70abbc3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '67'
ht-degree: 100%

---

# 使用 JavaScript 2.x 实施标准元数据{#implement-standard-metadata-on-javascript}

## 元数据常量

| 常量名称 | 描述   |
| --- | --- |
| `StandardMediaMetadata` | 用于将标准元数据附加到 `MediaObject` 的常量 |

## 实施

实例化一个标准元数据对象，填充所需变量，并在媒体心跳对象中设置该元数据对象。例如：

```js
_onVideoLoad = function () {
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

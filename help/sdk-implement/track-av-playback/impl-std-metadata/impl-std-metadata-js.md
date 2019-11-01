---
title: 在 JavaScript 中实施标准元数据
description: 介绍如何设置标准视频和广告元数据，以便在浏览器应用程序(JS)中通过跟踪调用发送该元数据。
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 JavaScript 中实施标准元数据{#implement-standard-metadata-on-javascript}

## 元数据常数

| 常量名称 | 描述   |
| --- | --- |
| `StandardMediaMetadata` | Constant for attaching standard metadata on `MediaObject` |

## 实施

实例化一个标准元数据对象，填充所需变量，并在媒体心率对象中设置该元数据对象。例如：

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


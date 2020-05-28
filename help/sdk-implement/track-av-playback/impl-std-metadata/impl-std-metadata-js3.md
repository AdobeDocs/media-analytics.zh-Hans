---
title: 使用JavaScript 3.x实现标准元数据
description: 介绍如何在浏览器应用程序 (JS) 中设置要与跟踪调用一起发送的标准视频和广告元数据。
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# 使用JavaScript 3.x实现标准元数据{#implement-standard-metadata-on-javascript}

## 实施

实例化上下文数据对象，填充所需的标准元数据变量。 例如：

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
    contextData[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season";
    contextData[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist";
    contextData[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album";
    contextData[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label";

    this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```

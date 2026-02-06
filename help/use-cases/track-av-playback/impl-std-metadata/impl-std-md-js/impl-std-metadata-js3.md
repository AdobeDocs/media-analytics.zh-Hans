---
title: 了解如何使用 JavaScript 3.x 实施标准元数据
description: 了解如何在浏览器应用程序 (JS 3.x) 中设置要与跟踪调用一起发送的标准视频和广告元数据。
exl-id: 228ba000-10e2-4906-8417-265a03367a9b
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '48'
ht-degree: 100%

---

# 使用 JavaScript 3.x 实施标准元数据{#implement-standard-metadata-on-javascript}

## 实施

实例化上下文数据对象，填充所需的标准元数据变量。例如：

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
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```

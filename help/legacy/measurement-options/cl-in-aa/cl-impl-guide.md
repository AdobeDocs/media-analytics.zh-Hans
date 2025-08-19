---
title: 自定义链接实施说明
description: 了解如何在流媒体服务中实施自定义链接跟踪。
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 93%

---

# 自定义链接实施指南{#custom-link-implementation-guide}

自定义视频跟踪可利用 Analytics `appMeasurement` 中的使用自定义链接代码的手动链接跟踪。大多数情况下，自定义视频链接视频跟踪会用在需要少量视频测量的平台和设备上。

* 在 JavaScript 中：`s.tl()` 函数
* 在移动设备应用程序中：[trackAction() Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=zh-Hans)、[trackAction() iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=zh-Hans) 和 [trackAction() OTT](/help/use-cases/analytics-with-ott/track-app-actions.md)
* 在 Data Insertion API 中：[linktype 标记](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## 要求

* 访问视频播放器 API 事件和数据
* 在使用 Analytics SDK 时能够添加脚本
* 如果使用 Data Insertion API，则能够添加跟踪信标（自定义脚本或硬编码）

## 元数据

* 可以将元数据作为链接数据的一部分添加到任何跟踪调用中
* 请记住要更新 `linkTrackVars` 和 `linkTrackEvents`

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
    s.linkTrackEvents = 'event3';
    s.prop10 = mediaName;
    s.eVar10 = mediaName;
    s.eVar12 = "video";
    s.eVar13 = document.title;
    s.eVar15 = mediaPlayerName;
    s.events = 'event3';
    s.tl(this,'o','Video Complete');
};
```

## 使用自定义链接的理由

* 需要满足最低的先决条件
* 适用于任何平台，包括无脚本
* 任何计算（如逗留时间或四分位点）都必须在自定义脚本中计算
* 无隐藏库或脚本，非常简单直观
* 全面控制视频数据的各个方面

## 适用于 HTML5 播放器的 JavaScript 示例

```javascript
<script type="text/javascript">
  myvideo = document.getElementById('movie');
  myvideo.addEventListener('play',myHandler,false);
  myvideo.addEventListener('seeked',myHandler,false);
  myvideo.addEventListener('seeking',myHandler,false);
  myvideo.addEventListener('pause',myHandler,false);
  myvideo.addEventListener('ended',myHandler,false);

  function myHandler(e) {
      var video = document.getElementsByTagName('video')[0];
      var mediaName="13502979:Sailing";
      var mediaLength = video.duration;
      var mediaPlayerName = "HTML5 Player";
      /*Define video offset*/
      if (video.currentTime > 0) {
          mediaOffset = Math.floor(video.currentTime);
      } else {
          mediaOffset = 0;
      };
      /*Call on video start*/
      if (e.type == "play") {
          if (mediaOffset == 0) {
              console.log(mediaPlayerName +
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime));
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event2';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event2';
              s.tl(this,'o','Video Start');
          }
      };

      /*Call on video pause*/
      if (e.type == "pause") {
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime));
          if (video.currentTime != video.duration) {
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event7';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event7';
              s.tl(this,'o','Video Pause');
          }
      };

      /*Call on video complete*/
      if (e.type == "ended") {
          console.log(mediaPlayerName +
            ' -> ended -> playhead: ' +
            Math.floor(video.currentTime));
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
          s.linkTrackEvents = 'event3';
          s.prop10= m ediaName;
          s.eVar10=mediaName;
          s.eVar12="video";
          s.eVar13=document.title;
          s.eVar15=mediaPlayerName;
          s.events='event3';
          s.tl(this,'o','Video Complete');
      };
  };
</script>
```

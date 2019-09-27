---
seo-title: 自定义链接实施指南
title: 自定义链接实施指南
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
translation-type: tm+mt
source-git-commit: 8727044729eb98634eaab129cbfdc88f90892a51

---


# Custom Link Implementation Guide{#custom-link-implementation-guide}

Custom Video Tracking uses [manual link tracking using custom link code](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) within Analytics `appMeasurement`. 大多数情况下，自定义视频链接视频跟踪会用在需要少量视频测量的平台和设备上。

* In JavaScript: the  function`s.tl()`
* 在移动设备应用程序中：[trackAction() Android](https://marketing.adobe.com/resources/help/en_US/mobile/android/actions.html)、[trackAction() iOS](https://marketing.adobe.com/resources/help/en_US/mobile/ios/actions.html) 和 [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* In the Data Insertion API: [linktype tag](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## 要求

* 有权访问视频播放器 API 事件和数据
* 使用 Analytics SDK 时，能够添加脚本
* 使用 Data Insertion API 时，能够添加跟踪信标（自定义脚本或硬编码）

## 元数据

* 可以将元数据作为链接数据的一部分添加到任何跟踪调用中
* Remember to update the `linkTrackVars` and `linkTrackEvents`

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

## 为何使用自定义链接

* 需要满足的前提条件很少
* 适用于任何平台，包括 NoScript
* 任何计算（例如逗留时间和四分位数）必须在自定义脚本中执行
* 非常简单，没有任何隐藏的库或脚本
* 可全方位完全掌控视频数据
* 可删除指向示例播放器的链接

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


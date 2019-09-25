---
seo-title: 设置概述
title: 设置概述
uuid: 06fedb-b0c8-4f7d-90c8-e374cde1695
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# 设置概述{#setup-overview}

>[!IMPORTANT]
>
>以下说明适用于2.x Media SDK。 如果您实施的是 1.x 版本的 Media SDK，请参阅 [1.x Media SDK 文档。](/help/sdk-implement/download-sdks.md) 对于Primetime集成商，请参 _阅以下Primetime Media SDK文档_ 。


## 最低平台版本支持 {#minimum-platform-version}

下表介绍了从2019年2月19日开始的每个SDK支持的最低平台版本。

| 操作系统／浏览器 | 需要的最低版本 |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ —— 棒棒糖 |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## 一般实施指南 {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

媒体跟踪涉及三个主要的 SDK 组件：
* 媒体心率配置 - 配置包含报表的基本设置。
* 媒体心率委派 - 委派控制播放时间和 QoS 对象。
* 媒体心率 - 包含成员和方法的主库。

完成以下实施步骤：

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  变量名称  | 描述  | 必需 |  默认值  |
   |---|---|:---:|---|
   | `trackingServer` | 用于 Media Analytics 的跟踪服务器。这与您的分析跟踪服务器不同。 | 是 | 空字符串 |
   | `channel` | 渠道名称 | 否 | 空字符串 |
   | `ovp` | 用于分发内容的在线媒体平台的名称 | 否 | 空字符串 |
   | `appVersion` | 媒体播放器应用程序/SDK 的版本 | 否 | 空字符串 |
   | `playerName` | 正在使用的媒体播放器的名称，例如“AVPlayer”、“HTML5 播放器”、“我的自定义播放器” | 否 | 空字符串 |
   | `ssl` | 指示是否应当通过 HTTPS 进行调用 | 否 | false |
   | `debugLogging` | 指示是否启用调试日志记录 | 否 | false |

1. 实施 `MediaHeartbeatDelegate`.

   |  方法名称  |  描述  | 必需 |
   | --- | --- | :---: |
   | `getQoSObject()` | 返回包含当前 QoS 信息的 `MediaObject` 实例。在播放会话期间，此方法将被调用多次。播放器实施必须始终返回最新的可用 QoS 数据。 | 是 |
   | `getCurrentPlaybackTime()` | 返回播放头的当前位置。对于 VOD 跟踪，该值以秒为单位，从媒体项目的开头起计算。对于 LINEAR/LIVE 跟踪，该值以秒为单位，从计划的开头起计算。 | 是 |

   >[!TIP]
   >
   >服务质量(QoS)对象是可选的。 如果 QoS 数据可供播放器使用，并且您想要跟踪该数据，则需要以下变量：

   | 变量名称 | 描述   | 必需 |
   | --- | --- | :---: |
   | `bitrate` | 媒体的比特率（以比特/秒为单位）. | 是 |
   | `startupTime` | 媒体的开始时间（以毫秒为单位）。 | 是 |
   | `fps` | 每秒显示的帧数。 | 是 |
   | `droppedFrames` | 截至目前的丢帧数量. | 是 |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. 此实例将用于以下所有的媒体跟踪事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要一个实例 `AppMeasurement` 来向Adobe Analytics发送调用。

1. 合并所有片段。

   以下代码示例为 HTML5 视频播放器使用我们的 JavaScript 2.x SDK：

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## 验证 {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

媒体分析跟踪实施会生成两种类型的跟踪调用：

* 媒体和广告开始调用将直接发送到Adobe Analytics(AppMeasurement)服务器。
* 心跳调用将发送到Media Analytics（心跳）跟踪服务器，在该服务器处理，并传递到Adobe Analytics服务器。

* **Adobe Analytics(AppMeasurement)服务器有关跟**&#x200B;踪服务器选项的详细信息，请参 [阅正确填充trackingServer和trackingServerSecure变量。](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Experience cloud访客ID服务需要RDC跟踪服务器或解析到RDC服务器的CNAME。

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** Media Analytics(Heartbeats)服务器**它始终采用“`[your_namespace].hb.omtrdc.net`”格式。 “”的值指`[your_namespace]`定您的公司，并由Adobe提供。

媒体跟踪在所有平台、桌面和移动设备上的工作方式都是相同的。Audio tracking currently works on mobile platforms. 在所有跟踪调用中，有一些需要验证的关键通用变量：

## SDK 1.x文档 {#section_acj_tkk_t2b}

| Video Analytics 1.x SDK |  开发人员指南（仅限PDF） |
| --- | --- |
| Android | [用于 Android 的配置 ](vhl-dev-guide-v15_android.pdf) |
| AppleTV | [用于 AppleTV 的配置 ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [用于 Chromecast 的配置 ](chromecast_1.x_sdk.pdf) |
| iOS | [用于 iOS 的配置 ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [用于 JavaScript 的配置 ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [用于 TVML 的配置 ](vhl_tvml.pdf) |

## Primetime Media SDK 文档 {#primetime-docs}

* [Primetime用户指南](https://helpx.adobe.com/primetime/user-guide.html)

---
title: 解释实施旧版 Media SDK
description: 了解如何设置**旧版** 2.x Media SDK 以在您的移动应用程序、OTT 和浏览器 (JS) 应用程序中进行媒体跟踪。
feature: Streaming Media
role: User, Admin, Developer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 97%

---

# 旧版 2.x 流媒体 SDK 设置概述{#setup-overview}

此部分中的说明适用于&#x200B;**旧版** 2.x Media SDK。

* 有关实施 1.x 版本的 Media SDK 的信息，请参阅 [1.x Media SDK 文档。](/help/getting-started/download-sdks.md)

* 有关 Primetime 集成程序，请参阅 _Primetime Media SDK 文档_。

>[!IMPORTANT]
>
>Adobe 将于 2021 年 8 月 31 日终止支持版本 4 Mobile SDK，届时还将终止对适用于 iOS 和 Android 的 Media Analytics SDK 的支持。有关更多信息，请参阅 [Media Analytics SDK 支持终止常见问题解答](/help/additional-resources/end-of-support-faqs.md)。


## 支持的最低平台版本 {#minimum-platform-version}

下表介绍了从 2019 年 2 月 19 日开始每个 SDK 支持的最低平台版本。

| 操作系统／浏览器 | 所需的最低版本 |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## 一般实施指南 {#general-implementation-guidelines}

媒体跟踪涉及三个主要 SDK 组件：
* 媒体心跳配置 - 配置包含用于报表的基本设置。
* 媒体心跳委派 - 委派控制播放时间和 QoS 对象。
* 媒体心跳 - 包含成员和方法的主库。

完成以下实施步骤：

1. 创建一个 `MediaHeartbeatConfig` 实例，并设置您的配置参数值。

   |  变量名称  | 描述  | 必需 |  默认值  |
   |---|---|:---:|---|
   | `trackingServer` | 适用于 Media Analytics 的跟踪服务器。这与您的分析跟踪服务器不同。 | 是 | 空字符串 |
   | `channel` | 渠道名称 | 否 | 空字符串 |
   | `ovp` | 用于分发内容的在线媒体平台的名称 | 否 | 空字符串 |
   | `appVersion` | 媒体播放器应用程序/SDK 的版本 | 否 | 空字符串 |
   | `playerName` | 正在使用的媒体播放器的名称（例如“AVPlayer”、“HTML5 播放器”、“我的自定义播放器”） | 否 | 空字符串 |
   | `ssl` | 指示是否应通过 HTTPS 进行调用 | 否 | false |
   | `debugLogging` | 指示是否启用调试日志记录 | 否 | false |

1. 实施 `MediaHeartbeatDelegate`。

   |  方法名称  |  描述  | 必需 |
   | --- | --- | :---: |
   | `getQoSObject()` | 返回包含当前 QoS 信息的 `MediaObject` 实例。在播放会话期间，此方法将被调用多次。播放器实施必须始终返回最新的可用 QoS 数据。 | 是 |
   | `getCurrentPlaybackTime()` | 返回播放头的当前位置。<br />对于 VOD 跟踪，该值以秒为单位，从媒体项目的开头起计算。<br />对于直播，如果播放器不提供有关内容持续时间的信息，则该值可以指定为自当天 UTC 午夜开始的秒数。<br />请注意：使用进度标记时，需要内容持续时间，并且播放头需要更新为从媒体项目开始的秒数，从 0 开始。 | 是 |

   >[!TIP]
   >
   >服务质量 (QoS) 对象是可选的。如果您的播放器有 QoS 数据，并且您希望跟踪该数据，则需要以下变量：

   | 变量名称 | 描述   | 必需 |
   | --- | --- | :---: |
   | `bitrate` | 媒体的比特率（以位/秒为单位）。 | 是 |
   | `startupTime` | 媒体的开始时间（以毫秒为单位）。 | 是 |
   | `fps` | 每秒显示的帧数。 | 是 |
   | `droppedFrames` | 到目前为止丢帧的数量。 | 是 |

1. 创建 `MediaHeartbeat` 实例。

   使用 `MediaHertbeatConfig` 和 `MediaHertbeatDelegate` 创建 `MediaHeartbeat` 实例。

   >[!IMPORTANT]
   >
   >在会话结束前，请确保您的 `MediaHeartbeat` 实例可以访问且未被取消分配。此实例将用于以下所有的媒体跟踪事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要 `AppMeasurement` 的实例，才能向 Adobe Analytics 发送调用。

1. 合并所有部分。

   以下代码示例对 HTML5 媒体播放器使用 JavaScript 2.x SDK。

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

## 验证 {#validate}

Media Analytics 跟踪实施会生成两种类型的跟踪调用：

* 将媒体和广告开始调用直接发送到 Adobe Analytics (AppMeasurement) 服务器。
* 将心跳调用发送到 Media Analytics (Heartbeats) 跟踪服务器，在该服务器上进行处理，然后传递到 Adobe Analytics 服务器。

* **Adobe Analytics (AppMeasurement) 服务器**
有关跟踪服务器选项的更多信息，请参阅[正确填充 trackingServer 和 trackingServerSecure 变量](https://helpx.adobe.com/analytics/kb/determining-data-center.html)。

  >[!IMPORTANT]
  >
  >Experience Cloud 访客 ID 服务需要一个 RDC 跟踪服务器或解析为 RDC 服务器的 CNAME。

  分析跟踪服务器应该以“`.sc.omtrdc.net`”结尾，或者应该为一个 CNAME。

* **&#x200B; Media Analytics (Heartbeats) 服务器**
其格式始终为“`[your_namespace].hb.omtrdc.net`”。“`[your_namespace]`”的值指定您的公司，由 Adobe 提供。

媒体跟踪在所有平台、桌面和移动设备上的工作方式都是相同的。音频跟踪当前适用于移动设备平台。在所有跟踪调用中，有一些需要验证的关键通用变量：

## SDK 1.x 文档 {#sdk-1x-documentation}

| Video Analytics 1.x SDK | 开发人员指南（仅 PDF） |
| --- | --- |
| Android | 为Android配置[&#128279;](vhl-dev-guide-v15_android.pdf) |
| Apple TV | 为Apple TV配置[&#128279;](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | 为Chromecast配置[&#128279;](chromecast_1.x_sdk.pdf) |
| iOS | 为iOS配置[&#128279;](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | 为JavaScript配置[&#128279;](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android：[配置 Media Analytics](https://help.adobe.com/zh_CN/primetime/psdk/android/1.4/index.html) </li> <li> DHLS：[配置 Media Analytics](https://help.adobe.com/zh_CN/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS：[配置 Media Analytics](https://help.adobe.com/zh_CN/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [为TVML配置](vhl_tvml.pdf) |

## Primetime Media SDK 文档 {#primetime-docs}

* [Primetime 用户指南](https://helpx.adobe.com/cn/primetime/user-guide.html)

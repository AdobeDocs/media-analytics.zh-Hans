---
title: 了解如何使用 JavaScript 3.x 跟踪广告
description: 使用 Media SDK 在浏览器 (JS) 应用程序中实施广告跟踪。
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 88%

---

# 使用 JavaScript 3.x 跟踪广告{#track-ads-on-javascript}

以下说明为使用 3.x SDK 的实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 SDK 之前的版本，可以在此处下载开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 广告跟踪常量

| 常量名称 | 描述   |
|---|---|
| `AdBreakStart` | 用于跟踪 AdBreak 开始事件的常量 |
| `AdBreakComplete` | 用于跟踪 AdBreak 结束事件的常量 |
| `AdStart` | 用于跟踪广告开始事件的常量 |
| `AdComplete` | 用于跟踪广告结束事件的常量 |
| `AdSkip` | 用于跟踪广告跳过事件的常量 |

## 实施步骤

1. 识别广告时间（包括前置广告）边界开始的时间，然后使用广告时间信息创建 `AdBreakObject`。

   `AdBreakObject` 引用：

   | 变量名称 | 类型 | 描述 |
   | --- | --- | --- |
   | `name` | 字符串 | 非空字符串，表示广告时间名称（前置式广告、中置式广告和后置式广告）。 |
   | `position` | 数字 | 广告时间的位置编号，从 1 开始编号。 |
   | `startTime` | 数字 | 广告时间开始的播放头值。 |

   广告时间对象创建：

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. 在 `MediaHeartbeat` 实例中使用 `AdBreakStart` 调用 `trackEvent()`，以开始跟踪广告时间：

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. 识别广告的开始时间，然后使用广告信息创建 `AdObject` 实例。

   `AdObject` 引用：

   | 变量名称 | 类型 | 描述 |
   | --- | --- | --- |
   | `name` | 字符串 | 表示广告名称的非空字符串。 |
   | `adId` | 字符串 | 表示广告标识符的非空字符串。 |
   | `position` | 数字 | 广告时间中广告的位置编号，从 1 开始编号。 |
   | `length` | 数字 | 正数，表示广告长度。 |

   广告对象创建：

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. （可选）通过上下文数据变量将标准和/或广告元数据附加到媒体跟踪会话。

   * [在 JavaScript 中实施标准广告元数据](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **自定义广告元数据 –** 对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告的数据进行填充：

     ```js
     /* Set context data */
     // Standard metadata keys provided by adobe.
     adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
     adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
     
     // Custom metadata keys
     adMetadata["affiliate"] = "Sample affiliate";
     adMetadata["campaign"] = "Sample ad campaign";
     adMetadata["creative"] = "Sample creative";
     ```

1. 在 `MediaHeartbeat` 实例中使用 `AdStart` 事件调用 `trackEvent()`，以开始跟踪广告播放。

   在事件调用中添加对自定义元数据变量（或空对象）的引用，以将其作为第三个参数：

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. 当广告播放到达广告结尾时，使用 `AdComplete` 事件调用 `trackEvent()`：

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. 如果由于用户选择跳过广告而使广告播放未能完成，则跟踪 `AdSkip` 事件：

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 7。
1. 当广告时间结束时，使用 `AdBreakComplete` 事件进行跟踪：

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

有关更多信息，请参阅跟踪场景[包含前置广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)。

## 粒度广告跟踪

默认广告Ping间隔为`10 seconds`。

您可以设置粒度广告跟踪以启用`1 second`广告跟踪。

>[!IMPORTANT]
>
>在启动跟踪会话时，必须提供此信息。



**语法**

```javascript
ADB.Media.MediaObjectKey = {
   GranularAdTracking: "media.granularadtracking"
   }
```

**示例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

// Enable granular ad tracking
mediaObject[ADB.Media.MediaObjectKey.GranularAdTracking] = true;

tracker.trackSessionStart(mediaObject);
```

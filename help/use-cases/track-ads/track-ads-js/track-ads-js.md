---
title: 了解如何使用JavaScript 2.x跟踪广告
description: 使用 Media SDK 在浏览器 (JS) 应用程序中实施广告跟踪。
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
exl-id: 4404d3a6-ab98-40f0-9573-ee32f480f650
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 96%

---

# 使用JavaScript 2.x跟踪广告{#track-ads-on-javascript}

以下说明为使用 2.x SDK 进行实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

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

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告时间的名称，例如前置广告、中置广告或后置广告。 | 是 |
   | `position` | 广告时间的位置编号，从 1 开始编号。 | 是 |
   | `startTime` | 广告时间开始的播放头值。 | 是 |

   广告时间对象创建：

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. 在 `MediaHeartbeat` 实例中使用 `AdBreakStart` 调用 `trackEvent()`，以开始跟踪广告时间：

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. 识别广告的开始时间，然后使用广告信息创建 `AdObject` 实例。

   `AdObject` 引用：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告的友好名称. | 是 |
   | `adId` | 广告的唯一标识符。 | 是 |
   | `position` | 广告时间中广告的位置编号，从 1 开始编号。 | 是 |
   | `length` | 广告长度 | 是 |

   广告对象创建：

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. （可选）通过上下文数据变量将标准和/或广告元数据附加到媒体跟踪会话。

   * [在 JavaScript 中实施标准广告元数据](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **自定义广告元数据 -** 对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告的数据进行填充：

      ```js
      /* Set custom context data */
      var adCustomMetadata = {
          affiliate: "Sample affiliate",
          campaign: "Sample ad campaign",
          creative: "Sample creative"
      };
      ```

1. 在 `MediaHeartbeat` 实例中使用 `AdStart` 事件调用 `trackEvent()`，以开始跟踪广告播放。

   在事件调用中添加对自定义元数据变量（或空对象）的引用，以将其作为第三个参数：

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. 当广告播放到达广告结尾时，使用 `AdComplete` 事件调用 `trackEvent()`：

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. 如果由于用户选择跳过广告而使广告播放未能完成，则跟踪 `AdSkip` 事件：

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 7。
1. 当广告时间结束时，使用 `AdBreakComplete` 事件进行跟踪：

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

有关更多信息，请参阅跟踪方案[包含前置广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)。

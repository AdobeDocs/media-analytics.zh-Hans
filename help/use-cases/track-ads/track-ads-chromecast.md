---
title: 了解如何在 Chromecast 中跟踪广告
description: 使用 Media SDK 在 Chromecast 应用程序中实施广告跟踪。
uuid: 7b1f584a-3472-416c-944c-5f5ea0ee5529
exl-id: 57465c42-b349-439d-b8d7-083b299a8c83
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 92%

---

# 在 Chromecast 中跟踪广告{#track-ads-on-chromecast}

以下说明为使用 2.x SDK 的实施提供了指南。

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

   广告时间对象创建：[createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName);
   ```

1. 在 `MediaHeartbeat` 实例中使用 `AdBreakStart` 调用 `trackEvent()`，以开始跟踪广告时间：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. 识别广告资源的开始时间，然后使用广告信息创建 `AdObject` 实例。

   广告对象创建：[createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH);
   ```

1. （可选）通过上下文数据变量将标准和/或广告元数据附加到媒体跟踪会话。

   * **标准广告元数据 —**&#x200B;对于标准广告元数据，请使用平台的键创建标准广告元数据键值对的字典：
   * **自定义广告元数据 -** 对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告资源的数据进行填充：

1. 使用 `AdStart` 事件调用 `trackEvent()`，以开始跟踪广告播放。

   在事件调用中添加对自定义元数据变量（或空对象）的引用，以将其作为第三个参数：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. 当广告资源播放到达广告结尾时，使用 `AdComplete` 事件调用 `trackEvent()`：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
   ```

1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 6。
1. 当广告时间结束时，使用 `AdBreakComplete` 事件进行跟踪：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

有关更多信息，请参阅跟踪场景[包含前置广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)。

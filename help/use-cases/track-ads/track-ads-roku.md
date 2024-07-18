---
title: 了解如何在 Roku 中跟踪广告
description: 使用 Media SDK 在 Roku 应用程序中实施广告跟踪。
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 100%

---

# 在 Roku 中跟踪广告{#track-ads-on-roku}

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

   `AdBreakObject` 引用：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告时间的名称，例如前置广告、中置广告或后置广告。 | 是 |
   | `position` | 广告时间的位置编号，从 1 开始编号。 | 是 |
   | `startTime` | 广告时间开始的播放头值。 | 是 |

   ```
   ‘ Create an adbreak info object
   adBreakInfo = adb_media_init_adbreakinfo()
   adBreakInfo.name = <ADBREAK_NAME>
   adBreakInfo.startTime = <START_TIME>
   adBreakInfo.position = <POSITION>
   ```

1. 在 `MediaHeartbeat` 实例中使用 `AdBreakStart` 调用 `trackEvent()`，以开始跟踪广告时间：

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. 识别广告资源的开始时间，然后使用广告信息创建 `AdObject` 实例。

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration)
   ```

1. （可选）通过上下文数据变量将标准和/或广告元数据附加到媒体跟踪会话。

   * [在 Roku 中实施标准广告元数据](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **自定义广告元数据 –** 对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告资源的数据进行填充：

     ```
     contextData = {}
     contextData["adinfo1"] = "adinfo2"
     contextData["adinfo2"] = "adinfo2"
     ```

1. 在 `MediaHeartbeat` 实例中使用 `AdStart` 事件调用 `trackEvent()`，以开始跟踪广告播放：

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. 当广告资源播放到达广告结尾时，使用 `AdComplete` 事件调用 `trackEvent()`。

   ```
   standardAdMetadata = {}
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. 如果由于用户选择跳过广告而使广告播放未能完成，则跟踪 `AdSkip` 事件：

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 7。
1. 当广告时间结束时，使用 `AdBreakComplete` 事件进行跟踪：

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

有关更多信息，请参阅跟踪场景[包含前置广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)。

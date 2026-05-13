---
title: 了解如何在 Android 中跟踪广告
description: 使用 Media SDK 在 Android 应用程序中实施广告跟踪。
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/9TbZkzhIR-b4nvKcVgmCAKsvN-nljf3YCDNPNEUA4yI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 381
ht-degree: 88%

---

# 在 Android 中跟踪广告{#track-ads-on-android}

以下说明为使用 2.x SDK 的实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 广告跟踪常量

| 常量名称 | 描述 |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | 用于跟踪 AdBreak 开始事件的常量 |
| `MediaHeartbeat.Event.AdBreakComplete` | 用于跟踪 AdBreak 结束事件的常量 |
| `MediaHeartbeat.Event.AdStart` | 用于跟踪广告开始事件的常量 |
| `MediaHeartbeat.Event.AdComplete` | 用于跟踪广告结束事件的常量 |
| `MediaHeartbeat.Event.AdSkip` | 用于跟踪广告跳过事件的常量 |

## 实施步骤

1. 识别广告时间（包括前置广告）边界开始的时间，然后使用广告时间信息创建 `AdBreakObject`。

   `AdBreakObject` 引用：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告时间名称，例如前置广告、中置广告和后置广告。 | 是 |
   | `position` | 广告时间在内容中的位置编号，从1开始编号。 | 是 |
   | `startTime` | 广告时间开始的播放头值。 | 是 |

   广告时间对象创建：

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. 在 `MediaHeartbeat` 实例中使用 `AdBreakStart` 调用 `trackEvent()`，以开始跟踪广告时间：

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null);
   }
   ```

1. 识别广告的开始时间，然后使用广告信息创建 `AdObject` 实例。

   `AdObject` 引用：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告的友好名称. | 是 |
   | `adId` | 广告的唯一标识符。 | 是 |
   | `position` | 广告时间中广告的位置编号，从1开始编号。 | 是 |
   | `length` | 广告长度 | 是 |

   广告对象创建：

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME>
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. （可选）通过上下文数据变量将标准和/或广告元数据附加到媒体跟踪会话。

   * [在 Android 中实施标准广告元数据](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)

   help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md

   * **自定义广告元数据 –** 对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告的数据进行填充：

     ```java
     // Setting Ad Metadata
     HashMap<String, String> adMetadata = new HashMap<String, String>();
     adMetadata.put("affiliate", "Sample affiliate");
     adMetadata.put("campaign", "Sample ad campaign");
     ```

1. 在 `MediaHeartbeat` 实例中使用 `AdStart` 事件调用 `trackEvent()`，以开始跟踪广告播放。

   在事件调用中添加对自定义元数据变量（或空对象）的引用，以将其作为第三个参数：

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata);
   }
   ```

1. 当广告播放到达广告结尾时，使用 `AdComplete` 事件调用 `trackEvent()`：

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null);
   }
   ```

1. 如果由于用户选择跳过广告而使广告播放未能完成，则跟踪 `AdSkip` 事件：

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null);
   }
   ```

1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 7。
1. 当广告时间结束时，使用 `AdBreakComplete` 事件进行跟踪：

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null);
   }
   ```

有关更多信息，请参阅跟踪场景[包含前置广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)。

---
seo-title: 概述
title: 概述
uuid: 1607798b-c6 ef-4d60-8e40-e958 c345 b09 c
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# 概述{#overview}

>[!IMPORTANT]
>
>以下说明为使用2.x SDK提供了实施指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK.](/help/sdk-implement/download-sdks.md)

广告播放包括跟踪广告时间、广告开始、广告结束和广告跳过。使用媒体播放器的API识别关键播放器事件并填充所需和可选的广告变量。请参阅此处全面的元数据列表： [广告参数。](/help/metrics-and-metadata/ad-parameters.md)

## Player活动 {#player-events}


### 在广告分页开始时

>[!NOTE]
>包括预滚动

* 为广告时间创建一个 `adBreak` 对象实例。例如：`adBreakObject`。

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### 在每个广告资产开始时

* 为广告资产创建一个广告对象实例。例如：`adObject`。
* Populate the ad metadata, `adCustomMetadata`.
* 为广告开始事件调用 `trackEvent`。

### 在每个广告完成时

* 为广告结束事件调用 `trackEvent`。

### 在广告跳过时

* 为广告跳过事件调用 `trackEvent`。

### 在广告时间结束时

* 为广告时间结束事件调用 `trackEvent`。

## 实施广告跟踪 {#section_83E0F9406A7743E3B57405D4CDA66F68}

### 广告跟踪常量

| 常量名称 | 描述   |
|---|---|
| `AdBreakStart` | 用于跟踪 AdBreak 开始事件的常量 |
| `AdBreakComplete` | 用于跟踪 AdBreak 结束事件的常量 |
| `AdStart` | 用于跟踪广告开始事件的常量 |
| `AdComplete` | 用于跟踪广告结束事件的常量 |
| `AdSkip` | 用于跟踪广告跳过事件的常量 |

### 实施步骤

1. 识别广告时间（包括前置广告）边界开始的时间，然后使用广告时间信息创建 `AdBreakObject`。

   `AdBreakObject` 参考：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告时间的名称，例如前置广告、中置广告或后置广告。 | 是 |
   | `position` | 内容中广告时间的位置编号，从 1 开始编号。 | 是 |
   | `startTime` | 广告时间开始的播放头值。 | 是 |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. 识别广告的开始时间，然后使用广告信息创建 `AdObject` 实例。

   `AdObject` 参考：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告的友好名称。 | 是 |
   | `adId` | 广告的唯一标识符。 | 是 |
   | `position` | 广告时间中广告的位置编号，从 1 开始编号。 | 是 |
   | `length` | 广告长度 | 是 |

1. （可选）通过上下文数据变量将标准和/或广告元数据附加到跟踪会话。

   * **标准广告元数据 -** 对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典。
   * **自定义广告元数据 -** 对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告的数据进行填充。

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   在事件调用中添加对自定义元数据变量（或空对象）的引用，以将其作为第三个参数。

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. 如果由于用户选择跳过广告而使广告播放未能完成，则跟踪 `AdSkip` 事件。
1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 7。
1. When the ad break is complete, use the `AdBreakComplete` event to track it.

>[!IMPORTANT]
>
>确保在广告播放()期间不增加内容播放器播放头(`l:event:playhead`)`s:asset:type=ad`。如果您这样做，内容逗留时间指标会受到负面影响。

以下示例代码将JavaScript2.x SDK用于HTML媒体播放器。

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```


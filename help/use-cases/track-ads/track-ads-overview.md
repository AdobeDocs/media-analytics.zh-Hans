---
title: 解释跟踪广告
description: 有关使用 Media SDK 实施广告跟踪的概述。
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 79%

---

# 概述{#overview}

以下说明为使用 2.x SDK 的实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

广告播放包括跟踪广告时间、广告开始、广告结束和广告跳过。可以使用媒体播放器的 API 来识别关键播放器事件，以及填充必需和可选的广告变量。请在此处查看元数据的完整列表：[广告参数](../../implementation/variables/ad-parameters.md)。

## 播放器事件 {#player-events}


### 在广告时间开始时

>[!NOTE]
>包括前置广告

* 为广告时间创建一个 `adBreak` 对象实例。例如，`adBreakObject`。

* 使用 `adBreakObject` 为广告时间开始事件调用 `trackEvent`。

### 在每个广告资源开始时

* 为广告资源创建一个广告对象实例。例如，`adObject`。
* 填充广告元数据 `adCustomMetadata`。
* 为广告开始事件调用 `trackEvent`。

### 在每个广告完成时

* 为广告结束事件调用 `trackEvent`。

### 在广告跳过时

* 为广告跳过事件调用 `trackEvent`。

### 在广告时间结束时

* 为广告时间结束事件调用 `trackEvent`。

## 实施广告跟踪 {#implement-ad-tracking}

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

   `AdBreakObject` 引用：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告时间名称，例如前置广告、中置广告和后置广告。 | 是 |
   | `position` | 广告时间在内容中的位置编号，从1开始编号。 | 是 |
   | `startTime` | 广告时间开始的播放头值。 | 是 |

1. 在 `MediaHeartbeat` 实例中使用 `AdBreakStart` 调用 `trackEvent()`，以开始跟踪广告时间。

1. 识别广告的开始时间，然后使用广告信息创建 `AdObject` 实例。

   `AdObject` 引用：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告的友好名称. | 是 |
   | `adId` | 广告的唯一标识符。 | 是 |
   | `position` | 广告时间中广告的位置编号，从1开始编号。 | 是 |
   | `length` | 广告长度 | 是 |

1. （可选）通过上下文数据变量将标准和/或广告元数据附加到跟踪会话。

   * **标准广告元数据 —**&#x200B;对于标准广告元数据，请使用平台的键创建标准广告元数据键值对的字典。
   * **自定义广告元数据 —**&#x200B;对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告的数据进行填充。

1. 在 `MediaHeartbeat` 实例中使用 `AdStart` 事件调用 `trackEvent()`，以开始跟踪广告播放。

   在事件调用中添加对自定义元数据变量（或空对象）的引用，以将其作为第三个参数。

1. 当广告播放到达广告结尾时，使用 `AdComplete` 事件调用 `trackEvent()`。

1. 如果由于用户选择跳过广告而使广告播放未能完成，则跟踪 `AdSkip` 事件。
1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 7。
1. 当广告时间结束时，使用 `AdBreakComplete` 事件对其进行跟踪。

>[!IMPORTANT]
>
>确保在广告播放 (`s:asset:type=ad`) 期间不增加内容播放器播放头 (`l:event:playhead`)。否则，“内容逗留时间”量度将受到不良影响。

以下代码示例对 HTML5 媒体播放器使用 JavaScript 2.x SDK。

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

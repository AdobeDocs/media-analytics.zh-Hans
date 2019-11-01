---
title: 解决广告之间出现的主要播放问题
description: 如何处理意外的main：广告之间的play调用。
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 解决在广告之间出现 main:play 的问题{#resolving-main-play-appearing-between-ads}

## 问题

在一些广告跟踪方案中，您可能会遇到在一个广告结束与另一个广告开始之间意外发生 `main:play` 调用的情况。If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. 如果这种回退到 `main:play` 的情况发生在前置广告时间，则内容开始量度可能会提前引入。

对于如上所述的广告空白，由于它与任何广告内容均不存在重叠，因此 Media SDK 会将其解读为主内容。Media SDK 上未引入任何广告信息，并且播放器处于播放状态。如果没有广告信息并且播放器处于播放状态，那么 Media SDK 会默认将出现的空白时长计入主内容的时长。VA SDK 不能将该播放时长计为无广告信息的时长。

## 识别

在使用Adobe Debug或网络数据包嗅探器（如Charles）时，如果在前置广告中断期间按此顺序看到以下心跳调用：

* 会话开始: `s:event:type=start` &amp; `s:asset:type=main`
* 广告开始: `s:event:type=start` &amp; `s:asset:type=ad`
* 广告播放: `s:event:type=play` &amp; `s:asset:type=ad`
* 广告结束: `s:event:type=complete` &amp; `s:asset:type=ad`
* 主要内容播放： `s:event:type=play` 和 `s:asset:type=main`**（意外）**

* 广告开始: `s:event:type=start` &amp; `s:asset:type=ad`
* 广告播放: `s:event:type=play` &amp; `s:asset:type=ad`
* 广告结束: `s:event:type=complete` &amp; `s:asset:type=ad`
* 主要内容播放： `s:event:type=play` 和 `s:asset:type=main`**（预期）**

## 解决办法

***延迟触发广告完成调用。***

在播放器内部处理此空白：延迟为第一个广告调用 `trackEvent:AdComplete`，然后紧接着为第二个广告调用 `trackEvent:AdStart`。当第一个广告完成后，应用程序应延迟调用 `AdComplete` 事件。请确保在广告时间为上一个广告调用 `trackEvent:AdComplete`。如果播放器能识别出当前的广告资产是广告时间的最后一个广告，则可立即调用 `trackEvent:AdComplete`。此解决办法将导致计入前一个广告单元的广告用时额外多出，多出的时间不会超过 1 秒。

**在广告时间（包括前置广告）开始时：**

* 为广告时间创建 `adBreak` 对象实例；例如，`adBreakObject`。

* 调用 `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**在每个广告资产开始时：**

* **呼叫`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >仅在上一广告未完成时调用此选项。 请考虑使用布尔值维护前一个广告的“`isinAd`”状态。

* 为广告资产创建广告对象实例：例如，`adObject`。
* Populate the ad metadata, `adCustomMetadata`.
* 调用 `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**在每个广告资产完成时：**

* **不要打电话**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**在广告跳过时：**

* 调用 `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**在广告时间完成时：**

* **呼叫`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* 调用 `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.


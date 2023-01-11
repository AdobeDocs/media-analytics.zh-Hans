---
title: 解决在广告之间出现 main:play 的问题
description: “了解如何处理在广告之间出现的意外 main:play 调用。”
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '448'
ht-degree: 100%

---


# 处理广告之间出现的间隔{#resolving-main-play-appearing-between-ads}

## 问题

在一些广告跟踪场景中，您可能会遇到在一个广告结束与另一个广告开始之间意外发生 `main:play` 调用的情况。如果广告完成调用与下一个广告开始调用之间的延迟超过 250 毫秒，则 Media SDK 将回退到发送 `main:play` 调用。如果这种回退到 `main:play` 的情况发生在前置广告时间，则内容开始量度可能会提前引入。

对于如上所述的广告空白，由于它与任何广告内容均不存在重叠，因此 Media SDK 会将其解读为主内容。Media SDK 上未引入任何广告信息，并且播放器处于播放状态。如果没有广告信息并且播放器处于播放状态，那么 Media SDK 会默认将出现的空白时长计入主内容的时长。VA SDK 不能将该播放时长计为无广告信息的时长。

## 识别

在使用 Adobe Debug 或网络数据包探查器（例如 Charles）时，如果您在前置广告时间看到按此顺序出现的以下心跳调用：

* 会话开始：`s:event:type=start` 和 `s:asset:type=main`
* 广告开始：`s:event:type=start` 和 `s:asset:type=ad`
* 广告播放：`s:event:type=play` 和 `s:asset:type=ad`
* 广告结束：`s:event:type=complete` 和 `s:asset:type=ad`
* 主内容播放：`s:event:type=play` 和 `s:asset:type=main`**（意外）**

* 广告开始：`s:event:type=start` 和 `s:asset:type=ad`
* 广告播放：`s:event:type=play` 和 `s:asset:type=ad`
* 广告结束：`s:event:type=complete` 和 `s:asset:type=ad`
* 主内容播放：`s:event:type=play` 和 `s:asset:type=main`**（预期）**

## 解决办法

***延迟触发广告完成调用。***

在播放器内部处理此空白：延迟为第一个广告调用 `trackEvent:AdComplete`，然后紧接着为第二个广告调用 `trackEvent:AdStart`。当第一个广告完成后，应用程序应延迟调用 `AdComplete` 事件。请确保在广告时间为上一个广告调用 `trackEvent:AdComplete`。如果播放器能识别出当前的广告资源是广告时间的最后一个广告，则可立即调用 `trackEvent:AdComplete`。此解决办法将导致计入前一个广告单元的广告用时额外多出，多出的时间不会超过 1 秒。

**在广告时间（包括前置广告）开始时：**

* 为广告时间创建 `adBreak` 对象实例；例如，`adBreakObject`。

* 调用 `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`。

**在每个广告资源开始时：**

* **调用`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >应仅在前一个广告未完成时调用此实例。请考虑使用布尔值维护前一个广告的“`isinAd`”状态。

* 为广告资源创建广告对象实例：例如，`adObject`。
* 填充广告元数据 `adCustomMetadata`。
* 调用 `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`。
* 调用 `trackPlay()`（如果这是前置广告时间的第一个广告）。

**在每个广告资源完成时：**

* **请勿进行调用**

   >[!NOTE]
   >
   >如果应用程序知道该资源是广告时间的最后一个广告，请在此时调用 `trackEvent:AdComplete`，并在 `trackEvent:AdBreakComplete` 中跳过设置 `trackEvent:AdComplete`

**在广告跳过时：**

* 调用 `trackEvent(MediaHeartbeat.Event.AdSkip);`。

**在广告时间完成时：**

* **调用`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >如果前面在上一次 `trackEvent:AdComplete` 调用中已经执行此步骤，那么可以跳过此调用。

* 调用 `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`。

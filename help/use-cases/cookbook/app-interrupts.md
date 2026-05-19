---
title: 处理播放期间的应用程序中断
description: 了解如何处理媒体播放过程中的跟踪中断问题。
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/BlL-c1rf5d3juDKHybex9vrPvQsBIiNXVO2ug9LKl0g
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 41%

---

# 处理播放期间的应用程序中断{#handling-application-interrupts-during-playback}

可以通过多种方式中断媒体应用程序中的播放。 例如，用户可以明确地按下暂停键，或者用户可以将应用程序置于后台。 不论媒体播放过程因何种原因中断，跟踪指令均相同。

1. 在应用程序中断（进入后台、媒体暂停等）时，调用 **`trackPause`**。
1. 在应用程序返回前台和/或媒体重新开始播放时，调用 **`trackPlay`**。

>[!NOTE]
>
>在应用程序从后台返回时调用`trackSessionStart`可能会导致截至该时间为止的播放未计入总播放时间，同时还会丢失之前的进度标记、区段等。 因此，在应用程序返回前台和/或媒体重新开始播放时，应调用 `trackPlay`。

## 有关处理应用程序中断的常见问题解答： {#faq-about-handling-application-interrupts}

* _应用程序应在会话关闭前多久转入后台？_

  如果应用程序允许后台播放，它可以通过调用我们的API继续跟踪，我们将发送所有常规跟踪ping。 除 YouTube Red 之外，并没有许多视频应用程序允许后台播放，但是，所有音频应用程序都允许这样做。 如果应用程序不允许后台播放，则明智的做法是先保持“暂停状态”一分钟，然后再结束跟踪会话。 此时，应用程序将无法再继续发送暂停 ping，这是因为在大多数情况下，应用程序无法判断用户是否将重新继续观看媒体，也无法判断何时终止观看过程。 在后台继续发送ping也是一种糟糕的体验。

* _在应用程序在后台长时间运行后，处理重新启动跟踪的正确方法是什么？_

  应用程序应该调用 `trackSessionEnd` 以终止跟踪会话。 从版本2.1开始，SDK发送“结束”ping以通知后端跟踪会话已关闭。

* _重新启动相同会话如何？_

  有关恢复跟踪会话的信息，请参阅[恢复不活动的会话](resuming-inactive.md)。SDK会发送一个“恢复”ping，以通知后端用户正在手动恢复会话。

* _如果同一会话调用了`trackSessionEnd`两次，会发生什么情况？_

  为同一会话多次调用`trackSessionEnd`是安全的。 后端关闭第一个事件上的会话，并静默丢弃该会话ID的所有后续事件，包括第二个`trackSessionEnd`。 这意味着竞争条件（例如，在查看器关闭播放器的同一时刻触发30分钟的非活动超时）不会生成重复数据。

* _如果在会话已处于活动状态时调用`trackSessionStart`，会发生什么情况？_

  如果会话尚未关闭，SDK将忽略第二次`trackSessionStart`调用。 如果需要启动新会话，请先调用`trackSessionEnd`以显式关闭当前会话，然后为新会话调用`trackSessionStart`。

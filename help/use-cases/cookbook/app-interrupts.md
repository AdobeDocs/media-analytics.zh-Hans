---
title: 处理播放期间的应用程序中断
description: 了解如何处理媒体播放过程中的跟踪中断问题。
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
exl-id: a84af6ad-dd4f-4f0d-93dd-66f2f84ddc0e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 90%

---

# 处理播放期间的应用程序中断{#handling-application-interrupts-during-playback}

可以通过多种方式中断媒体应用程序中的播放。例如，用户可以明确地按下暂停键，或者用户可以将应用程序置于后台。不论媒体播放过程因何种原因中断，跟踪指令均相同。

1. 在应用程序中断（进入后台、媒体暂停等）时，调用 **`trackPause`**。
1. 在应用程序返回前台和/或媒体重新开始播放时，调用 **`trackPlay`**。

>[!NOTE]
>
>在应用程序从后台返回时调用`trackSessionStart`可能会导致截至该时间为止的播放未计入总播放时间，同时还会丢失之前的进度标记、区段等。 因此，在应用程序返回前台和/或媒体重新开始播放时，应调用 `trackPlay`。

## 有关处理应用程序中断的常见问题解答： {#faq-about-handling-application-interrupts}

* _在会话关闭前，应当将应用程序置于后台多长时间？_

  如果应用程序允许后台播放，则它可以通过调用我们的 API 继续进行跟踪，我们也会发送所有常规跟踪 ping。除 YouTube Red 之外，并没有许多视频应用程序允许后台播放，但是，所有音频应用程序都允许这样做。如果应用程序不允许后台播放，则明智的做法是先保持“暂停状态”一分钟，然后再结束跟踪会话。此时，应用程序将无法再继续发送暂停 ping，这是因为在大多数情况下，应用程序无法判断用户是否将重新继续观看媒体，也无法判断何时终止观看过程。而且，如果应用程序在后台中还是不断发送 ping，这也不是一种很好的体验。

* _在应用程序已进入后台很长时间后，要如何正确操作才能重新启动跟踪？_

  应用程序应该调用 `trackSessionEnd` 以终止跟踪会话。从版本 2.1 起，SDK 会发送一个“终止”ping，以告知后端跟踪会话已关闭。

* _要如何重新启动同一个会话呢？_

  有关恢复跟踪会话的信息，请参阅[恢复不活动的会话](resuming-inactive.md)。SDK 会发送恢复 Ping 以通知后端用户正在手动恢复会话。

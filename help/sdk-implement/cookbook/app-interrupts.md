---
seo-title: 处理应用程序在播放过程中出现的中断问题
title: 处理应用程序在播放过程中出现的中断问题
uuid: 1ccb4507-bda6-462d-bf67-e22978a4db3d
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# 处理应用程序在播放过程中出现的中断问题{#handling-application-interrupts-during-playback}

媒体应用程序中的播放可以通过多种方式中断：用户显式按下暂停，或当用户将应用程序置于后台时。 无论哪些因素导致媒体播放中断，跟踪指令都是相同的：

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. 这样做会导致播放到该时间点为止不计入总播放时间，并会丢失以前的进度标记、段等。 Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## FAQ about handling application interrupts: {#faq-about-handling-application-interrupts}

* _在会话关闭前，应当将应用程序置于后台多长时间？_

   如果应用程序允许后台播放，则它可以通过调用我们的 API 继续进行跟踪，我们也会发送所有常规跟踪 ping。除YouTube红色之外，许多视频应用程序都允许后台播放，但所有音频应用程序都允许此操作。 如果应用程序不允许后台播放，则建议在“暂停状态”中停留一分钟，然后结束跟踪会话。 应用程序无法继续发送暂停ping ，因为在大多数情况下，它无法确定用户是要返回继续查看媒体，还是确定何时将停止媒体。 而且，如果应用程序在后台中还是不断发送 ping，这也不是一种很好的体验。

* _在应用程序已进入后台很长时间后，要如何正确操作才能重新启动跟踪？_

   应用程序应该调用 `trackSessionEnd` 以终止跟踪会话。从版本 2.1 起，SDK 会发送一个“终止”ping，以告知后端跟踪会话已关闭。

* _要如何重新启动同一个会话呢？_

   有关重新启动跟踪会话的详细说明，请参阅此页面：[恢复不活动的会话。](/help/sdk-implement/cookbook/resuming-inactive.md)SDK 会发送一个“恢复”ping，以告知后端用户正在手动恢复会话。


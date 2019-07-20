---
seo-title: 处理应用程序在播放过程中出现的中断问题
title: 处理应用程序在播放过程中出现的中断问题
uuid: 1ccb4507-bda6-462d-bf67-e22778 a4 db3 d
translation-type: tm+mt
source-git-commit: 8c9592ee7ad97de2cf4aefb226ed1390bc5b53a8

---


# 处理应用程序在播放过程中出现的中断问题{#handling-application-interrupts-during-playback}

在媒体应用程序中播放可能会以各种方式中断：用户显式按下暂停，或者当用户将应用程序放入后台时。无论何种原因导致媒体播放中断，跟踪说明都是相同的：

1. Call **`trackPause`** when the application is interrupted (goes to background, media pauses, etc.).
1. Call **`trackPlay`** when the application returns to the foreground and/or the media resumes playing.

>[!NOTE]
>
>The Media Analytics team has seen instances where customers called `trackSessionStart` when their app returned from the background. 这样做会导致播放在未计入总回放时间的情况下进行计算，以及丢失较早的进度标记、段等。Instead, call `trackPlay` when the app returns and/or the media resumes playing.

## FAQ about handling application interrupts: {#section_osf_xqs_h2b}

* _在会话关闭前，应当将应用程序置于后台多长时间？_

   如果应用程序允许后台播放，则它可以通过调用我们的 API 继续进行跟踪，我们也会发送所有常规跟踪 ping。除了YouTube Red之外，很多视频应用程序允许后台播放，但所有音频应用程序允许这样做。如果应用程序不允许后台播放，则建议在暂停状态下一分钟保留一分钟，然后结束跟踪会话。应用程序无法继续发送暂停ping，因为在大多数情况下，它无法确定用户是否返回继续查看媒体或确定何时将停止查看。而且，如果应用程序在后台中还是不断发送 ping，这也不是一种很好的体验。

* _在应用程序已进入后台很长时间后，要如何正确操作才能重新启动跟踪？_

   应用程序应该调用 `trackSessionEnd` 以终止跟踪会话。从版本 2.1 起，SDK 会发送一个“终止”ping，以告知后端跟踪会话已关闭。

* _要如何重新启动同一个会话呢？_

   有关重新启动跟踪会话的详细说明，请参阅此页面：[恢复不活动的会话。](../../sdk-implement/cookbook/resuming-inactive.md)SDK 会发送一个“恢复”ping，以告知后端用户正在手动恢复会话。


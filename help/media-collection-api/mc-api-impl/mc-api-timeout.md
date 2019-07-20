---
seo-title: 超时情况
title: 超时情况
uuid: 2a4ea13e-a561-4adf-b567-f980301 b32 c8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 超时情况{#timeout-conditions}

**Media Collection API超时条件**

Media Collection API无状态，与Media SDK的机制没有相同的机制，用于在超时条件发生时发出新的会话ID。出现超时情况时，后端将关闭会话，并且将删除使用该会话 ID 进行的所有后续调用。处理会话超时的逻辑必须在客户端中对进行处理。也就是说，播放器必须监控超时情况，并在超时发生时获取新的会话 ID。

* **10分钟：无API事件**

   如果后端没有收到任何API事件，它将关闭会话。
* **30分钟：无播放头更改**

   如果播放头未移动30分钟(例如，用户点击暂停并离开)，则后端将关闭会话。

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.


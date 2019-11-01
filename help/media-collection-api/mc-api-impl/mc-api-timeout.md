---
title: 超时情况
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 超时情况{#timeout-conditions}

**Media Collection API超时条件**

Media Collection API是无状态的，它与Media SDK没有相同的机制，在出现超时情况时发布新的会话ID。 出现超时情况时，后端将关闭会话，并且将删除使用该会话 ID 进行的所有后续调用。处理会话超时的逻辑必须在客户端中对进行处理。也就是说，播放器必须监控超时情况，并在超时发生时获取新的会话 ID。

* **10分钟：无API事件**

   如果后端未收到任何API事件，它将关闭会话。
* **30分钟：无播放头更改**

   如果播放头在30分钟内未移动（例如，用户点击“暂停”并离开），则后端将关闭会话。

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.


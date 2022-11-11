---
title: 超时情况
description: 了解流媒体收集API超时情况。
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 95%

---

# 超时情况{#timeout-conditions}

**媒体收集 API 超时条件**

媒体收集 API 是无状态的，因此它在出现超时情况时发出新会话 ID 的机制与 Media SDK 并不相同。出现超时情况时，后端将关闭会话，并且将删除使用该会话 ID 进行的所有后续调用。处理会话超时的逻辑必须在客户端中对进行处理。也就是说，播放器必须监控超时情况，并在超时发生时获取新的会话 ID。

* **10 分钟：无 API 事件**

   如果后端未收到任何 API 事件，则后端将关闭会话。
* **30 分钟：无播放头更改**

   如果播放头持续 30 分钟没有移动（例如，用户点击暂停并走开），则后端将关闭会话。

>[!NOTE]
>
>您还可以通过发送具有 `sessionEnd` 事件类型的 `events` 请求来强制结束会话。

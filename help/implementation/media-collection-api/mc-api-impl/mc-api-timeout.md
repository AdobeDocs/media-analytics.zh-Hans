---
title: 超时情况
description: 了解媒体收集API超时情况。
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
ht-degree: 60%

---

# 超时情况{#timeout-conditions}

**媒体收集 API 超时条件**

媒体收集 API 是无状态的，因此它在出现超时情况时发出新会话 ID 的机制与 Media SDK 并不相同。 当发生超时情况时，后端将关闭会话，并且所有随后使用该会话ID进行的调用都将被丢弃。 必须在客户端中处理处理处理会话超时的逻辑。 也就是说，播放器必须监控超时情况，并在发生超时时获取新的会话ID。

* **10 分钟：无 API 事件**

  如果后端未收到任何 API 事件，则后端将关闭会话。
* **30 分钟：无播放头更改**

  如果播放头持续 30 分钟没有移动（例如，用户点击暂停并走开），则后端将关闭会话。

>[!NOTE]
>
>您还可以通过发送具有 `sessionEnd` 事件类型的 `events` 请求来强制结束会话。

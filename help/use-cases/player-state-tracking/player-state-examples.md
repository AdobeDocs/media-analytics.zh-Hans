---
title: 播放器状态跟踪示例
description: 本主题包括播放器状态跟踪功能的示例。
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# 播放器状态跟踪示例


## 长时间暂停示例

当视频会话的暂停持续时间超过 30 分钟时，API 需要启动新会话。 这种情况下，客户端应生成新的会话 ID。 对于这两个视频会话，客户端应保留播放器所处的所有状态，并在 `sessionStart` 调用之后作为 `stateStart` 事件发送所有信息。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

发送 `sessionEnd` 后，必须启动新的视频会话，并且第一个 API 事件为：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

长时间暂停示例显示，播放器还会存储其状态，以便将它们发送到新的视频会话。

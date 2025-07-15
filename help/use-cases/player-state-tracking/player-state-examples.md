---
title: 播放器状态跟踪示例
description: 本主题包括播放器状态跟踪功能的示例。
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 100%

---

# 播放器状态跟踪示例


## 长时间暂停示例

当视频会话的暂停持续时间超过 30 分钟时，API 需要启动新会话。这种情况下，客户端应生成新的会话 ID。对于这两个视频会话，客户端应保留播放器所处的所有状态，并在 `sessionStart` 调用之后作为 `stateStart` 事件发送所有信息。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

发送 `sessionEnd` 后，必须启动新的视频会话，并且第一个 API 事件为：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

长时间暂停示例显示，播放器还会存储其状态，以便将它们发送到新的视频会话。

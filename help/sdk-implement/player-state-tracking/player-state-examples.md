---
title: 播放器状态跟踪示例
description: 本主题包括播放器状态跟踪功能的示例。
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 播放器状态跟踪示例

添加示例


## 长暂停示例

当视频会话的暂停持续时间超过30分钟时，API需要新会话。 发生这种情况时，客户端应生成新的会话ID。 对于两个视频会话，客户端应保留播放器所处的所有状态，并在调用后将所有信息 `stateStart` 作为事件发 `sessionStart` 送。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

发送 `sessionEnd` 后，必须启动新视频会话，第一个API事件为：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

长暂停示例显示播放器还存储其状态，因此可以将它们发送到新视频会话。

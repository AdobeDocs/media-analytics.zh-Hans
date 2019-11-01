---
title: 事件类型和描述
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 事件类型和描述{#event-types-and-descriptions}

## sessionStart

随电话发 `sessions` 送。 当响应返回时，您将从 Location 标头中提取会话 ID，并将其用于对收集服务器的后续事件调用。

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). 播放器可从中转变为“正在播放”的其他状态包括：“正在缓冲”，用户从“已暂停”状态恢复，播放器从错误中恢复，自动播放等等。

## ping

* **主内容 -** 必须在主内容播放期间每 10 秒发送一次，而不考虑已发送的其他 API 事件。第一个 Ping 事件应该在主内容播放开始 10 秒后触发。
* **广告内容** - 必须在广告跟踪期间每 1 秒发送一次。

Ping 事件应该&#x200B;*不*&#x200B;包含请求正文中的 `params` 映射。

## bitrateChange

在位图发生更改时发送。

## bufferStart

在缓冲开始时发送。 没有 `bufferResume` 事件类型。A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

当用户按下“暂停”时发送。 没有 `resume` 事件类型。A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

表示广告时间的开始

## adStart

指示广告的开始

## adComplete

表示广告时间的结束

## adSkip

发出广告跳过的信号

## adBreakComplete

表示广告时间的结束

## chapterStart

表示章节区段的开始

## chapterSkip

表示章节跳过

## chapterComplete

表示章节的完成

## error

发出错误信号。

## sessionEnd

这用于通知Media Analytics后端，在用户放弃查看内容且不太可能返回时立即关闭会话。

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

达到主内容的结尾时发送

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.


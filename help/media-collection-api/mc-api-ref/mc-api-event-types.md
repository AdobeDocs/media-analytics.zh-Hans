---
title: 事件类型和描述
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 事件类型和描述{#event-types-and-descriptions}

## sessionStart

随 `sessions` 调用发送。当响应返回时，您将从 Location 标头中提取会话 ID，并将其用于对收集服务器的后续事件调用。

## play

当播放器从一种状态变为“正在播放”状态（即，播放器触发了 `on('Playing')` 回调）时发送。播放器可从中转变为“正在播放”的其他状态包括：“正在缓冲”，用户从“已暂停”状态恢复，播放器从错误中恢复，自动播放等等。

## ping

* **主内容 -** 必须在主内容播放期间每 10 秒发送一次，而不考虑已发送的其他 API 事件。第一个 Ping 事件应该在主内容播放开始 10 秒后触发。
* **广告内容** - 必须在广告跟踪期间每 1 秒发送一次。

Ping 事件应该&#x200B;*不*&#x200B;包含请求正文中的 `params` 映射。

## bitrateChange

在比特率发生更改时发送。

## bufferStart

缓冲开始时发送。没有 `bufferResume` 事件类型。在 `bufferStart` 之后发送 `play` 事件时一定会发生 `bufferResume` 事件。

## pauseStart

用户按“暂停”时发送。没有 `resume` 事件类型。在 `pauseStart` 之后发送 `play` 事件时一定会发生 `resume` 事件。

## adBreakStart

表示广告时间的开始

## adStart

表示广告的开始

## adComplete

表示广告时间的结束

## adSkip

表示广告跳过

## adBreakComplete

表示广告时间的结束

## chapterStart

表示章节区段的开始

## chapterSkip

表示章节跳过

## chapterComplete

表示一个章节的结束

## error

表示出现错误。

## sessionEnd

此事件用于在用户放弃观看内容并且不太可能返回时通知 Media Analytics 后端立即关闭会话。

如果不发送 `sessionEnd`，则放弃的会话通常会超时（未收到任何事件的时间达到 10 分钟后，或者播放头没有发生移动的时间达到 30 分钟时），并且会话将被后端删除。

## sessionComplete

达到主内容的结尾时发送

>[!IMPORTANT]
>
>对于每个事件类型，您应该参考 [JSON 验证架构](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)，以验证正确的事件参数类型和要求。


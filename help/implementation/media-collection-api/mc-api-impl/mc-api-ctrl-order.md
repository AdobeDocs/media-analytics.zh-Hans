---
title: 控制事件的顺序
description: 了解如何控制事件的顺序以及在某些情况下如何根据 playerTime 对象中提供的时间戳对事件重新排序。
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 100%

---

# 控制事件的顺序{#controlling-the-order-of-events}

流视频跟踪是一项高度依赖于时间的操作，有时媒体收集 API 跟踪调用会无序到达后端。在此情况下，后端会尝试根据 `playerTime` 对象中提供的时间戳对事件进行排队和重新排序。这种情况有一些限制。当前，如果乱序调用之间的延迟超过了一秒，则重新排序可能会失败。在将来更新中，可以优化和配置“可接受的延迟时间”。

## 乱序事件示例

当事件通过网络时会发生乱序事件，这有时会导致延迟。

例如，您可以依次发送一个 `adBreakStart` 事件和一个 `adStart` 事件。这是一个常见用例，因为广告需要在广告时间内开始。

如果广告已就绪且不需要缓冲，这两个事件几乎立即发生，并且两个事件的 `playerTime.ts` 彼此非常接近，但它们绝不应相等。

> 对于任何事件，事件的“playerTime.ts”绝不应相等，因为排序算法不知道哪个事件首先发生。每 2 个连续事件应该至少有 1 毫秒的时间戳差值。

由于这两个事件在触发网络调用时发生的时间非常接近，因此它们可能会乱序到达。在此示例中，`adStart` 事件先于 `adBreakStart` 事件到达。


有一个事件的定时时段：5 秒或最多 10 个事件。事件在发送到处理管道之前会进行缓冲。当满足条件时（过了 5 秒或收到超过 10 个事件），事件将根据 `playerTime.ts` 重新排序，然后按新顺序发送到处理管道。

>[!IMPORTANT]
>
>有一个立即发送到处理管道的异常事件，即 `sessionStart` 事件。

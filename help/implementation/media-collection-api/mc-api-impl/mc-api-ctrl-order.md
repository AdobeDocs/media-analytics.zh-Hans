---
title: 控制事件的顺序
description: 了解如何控制事件的顺序以及在某些情况下如何根据 playerTime 对象中提供的时间戳对事件重新排序。
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 73%

---

# 控制事件的顺序{#controlling-the-order-of-events}

流视频跟踪是一项高度依赖于时间的操作，有时媒体收集 API 跟踪调用会无序到达后端。 在此情况下，后端会尝试根据 `playerTime` 对象中提供的时间戳对事件进行排队和重新排序。  这种情况有一些限制。 当前，如果乱序调用之间的延迟超过了一秒，则重新排序可能会失败。 在将来更新中，可以优化和配置“可接受的延迟时间”。

## 乱序事件示例

当事件通过网络时会发生乱序事件，这有时会导致延迟。

例如，您可以依次发送一个 `adBreakStart` 事件和一个 `adStart` 事件。 这是一个常见用例，因为广告需要在广告时间内开始。

如果广告已就绪且不需要缓冲，则两个事件几乎立即发生，并且两个事件的`playerTime.ts`彼此非常接近。 但是，它们绝不应该相等，因为排序算法不知道哪个事件首先发生。 对于任何连续事件，始终保持至少1毫秒的时间戳差异。

由于这两个事件在触发网络调用时发生的时间非常接近，因此它们可能会乱序到达。 在此示例中，`adStart` 事件先于 `adBreakStart` 事件到达。

有一个事件的定时时段：5 秒或最多 10 个事件。 事件在发送到处理管道之前会进行缓冲。 当满足条件时（过了5秒或收到超过10个事件），事件将根据`playerTime.ts`重新排序，然后按新顺序发送到处理管道。

>[!IMPORTANT]
>
>有一个立即发送到处理管道的异常事件，即 `sessionStart` 事件。

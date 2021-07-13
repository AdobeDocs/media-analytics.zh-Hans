---
title: 控制事件的顺序
description: 了解如何控制事件的顺序，以及在某些情况下如何根据playerTime对象中提供的时间戳对事件进行重新排序。
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 3%

---

# 控制事件的顺序{#controlling-the-order-of-events}

流视频跟踪是一种高度依赖于时间的操作，有时，媒体收集API跟踪调用会无序到达后端。 在这种情况下，后端会尝试根据`playerTime`对象中提供的时间戳对事件进行排队和重新排序。  这存在一些限制。 目前，如果失序调用之间的延迟超过一秒，则重新排序可能会失败。 在将来的更新中，“可接受的延迟时间”可以优化和配置。

## 无序事件示例

当事件通过网络时发生顺序错误事件，这有时会导致延迟。

例如，您可以发送一个`adBreakStart`事件，后跟一个`adStart`事件。 这是常见的用例，因为广告需要在广告时间内开始。

如果广告已准备就绪，并且不需要缓冲，则两个事件几乎会立即发生，并且两个事件的`playerTime.ts`彼此非常接近，但它们绝不应相等。

> 对于任何事件，事件的“playerTime.ts”永远不应相等，因为排序算法不会知道首先发生了什么事件。 每连续2个事件的时间戳差应至少为1毫秒。

由于这两个事件在触发网络调用时会非常接近彼此发生，因此它们可能会失序到达。 在此示例中， `adStart`事件在`adBreakStart`事件之前到达。


有一个事件的定时窗口：5秒或最多10个事件。 在将事件发送到处理管道之前，会先缓冲这些事件。 当满足条件（5秒已过或接收了10个以上事件）时，会根据`playerTime.ts`对事件重新排序，然后按新顺序将事件发送到处理管道。

>[!IMPORTANT]
>
>有一个异常事件会立即发送到处理管道，即`sessionStart`事件。

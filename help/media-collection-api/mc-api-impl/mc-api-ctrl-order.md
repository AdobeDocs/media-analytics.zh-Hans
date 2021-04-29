---
title: 控制事件的顺序
description: 控制事件的顺序
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: 27694ec83de89980404df7a7cc77fa42b3d1a751
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 4%

---

# 控制事件的顺序{#controlling-the-order-of-events}

流式视频跟踪是一个高度依赖时间的操作，有时Media Collection API跟踪调用会按顺序到达后端。 在这种情况下，后端会尝试根据`playerTime`对象中提供的时间戳来排队和重新排序事件。  这存在一些限制。 目前，如果失序调用之间的延迟超过一秒，则重新排序可能会失败。 在将来的更新中，可以优化和配置“可接受的延迟时间”。

## 无序事件示例

当事件通过网络时，会出现无序事件，这有时会导致延迟。

例如，您可以发送`adBreakStart`事件，后跟`adStart`事件。 这是一个常见用例，因为广告在广告中断内开始是必需的。

如果广告准备就绪，并且不需要缓冲区，则两个事件几乎都会立即出现，并且两个事件的`playerTime.ts`彼此非常接近，但它们永远不应相等。

> 对于任何事件,事件的“playerTime.ts”永远不应相等，因为排序算法不知道事件首先发生了什么。 每两个连续事件至少应有1毫秒的时间戳差。

由于两个事件在触发网络呼叫时都非常接近，因此它们可能出现故障。 在此示例中，`adStart`事件在`adBreakStart`事件之前到达。


有一个事件的计时窗口：5秒或最多10个事件。 在将事件发送到处理流水线之前缓冲这些数据。 当满足条件时 — 已通过5秒或接收10个以上事件时，将根据`playerTime.ts`对事件进行重新排序，然后以新顺序发送到处理流水线。

>[!IMPORTANT]
>
>存在一个异常事件，该异常会立即发送到处理管线，即`sessionStart`事件。

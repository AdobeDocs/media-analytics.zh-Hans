---
title: 跟踪播放
description: 了解播放事件以及如何实施播放、暂停、缓冲、ping和比特率更改跟踪。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Cc5T13Z1S15MyG-CxpxMoHX-ckULmIe0dfUOe7650DE
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 2%

---


# 跟踪播放

播放事件在整个会话期间跟踪媒体播放器中的状态转变。 它们构成事件流的核心，并应用于任何内容类型。

## 播放器事件

| 播放器事件 | 操作 |
| --- | --- |
| 媒体播放或继续 | 呼叫播放 |
| 媒体暂停 | 呼叫暂停开始 |
| 缓冲开始 | 呼叫缓冲开始 |
| 缓冲结束 | 呼叫播放 |
| 比特率更改 | 调用比特率更改 |
| 计时器触发 | 呼叫Ping |

## 实施步骤

1. 当内容的第一帧呈现在屏幕上时，在[会话开始](../session/session-start.md)后&#x200B;**调用[播放](play.md)**。 在暂停或缓冲停止后继续播放时，也发送播放。 没有单独的恢复事件。
1. 当用户暂停播放时，**调用[暂停开始](pause-start.md)**。 继续播放时发送播放。
1. 播放器停止等待数据时，**调用[缓冲启动](buffer-start.md)**。 在基于XDM的API上，当您发送下一个播放事件时推断缓冲结束。 在Mobile SDK上，解析缓冲时也显式调用`BufferComplete`。
1. **在主内容播放期间，每10秒调用[Ping](ping.md)**；在广告播放期间，每1秒调用一次Ping。 Ping保持会话活动状态并记录播放头运动。 Mobile SDK会自动发送ping；所有其他平台必须手动发送。
1. 当播放器协商新比特率时，**调用[比特率更改](bitrate-change.md)**。 包括当前QoE数据（比特率、每秒帧数、丢帧数），以便后端可以计算[平均比特率](/help/reporting/metrics/average-bitrate.md)和相关质量量度。

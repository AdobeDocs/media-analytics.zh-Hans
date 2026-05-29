---
title: 跟踪内容播放
description: 了解如何跟踪核心播放，包括跟踪媒体载入、媒体开始、媒体暂停和媒体结束。
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 2%

---


# 跟踪内容播放

核心播放跟踪涵盖媒体载入、开始、暂停、恢复、完成和会话结束。 虽然不强制，但缓冲和搜寻跟踪也是完整播放实施的核心组件。

## 播放器事件

| 播放器事件 | 操作 |
| --- | --- |
| 媒体加载 | 创建媒体对象；调用SessionStart |
| 媒体开始 | 呼叫播放 |
| 暂停 | 调用PauseStart |
| 从暂停中恢复 | 呼叫播放 |
| 媒体结束 | 调用SessionComplete |
| 媒体中止/卸载 | 调用Sessionend |
| 缓冲开始 | 调用Bufferstart |
| 缓冲结束 | 呼叫播放（恢复） |
| 搜寻开始 | 调用SeekStart |
| 搜寻结束 | 调用SeekComplete；然后调用Play |

## 实施步骤

1. **识别用户何时触发播放**（用户点击“播放”或自动播放触发）。 创建具有内容名称、ID、长度、流类型和媒体类型的媒体对象。 有关字段定义，请参阅[内容名称](/help/implementation/variables/core/content-name.md)、[内容ID](/help/implementation/variables/core/content-id.md)、[内容长度](/help/implementation/variables/core/content-length.md)、[流类型](/help/implementation/variables/core/stream-type.md)和[内容类型](/help/implementation/variables/core/content-type.md)。
1. **可选附加元数据** — 标准元数据（节目、季、集等） 和自定义上下文数据变量。 有关标准元数据密钥引用，请参阅[节目](/help/implementation/variables/standard-metadata/show.md)、[季](/help/implementation/variables/standard-metadata/season.md)、[集](/help/implementation/variables/standard-metadata/episode.md)、[流派](/help/implementation/variables/standard-metadata/genre.md)和[网络](/help/implementation/variables/standard-metadata/network.md)。
1. **调用[会话开始](/help/implementation/events/session/session-start.md)**&#x200B;以开始跟踪会话。 这会加载数据和元数据，并开始开始时间QoS测量。 SessionStart跟踪要播放的&#x200B;*意图*，而不是第一帧。
1. 当第一帧内容在屏幕上呈现时，**调用[播放](/help/implementation/events/playback/play.md)**。
1. 播放器暂停时，**调用[暂停开始](/help/implementation/events/playback/pause-start.md)**。 恢复播放时再次调用播放。 没有单独的恢复事件。
1. 当查看器到达内容结尾时，**调用[会话完成](/help/implementation/events/session/session-complete.md)**。
1. 当播放器卸载或查看器放弃内容而未到达结尾时，**调用[会话结束](/help/implementation/events/session/session-end.md)**。 SessionEnd立即关闭会话；之后将无法跟踪其他事件。

>[!IMPORTANT]
>
>`SessionEnd` 标记跟踪会话的结尾。 如果会话成功观看至结束，请在`SessionEnd`之前调用`SessionComplete`。 在`SessionEnd`之后将忽略任何其他跟踪调用，新会话的`SessionStart`除外。

## 核心播放

以下示例显示了一个完整的会话流 — 从会话开始到内容完成和会话结束。

有关平台实现的详细信息，请参阅[会话开始](/help/implementation/events/session/session-start.md)、[播放](/help/implementation/events/playback/play.md)、[暂停开始](/help/implementation/events/playback/pause-start.md)、[会话完成](/help/implementation/events/session/session-complete.md)和[会话结束](/help/implementation/events/session/session-end.md)。

## 缓冲

缓冲开始表示播放器正在等待数据。 在BufferStart（基于XDM的API）之后发送播放事件时推断缓冲结束。 在Mobile SDK上，还应显式调用BufferComplete。

有关实现详细信息，请参阅[缓冲开始](/help/implementation/events/playback/buffer-start.md)。

## 搜寻

搜寻开始表示查看器正在推移。 搜寻结束之后，播放，可继续播放内容。

有关实施详细信息，请参阅[暂停开始](/help/implementation/events/playback/pause-start.md) （搜寻开始）和[播放](/help/implementation/events/playback/play.md) （搜寻结束）。

## 处理应用程序中断

媒体应用程序中的播放过程可能会因为多种原因出现中断 — 用户按下暂停，应用程序进入后台，接到电话。 无论原因如何，跟踪指令都相同：

1. 当应用程序中断（进入后台、媒体暂停等）时，调用&#x200B;**PauseStart**。
1. 当应用程序返回前台和/或媒体重新开始播放时，调用&#x200B;**播放**。

>[!NOTE]
>
>当应用程序从后台返回时，请勿调用SessionStart。 调用SessionStart会导致截至该时间为止的播放不计入总播放时间，并且之前的进度标记、区段和章节边界将丢失。

**暂停的会话应何时结束？** 如果应用程序不允许后台播放，请立即调用PauseStart ，然后在后台运行大约一分钟后调用SessionEnd 。 应用程序无法从后台继续发送暂停ping，无限期地保持会话打开状态会带来不良体验。 如果应用程序支持后台播放（音频应用程序、视频播客应用程序），请在后台时继续发送ping。

**在较长的后台时段后重新启动：**&#x200B;如果应用程序在后台运行的时间足够长，导致会话过期（30分钟不活动），请调用SessionEnd以完全关闭任何延迟的会话，然后在查看器返回时调用SessionStart以开始一个新会话。

## 恢复不活动的会话

如果未在10分钟内收到任何事件，或者播放头在30分钟内未移动，则会话将自动过期。 如果用户在会话过期后返回，请再次调用SessionStart以打开新会话。

**跨设备恢复（跨设备切换）：**&#x200B;当查看者在设备之间传输播放内容（例如，从手机到电视的播放）时，请使用恢复标志在Analytics报表中将会话拼合在一起：

1. 在&#x200B;**源设备**&#x200B;上，当查看器启动转换时，调用SessionEnd。 不调用SessionComplete — 内容未完成。
1. 在&#x200B;**目标设备**&#x200B;上，调用SessionStart并将恢复标志设置为`true`，并从源设备传递相同的内容元数据和播放头位置。

设置恢复标志会导致Analytics在移交的第二阶段递增[内容恢复](/help/reporting/metrics/content-resumes.md)，而不是[媒体开始](/help/reporting/metrics/media-starts.md)。

**手动恢复先前关闭的会话：**&#x200B;如果应用程序存储用户数据并可以恢复先前关闭的会话，请在会话开始时设置恢复标志。 请参阅[会话开始](/help/implementation/events/session/session-start.md#resuming-a-session)以了解所有平台上的实施详细信息。

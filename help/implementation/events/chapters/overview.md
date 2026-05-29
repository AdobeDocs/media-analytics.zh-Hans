---
title: 跟踪章节和区段
description: 如何使用 Media SDK 实施章节和区段跟踪。
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 191
ht-degree: 39%

---


# 跟踪章节和区段

章节和区段跟踪适用于自定义的媒体章节或区段。 章节跟踪的一些常见用例包括根据媒体内容定义自定义区段（例如，棒球赛的回合），或者定义不同广告时间之间的内容区段。 对于核心媒体跟踪实施，章节跟踪&#x200B;**并非**&#x200B;必需项。

章节跟踪包括章节开始、章节结束和章节跳过。 使用具有自定义分段逻辑的媒体播放器API来识别章节事件并填充章节变量。

## 播放器事件

| 播放器事件 | 操作 |
| --- | --- |
| 章节开始 | 创建章节对象；调用ChapterStart |
| 章节结束 | 调用ChapterComplete |
| 章节跳过 | 调用ChapterSkip |

## 实施步骤

1. 识别章节开始事件的发生时间并创建章节对象。 有关字段定义，请参阅[章节名称](/help/implementation/variables/chapters/chapter-name.md)、[章节位置](/help/implementation/variables/chapters/chapter-position.md)、[章节长度](/help/implementation/variables/chapters/chapter-length.md)和[章节偏移](/help/implementation/variables/chapters/chapter-offset.md)。
1. 可以选择为自定义章节元数据创建上下文数据变量。
1. 调用[章节开始](/help/implementation/events/chapters/chapter-start.md)以开始跟踪该章节。
1. 当播放到达章节结束边界时，调用[章节结束](/help/implementation/events/chapters/chapter-complete.md)。
1. 如果用户在完成之前跳过章节，请调用[章节跳过](/help/implementation/events/chapters/chapter-skip.md)。
1. 对于其他章节，请重复步骤1至5。

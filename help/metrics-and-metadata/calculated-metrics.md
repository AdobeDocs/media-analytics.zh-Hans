---
title: 流媒体计算量度
description: 了解Adobe流媒体计算量度和量度公式。
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 59%

---

# 计算量度{#calculated-metrics}

流媒体的计算量度是自定义量度，允许您获取目标流媒体数据，例如每个媒体流的平均广告逗留时间或平均广告数。

有关Adobe Analytics计算量度的信息，请参阅《Adobe Analytics组件指南》中的[计算量度和高级计算（派生）量度](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=en)。

>[!NOTE]
>
>下列计算量度是于 2018 年 9 月 13 日引入的。

| 量度 | 描述 | 公式 |
|---|---|---|
| 每个媒体流的平均广告数 | 每次媒体开始的广告开始次数 | `Ad Starts / Media Starts` |
| 每个媒体流的平均章节数 | 每次媒体开始的章节开始次数 | `Chapter Start / Media Starts` |
| 平均平均逗留时间 | 每次媒体开始的总逗留时间(HH:MM:SS) | `Media Time Spent / Media Starts` |
| 平均内容逗留时间 | 每次内容开始的内容逗留时间(HH:MM:SS) | `Content Time Spent / Content Start` |
| 平均平均逗留时间 | 每次广告开始的广告逗留时间(HH:MM:SS) | `Ad Time Spent / Ad Start` |
| 平均章节逗留时间 | 每次章节开始的章节逗留时间(HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| 媒体完成率 | 内容完成次数与媒体启动次数的比率 (%) | `Content Completes/ Media Starts` |
| 内容完成率 | 内容完成次数与内容开始次数的比率 (%) | `Content Completes / Content Starts` |
| 广告完成率 | 广告完成次数与广告开始次数的比率 (%) | `Ad Completes / Ad Starts` |
| 章节完成率 | 章节完成次数与章节开始次数的比率 (%) | `Chapter Completes / Chapter Starts` |
| 开始前放弃的比率 | 开始前丢帧次数与媒体开始次数的比率 (%) | `Drops before Starts / Media Starts` |
| 内容暂停时间率 | 暂停总时间与内容逗留时间的比率 (%) | `Total Pause Duration / Content Time Spent` |
| 内容缓冲时间率 | 缓冲总时间与内容逗留时间的比率 (% ) | `Total Buffer Duration / Content Time Spent` |
| 内容开始时间率 | 开始时间与内容逗留时间的比率 (%) | `Time to Start / Content Time Spent` |
| 广告逗留时间率 | 广告逗留时间与内容逗留时间的比率 (%) | `Ad Time Spent / Content Time Spent` |

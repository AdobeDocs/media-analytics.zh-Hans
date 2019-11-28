---
title: 计算量度
description: null
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 计算量度{#calculated-metrics}

>[!NOTE]
>
>下列计算量度是于 2018 年 9 月 13 日引入的。

| 量度 | 描述 | 公式 |
|---|---|---|
| 每个媒体流的平均广告数 | 每次媒体开始的广告开始次数 | `Ad Starts / Media Starts` |
| 每个媒体流的平均章节数 | 每次媒体开始的章节开始次数 | `Chapter Start / Media Starts` |
| 媒体平均逗留时间 | 每次媒体开始的总逗留时间 (HH:MM:SS) | `Media Time Spent / Media Starts` |
| 内容平均逗留时间 | 每次开始内容的内容逗留时间 (HH:MM:SS) | `Content Time Spent / Content Start` |
| 广告平均逗留时间 | 每次开始广告的广告逗留时间 (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| 章节平均逗留时间 | 每次开始章节的章节逗留时间 (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| 媒体完成率 | 已完成的内容与已启动的媒体的比率 (%) | `Content Completes/ Media Starts` |
| 内容完成率 | 已完成的内容与已开始的内容的比率 (%) | `Content Completes / Content Starts` |
| 广告完成率 | 已完成的广告与已开始的广告的比率 (%) | `Ad Completes / Ad Starts` |
| 章节完成率 | 已完成的章节与已开始的章节的比率 (%) | `Chapter Completes / Chapter Starts` |
| 开始前放弃的比率 | 开始前丢帧次数与媒体开始次数的比率 (%) | `Drops before Starts / Media Starts` |
| 内容暂停时长比 | 内容暂停总时长与内容逗留时间的比率 (%) | `Total Pause Duration / Content Time Spent` |
| 内容缓冲时长比 | 内容缓冲总时长与内容逗留时间的比率 (%) | `Total Buffer Duration / Content Time Spent` |
| 内容开始时间比 | 内容开始时间与内容逗留时间的比率 (%) | `Time to Start / Content Time Spent` |
| 广告逗留时间比 | 广告逗留时间与内容逗留时间的比率 (%) | `Ad Time Spent / Content Time Spent` |

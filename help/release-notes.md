---
title: 流媒体服务发行说明
description: 查看流媒体服务的发行说明。
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: f73667dc-d296-4875-8975-ac3fdc3adc42id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: ac8a38fa-dec3-4581-8f64-178fde9f64e8id: c77ba355-6681-41fe-b719-563d3f507fdbid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 722
ht-degree: 35%

---

# 流媒体服务发行说明

**上次更新时间**：2026年6月4日

## 2026

| 功能 | 描述 | 日期 |
| --- | --- | --- |
| **支持计划数据** | 上传过去实时内容的计划数据以按项目或区段跟踪收视率。 支持的内容类型包括：<ul><li>FAST（免费广告支持电视）平台</li><li>本地流</li><li>直播体育赛事</li></ul>有关详细信息，请参阅[上传计划数据以跟踪实时内容](/help/use-cases/track-schedule-data.md)用例。 | 开始推出：2025年10月29日<p>正式发布：2026年10月</p> |

## 2025

| 功能 | 描述 | 日期 |
| --- | --- | --- |
| **`mediaTimed`XDM字段弃用** | `mediaTimed` XDM对象已弃用，支持`mediaReporting`字段路径。 在2025年5月9日之前实施了Analytics Source Connector的客户必须迁移其配置。 有关更多信息，请参阅以下迁移指南：<ul><li>[将受众迁移到新的流媒体字段](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[迁移Customer Journey Analytics以使用新的流媒体字段](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[将自定义字段的数据准备迁移至新的流媒体字段](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[将配置文件迁移到新的流媒体字段](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | 2025 年 10 月 |

## 2024

| 功能 | 描述 | 日期 |
| --- | --- | --- |
| **Web SDK支持** | 使用Web SDK或Web SDK标记扩展将流媒体Web数据发送到Adobe Experience Platform Edge Network，从而支持跨平台解决方案（如Customer Journey Analytics、Real-time CDP、Journey Optimizer和事件转发）的统一收集方法。 有关详细信息，请参阅[为流媒体设置Web SDK](/help/implementation/edge/web-sdk.md)或[为流媒体设置Web SDK标记扩展](/help/implementation/edge/web-sdk-tags.md)。 | 2024 年 5 月 29 日 |
| **Roku支持** | 使用Roku Edge SDK将流媒体数据发送到Adobe Experience Platform。 有关详细信息，请参阅[为流媒体设置Roku Edge](/help/implementation/edge/roku.md)。 | 2024 年 4 月 12 日 |

## 2023

| 功能 | 描述 | 日期 |
| --- | --- | --- |
| **Experience Edge支持** | 使用适用于iOS和Android的Media Edge API或Mobile SDK实施流媒体收集。<ul><li>[为流媒体设置Media Edge API](/help/implementation/edge/media-edge-api.md)</li><li>[为流媒体设置iOS](/help/implementation/edge/ios.md)或[为带有标记的流媒体设置iOS](/help/implementation/edge/ios-tags.md)</li><li>[为流媒体设置Android](/help/implementation/edge/android.md)或[为带有标记的流媒体设置Android](/help/implementation/edge/android-tags.md)</li></ul> | 2023年5月12日 |

## 2022

| 功能 | 描述 | 日期 |
| --- | --- | --- |
| **多个播放器状态跟踪** | 使用媒体收集API实施多个[播放器状态跟踪](/help/implementation/events/player-state/overview.md)。 | 2022 年 9 月 |
| 重命名的 XDM 字段 | 已重命名XDM字段名称以保持一致性：<ul><li>音频和视频参数</li><li>广告参数</li><li>章节参数</li><li>播放器状态参数</li><li>质量参数</li></ul> | 2022 年 9 月 |
| **个面板已添加到Customer Journey Analytics** | 已将[媒体并行查看者面板](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)和[媒体播放耗时面板](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)添加到Customer Journey Analytics。 | 2022 年 8 月 9 日 |
| **平均受众访问分钟数** | 您可以使用[平均受众访问分钟数面板](https://experienceleague.adobe.com/zh-hans/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel)来更好地了解平均内容使用情况。 <br>平均受众访问分钟数可以比较任何长度或类型的编程。 此外，您可以将此数字平均受众访问分钟数与线性电视平均访问分钟数指标进行比较或附加到其上。 此面板提供了更大的灵活性来衡量自定义时间段的平均受众访问，以及持续时间分类更新的时间。 | 2022 年 3 月 16 日 |

## 2021

| 功能 | 描述 | 日期 |
| --- | --- | --- |
| **媒体播放耗时** | “[播放耗时”面板](https://experienceleague.adobe.com/zh-hans/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent)提供了有关观看者参与情况的宝贵insight，并使媒体组织能够通过具备时段分割功能的高级耗时分析，利用以分钟计的用户参与获得更深入、更精细的见解。 您可以观察在特定时间点查看媒体流的耗时。 您可以按不同的粒度分割播放时长，包括新的 5 分钟、15 分钟和 30 分钟粒度。 | 2021 年 9 月 |

## 2020

| 功能 | 描述 | 日期 |
| --- | --- | --- |
| **“媒体并行查看者”面板** | [并行查看者面板](https://experienceleague.adobe.com/zh-hans/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers)可帮助您了解出现并发峰值或发生锐减的位置。 获得关于内容质量和观众参与情况的宝贵洞察，并帮助进行故障排除或规划数量和规模。<br><br>[媒体并行查看者面板（教程）](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | 2020年9月；2021年1月 |
| **支持的设备和平台** | Media Launch Extension w/ AEP SDK 现在支持以下 OTT 设备： <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | 2020 年 6 月 |

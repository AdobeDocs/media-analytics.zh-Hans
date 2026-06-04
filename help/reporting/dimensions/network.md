---
title: 网络
description: 报告广播网络或频道名称。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 11%

---


# 网络

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**网络**&#x200B;报告维度。 有关如何收集此变量，请参阅[网络](/help/implementation/variables/standard-metadata/network.md)。*

>[!ENDSHADEBOX]

**网络**&#x200B;维度报告广播网络或频道名称（例如，`"Fox"`或`"ESPN"`）。 使用它来比较同一流资产中跨网络的参与度。

## 如何填充此维度

网络由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.network`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## 维度项目

每个项目都是会话开始时报告的文字网络值。 每个网络使用稳定、不同的名称，以便数据不会跨拼写变量进行分段。

---
title: MVPD
description: 报告用户通过其进行身份验证的电缆、卫星或虚拟提供商。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%
---

# MVPD

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**MVPD**报表维度。 有关如何收集此变量，请参阅[MVPD](/help/implementation/variables/standard-metadata/mvpd.md)。*

>[!ENDSHADEBOX]

**MVPD** （多频道视频节目分发服务器）维度报告用户通过Adobe Pass进行身份验证的提供程序（例如，`"Comcast"`或`"DirecTV"`）。 使用它可中断身份验证提供商的参与。

## 如何填充此维度

MVPD由播放器在会话开始时设置，内容通过Adobe Pass审核。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.pass.mvpd`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## 维度项目

每一项都是会话开始时报告的文字MVPD名称。 每个提供商使用规范的Adobe Pass MVPD标识符，以便数据汇总到每个提供商的单行项目。

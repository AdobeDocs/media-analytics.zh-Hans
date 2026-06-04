---
title: 应用程序版本
description: 报告用于每个流会话的媒体播放器应用程序的版本。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---


# 应用程序版本

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**应用程序版本**&#x200B;报告维度。 有关如何收集此变量，请参阅[应用程序版本](/help/implementation/variables/core/app-version.md)。*

>[!ENDSHADEBOX]

**应用程序版本**&#x200B;维度报告在SDK初始化时配置的媒体播放器应用程序的版本字符串。 使用它可识别哪些播放器版本正在被积极使用、将质量或行为更改与特定版本关联起来，并优先考虑对广泛使用版本的支持。

>[!NOTE]
>
>此维度捕获&#x200B;**媒体播放器应用程序**&#x200B;的版本，而不是Adobe的SDK库。 Adobe自己的SDK库版本将作为单独的内部字段自动收集。

## 如何填充此维度

应用程序版本在SDK初始化时设置一次，并自动包含在每个会话开始请求中。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 使用Edge实施时通过XDM字段映射自动收集。 对于仅限Analytics的实施，使用[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md)将上下文数据`media.sdkVersion`映射到自定义eVar。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | 没有专用数据馈送列。 对于仅限Analytics的实施，使用通过处理规则配置的自定义eVar的数据馈送列。 |
| Audience Manager | `c_contextdata.media.sdkVersion` （仅限Analytics的实施） |

## 维度项目

每一项都是在SDK初始化时配置的文字版本字符串。 在您的实施中使用一致的版本化方案，以便版本字符串在报表中以可预见的方式汇总。

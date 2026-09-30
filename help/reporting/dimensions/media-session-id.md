---
title: 媒体会话ID
description: 唯一标识每个播放会话。
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
source-wordcount: '205'
ht-degree: 6%
---

# 媒体会话ID

**媒体会话ID**&#x200B;维度唯一标识每个播放会话。 它由后端生成，并在会话的每个事件上加盖标记。 使用它可隔离单个会话的事件以进行调试，或在自定义分析中删除重复的会话。

## 如何填充此维度

当后端收到[会话开始](/help/implementation/events/session/session-start.md)事件时，将自动生成会话ID。 Web SDK和移动SDK实施会捕获并保留您的ID；直接API实施必须从`sessionStart`响应（媒体收集API的`Location`标头或Media Edge API的`media-analytics:new-session`句柄）中读取会话ID，并将其包含在后续事件中。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.vsid`映射到eVar的[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## 维度项目

每个项目是由后端生成的唯一会话ID（通常是22个字符的数字字母字符串）。 使用过滤器或搜索字段查找特定会话。

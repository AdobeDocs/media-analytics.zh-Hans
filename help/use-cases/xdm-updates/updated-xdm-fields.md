---
title: 将Analytics源连接器实施更新为适用于流媒体服务的新XDM字段
description: 了解如何将Analytics源连接器实施迁移到更新的XDM流媒体字段
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: d239b203-71ce-4307-884f-9d11cc623d04
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# 将Analytics源连接器实施更新为适用于流媒体服务的新XDM字段

>[!NOTE]
>
>此信息适用于使用[Analytics Source Connector](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/analytics)将流媒体数据从Adobe Analytics引入Adobe Experience Platform以用于Customer Journey Analytics报表或任何其他平台服务的组织。
>
>这些更改不会影响Adobe Analytics作为独立应用程序，包括数据收集、处理和报表。 数据馈送和处理规则等工具不受影响，因此无需更新Analytics实施。

适用于流媒体服务的新Adobe数据收集(Analytics Source Connector)实施现已可用，它可以从一组XDM字段迁移到另一组XDM字段。

## 新建XDM字段路径

作为此迁移的一部分，`mediaReporting` XDM字段路径已添加到Adobe数据收集（Analytics源连接器）流中使用的XDM架构。 任何现有和新生成的Adobe数据收集架构都将自动包含此新字段。

## 替换旧的XDM字段路径

所有将流媒体数据从Adobe Analytics传输到Adobe Experience Platform的Adobe数据收集(Analytics Source Connector)流当前都在发送新`mediaReporting` XDM字段路径和旧`media.mediaTimed` XDM字段路径的数据。 这两个外地路径将在三个月内（截至2025年10月底）可用。 10月之后，`media.mediaTimed`字段将完全弃用，10月之后摄取的数据将仅包含`mediaReporting`。 弃用后，`media.mediaTimed`字段将不再显示在Adobe Experience Platform架构UI中，并且这些字段上的数据摄取将停止。 因此，这些字段将不再可用于任何Adobe Experience Platform服务。

在此日期之前摄取的数据将仍可用于报告。

## 与新XDM字段路径的其他差异

通过适用于流媒体的新的Adobe Source Connector实施，来自Adobe Analytics的保持活动调用现在被引入到Adobe Experience Platform中。

以前，这些调用不反映在Customer Journey Analytics等Platform应用程序中。 因此，您的组织可能会在报表中发现以下差异：

* **会话计数准确**：在某些情况下，这可能意味着会话计数减少，因为保持活动状态调用有助于保持活动用户会话，即使不存在直接媒体交互也是如此。 这些保持活动状态调用在每次媒体播放的最后一个事件后每20分钟生成一次，旨在保持访问处于打开状态。 要确保Customer Journey Analytics中的最佳会话跟踪，建议在数据视图中将访问过期时间配置为30分钟。

* **事件数增加**：因为保持活动状态调用现在计入Customer Journey Analytics Events指标中。 如果要从报表中排除保持活动状态调用，可创建一个过滤器，以排除事件类型为`media.keepalive`的事件。

此更改确保Analytics与CJA报表之间更好地保持一致。

## 迁移现有设置

为确保顺利过渡，所有客户必须在2025年10月底之前将现有设置从`media.mediaTimed`字段迁移到`mediaReporting`字段。 受影响的区域是依赖`media.mediaTimed`使用的区域，应按照以下部分所述迁移这些区域。

### Customer Journey Analytics**

可通过两种方式迁移CJA报表：

>[!NOTE]
>
>选择以下选项之一后，您必须手动将Customer Journey Analytics报表中使用的每个`media.mediaTimed`字段替换为其相应的派生字段或报表XDM字段路径。

* **要保留历史数据**：Adobe团队已开发了一个预定义的Customer Journey Analytics模板，该模板引入了一组将旧字段和新XDM字段组合为一个字段的派生字段。 可以根据每个Customer Journey Analytics连接的请求启用此模板。 请联系Adobe支持团队以帮助您启用新字段。 这些派生字段不计入组织的派生字段限制。

  要查看映射列表，请参阅Adobe Experience Platform和Customer Journey Analytics的[Media Analytics参数映射](/help/use-cases/xdm-updates/parameters-mapping.md)。

* **如果不需要历史数据**：在报告时使用报告XDM字段路径就足够了。 有关详细信息，请参阅[迁移Customer Journey Analytics以使用新的流媒体字段](/help/use-cases/xdm-updates/migrate-cja-setup.md)。

### Real-Time CDP

所有受众和配置文件必须基于`mediaReporting`。 有关详细信息，请参阅[将配置文件迁移到新的流媒体字段](/help/use-cases/xdm-updates/migrate-profiles.md)。

### 数据流和数据收集

动态配置和数据映射必须使用`mediaReporting`。 有关详细信息，请参阅[将自定义字段的数据准备迁移到新的流媒体字段](/help/use-cases/xdm-updates/migrate-dataprep.md)。

### 必须迁移的其他服务

* Adobe Journey Optimizer： Campaign和历程配置需要合并`mediaReporting`。

* 事件转发：配置中只应包含`mediaReporting`字段。

* 查询服务：查询必须引用`mediaReporting`字段。

* 标记配置：任何标记设置都应引用`mediaReporting`字段。

* 连接和目标：导入和导出数据流应围绕`mediaReporting`字段进行构建。

请注意，依赖于`media.mediaTimed`字段的任何其他流都将受到影响，并需要逻辑更新。

## 后续步骤和支持

所有使用Adobe Data Collection for Streaming Media的客户都必须在指定的过渡期内完成迁移。

如有任何问题或需要支持，请随时联系Adobe支持团队。

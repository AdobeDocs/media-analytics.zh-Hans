---
title: 将受众迁移到新的Adobe Analytics for Streaming Media数据类型
description: 了解如何将受众迁移到新的Adobe Analytics for Streaming Media数据类型
feature: Streaming Media
role: User, Admin, Developer
exl-id: 5664bf56-b228-430a-944c-faaab55fa108
TQID: https://experienceleague.adobe.com/TqsfcR2JgxVjDNx3-CBBa9n6pwvuGk9JgQ--DvWeHg0
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 1%

---

# 将受众迁移到新的流媒体字段

本文档介绍应如何迁移使用Adobe流媒体服务数据类型“媒体”中的字段的受众，以便使用名为“[媒体报表详细信息](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)”的新对应数据类型。

## 迁移受众

要将受众从名为“媒体”的旧数据类型迁移到名为“[媒体报告详细信息](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)”的新数据类型，您必须编辑受众，并在每个规则中将已弃用数据类型的旧字段替换为新数据类型的相应字段：

1. 查找包含来自已弃用“媒体”数据类型的字段的规则。 这是以路径`media.mediaTimed`开头的所有字段。

1. 使用新“[媒体报告详细信息](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)”数据类型的字段复制这些规则。

1. 将这两个规则都保留在适当位置，直到您验证受众是否按预期工作。

1. 从已弃用的“Media”数据类型中删除包含字段的规则。

1. 验证受众是否仍在按预期工作。

查看[内容ID](/help/reporting/dimensions/content.md)参数以及[流媒体服务](/help/media-overview.md)下记录的其余流媒体变量，以便在旧字段和新字段之间映射。 旧字段路径位于“XDM字段路径”属性下，而新字段路径位于“报告XDM字段路径”属性下。

![旧和新XDM字段路径](assets/field-paths-updated.jpeg)

## 示例

为了更便于遵循迁移准则，请考虑以下示例，其中包含具有单个规则的受众。 由于受众只有一个规则，因此您只需应用迁移准则一次。

1. 选择右上角的&#x200B;[!UICONTROL **编辑受众**]&#x200B;按钮。

1. 找到为受众配置的规则。

   ![编辑受众](assets/audience-edit.jpeg)

   ![编辑受众](assets/audience-edit2.jpeg)

1. 选择规则以打开其配置。

   ![编辑受众](assets/audience-edit3.jpeg)

1. （可选）要查看规则中使用的字段的路径，请选择字段名称旁边的信息按钮。

   ![编辑受众](assets/audience-edit4.jpeg)

1. 标识字段名称（本例中为“Media Starts”）。

   ![编辑受众](assets/audience-edit5.jpeg)

1. 查看[流媒体服务](/help/media-overview.md)下记录的流媒体变量以在旧字段之间映射。 旧字段路径可在“XDM字段路径”属性下找到，而新字段路径可在“报告XDM字段路径”属性下找到。 例如，对于[Media Starts](/help/reporting/metrics/media-starts.md)参数，`media.mediaTimed.impressions.value`的通讯对方是`xdm.mediaReporting.sessionDetails.isViewed`。

   ![已更新XDM路径](assets/updated-xdm-path.jpeg)

1. 使用新字段添加与现有规则相同的规则。

   ![添加规则](assets/add-rule.jpeg)

   ![添加规则](assets/add-rule2.jpeg)

   ![添加规则](assets/add-rule3.jpeg)

1. 选择&#x200B;[!UICONTROL **保存**]&#x200B;以保存受众。 您可以保留此设置，只要您需要验证受众是否仍按预期工作。

1. 验证完成后，删除旧字段，然后选择&#x200B;[!UICONTROL **保存**]&#x200B;以保存受众。

   ![添加规则](assets/add-rule4.jpeg)

1. 再次验证受众。

   受众迁移过程已完成。

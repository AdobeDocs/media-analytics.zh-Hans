---
title: 发送 QoE 数据
description: 了解如何使用qoeData JSON键发送事件。
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 84%

---

# 发送 QoE 数据{#sending-qoe-data}

每个事件都可以使用名为 `qoeData` 的额外 JSON 键进行修饰，该键位于 JSON 请求正文中的 `params` 键旁边。

>[!NOTE]
>
>您应该查看 [JSON 验证架构](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)以验证参数类型以及它们是必选参数还是可选参数。

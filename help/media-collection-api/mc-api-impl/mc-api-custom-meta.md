---
title: 自定义元数据支持
description: 自定义元数据支持
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# 自定义元数据支持{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自定义键:值对。此信息必须在 JSON 键 `customMetadata` 中提供，该键位于 `params` 键旁边。

`customMetadata` JSON 键应包含键:值对的对象。该键应该只包含字母数字字符、下划线和点/句点。

[MA 收集 API 事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

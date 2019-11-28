---
title: 自定义元数据支持
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 自定义元数据支持{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自定义键:值对。此信息必须在 JSON 键 `customMetadata` 中提供，该键位于 `params` 键旁边。

`customMetadata` JSON 键应包含键:值对的对象。该键应该只包含字母数字字符、下划线和点/句点。

[MA 收集 API 事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)


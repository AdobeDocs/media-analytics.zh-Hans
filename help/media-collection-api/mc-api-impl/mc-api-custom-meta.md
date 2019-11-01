---
title: 自定义元数据支持
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 自定义元数据支持{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. 此信息必须在 JSON 键 `customMetadata` 中提供，该键位于 `params` 键旁边。

The `customMetadata` JSON key should contain an object of key:value pairs. 该键应该只包含字母数字字符、下划线和点/句点。

[MA Collection API事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)


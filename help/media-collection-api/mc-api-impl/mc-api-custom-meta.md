---
seo-title: 自定义元数据支持
title: 自定义元数据支持
uuid: df4109dd-9fca-4c33-a7 d5-8e6 eec257527
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 自定义元数据支持{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. 此信息必须在 JSON 键 `customMetadata` 中提供，该键位于 `params` 键旁边。

`customMetadata` JSON键应包含一个密钥对象：值对。该键应该只包含字母数字字符、下划线和点/句点。

[MA Collection API事件](../mc-api-ref/mc-api-events-req.md)


---
title: 自定义元数据支持
description: “了解如何在sessionStart、chapterStart和adStart事件中提供自定义键：值对。”
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 48%

---

# 自定义元数据支持{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自定义键:值对。此信息必须在 JSON 键 `customMetadata` 中提供，该键位于 `params` 键旁边。

`customMetadata` JSON 键应包含键:值对的对象。该键应该只包含字母数字字符、下划线和点/句点。

[MA 收集 API 事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## 示例

当前，您可以发送具有以下键值对的`sessionStart`事件：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

对于上述配置，发送到Analytics的报表数据如下所示：

`c.a.media.channel=channel-2`

### 推荐

我们建议您为自定义元数据使用单独的命名空间。 例如：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

在推荐的示例中，发送给Analytics的自定义元数据的报表数据如下所示：

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`

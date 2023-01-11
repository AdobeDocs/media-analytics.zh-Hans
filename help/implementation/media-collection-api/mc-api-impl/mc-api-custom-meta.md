---
title: 自定义元数据支持
description: “了解如何在 sessionStart、chapterStart 和 adStart 事件中提供自定义键值对。”
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '127'
ht-degree: 100%

---

# 自定义元数据支持{#custom-metadata-support}

您可以在 `sessionStart`、`chapterStart` 和 `adStart` 事件中提供自定义键:值对。此信息必须在 JSON 键 `customMetadata` 中提供，该键位于 `params` 键旁边。

`customMetadata` JSON 键应包含键:值对的对象。该键应该只包含字母数字字符、下划线和点/句点。

[MA 收集 API 事件](../mc-api-ref/mc-api-events-req.md)

## 示例

目前，您可以使用以下键值对发送 `sessionStart` 事件：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

对于上述配置，发送到 Analytics 的报告数据如下：

`c.a.media.channel=channel-2`

### 推荐

我们建议您为自定义元数据使用单独的命名空间。例如：

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

在推荐的示例中，发送到 Analytics 的自定义元数据的报告数据如下：

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`

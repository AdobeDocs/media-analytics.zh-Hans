---
title: 自定义元数据支持 — XDM格式
description: 了解如何使用Experience Edge XDM格式发送带有媒体跟踪事件的自定义元数据。
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 5%

---


# 自定义元数据支持 — XDM格式

Experience Edge API允许您在`sessionStart`、`adStart`和`chapterStart` API事件中发送媒体自定义元数据以及标准XDM字段。 通过XDM格式发送的媒体自定义元数据可以转发到&#x200B;**Adobe Analytics**&#x200B;和&#x200B;**Adobe Experience Platform**。

有关媒体收集API实施，请参阅[自定义元数据支持](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)。

## 概述

可以在Experience Edge请求中的两个位置发送媒体自定义元数据，每个位置具有不同的路由行为：

| 位置 | 发送至Adobe Analytics | 发送至Adobe Experience Platform | 用例 |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅是 | ✅是 | 两个系统都需要业务数据 |
| `_data` | ✅是 | ❌否 | 特定于Analytics的标记或处理提示 |

自定义元数据适用于三种事件类型：

| 事件 | 元数据应用于 |
|-------|-------------------|
| `sessionStart` | 主要内容（整个会话） |
| `adStart` | 个人广告 |
| `chapterStart` | 内容章节或区段 |

## 结构

### `xdm.mediaCollection.customMetadata` (Analytics + AEP)

自定义元数据是`mediaCollection`对象中的名称值对象&#x200B;**的**&#x200B;数组：

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

<InlineAlert variant="warning" slots="text" />

`customMetadata`必须是`mediaCollection`内的&#x200B;**数组**，而不是位于`xdm`根级别。

**不正确：**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**正确：**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data` （仅限Analytics）

`_data`对象是一个特殊的Experience Edge构造，它绕过Adobe Analytics数据集，以独占方式将数据发送到AEP。 自定义元数据必须放在`__adobe.analytics.contextData`下。

与使用&#x200B;**名称值对象**&#x200B;数组的`xdm.mediaCollection.customMetadata`不同，`_data`映射直接在`contextData`下使用平面&#x200B;**键值对象**：

| 方法 | 结构 | 目的地 |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | `{"name": "...", "value": "..."}`对象的数组 | Analytics + AEP |
| `_data.__adobe.analytics.contextData` | 平面键值对象`{"key": "value"}` | 仅限Analytics |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### 命名约定

* **XDM格式：**&#x200B;前缀，租户命名空间使用下划线。 您还可以在租户自定义字段组中创建结构，如`_<tenant>.<struct_name>.<field_name>`。
* **`_data`格式：**&#x200B;字段放在`_data.__adobe.analytics.contextData`下。 字段名称无需使用下划线前缀（例如，`debugFlag`）。

## 主内容自定义元数据

与`sessionStart`一起发送。 适用于被跟踪的主媒体，并在整个广告和章节调用中保持可用。 此处定义的任何自定义元数据都将由媒体后端在相应的关闭调用中自动合并。 它将与为广告和章节定义的任何特定自定义元数据一起包含。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 请求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## 广告自定义元数据

与`adStart`一起发送。 特定于每个单独广告。 来自`sessionStart`的自定义元数据也将由广告关闭调用上的媒体后端与此处定义的任何特定于广告的自定义元数据自动合并。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 请求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## 章节自定义元数据

与`chapterStart`一起发送。 特定于每个内容章节或区段。 来自`sessionStart`的自定义元数据也将由媒体后端在章节关闭调用中自动合并，以及此处定义的任何特定于章节的自定义元数据。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 请求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## 使用`_data`对象（仅限Analytics的元数据）

当您在Adobe Analytics中需要&#x200B;**而不是**&#x200B;存储在AEP数据集中的元数据时，请使用`_data`对象。 示例包括临时标记、调试变量或特定于Analytics的处理提示。

<InlineAlert variant="warning" slots="text" />

通过`_data`发送的数据未存储在Adobe Experience Platform中，并且不适用于Real-Time CDP、Journey Orchestration或其他AEP服务。

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### 请求

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

在此示例中：

* `_mycompany.league`→发送到Analytics和AEP
* `debugMode`和`testFlag`（在`_data.__adobe.analytics.contextData`下）仅→发送到Analytics


## 下游数据位置

<InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata`是用于随事件发送自定义元数据的&#x200B;**入站API路径**。 处理后，数据将作为上下文数据变量转发到Adobe Analytics，并存储在`xdm.mediaReporting.customMetadata`下的Adobe Experience Platform中以及作为顶级拼合字段。

**Adobe Analytics:**

* 处理后，自定义元数据将作为上下文数据变量转发到Adobe Analytics。 `_tenant`前缀被自动去除，因此处理规则仅引用`_tenant`之后的字段路径（例如，`_mycompany.contentCategory`变为`contentCategory`）
* 通过`_data`发送的数据也将转发到Adobe Analytics，并可通过处理规则使用
* 使用处理规则将上下文数据变量映射到eVar、prop或其他Analytics变量。 有关详细信息，请参阅Adobe Experience Platform Edge Network的[数据变量映射](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/aep-edge/data-var-mapping)。

**Adobe Experience Platform：**

* 自定义元数据字段必须定义为XDM架构中的自定义字段（例如，`_mycompany`），并且它们可以在AEP中作为拼合字段存储和查询

  ![XDM架构中的自定义字段定义](assets/custom_metadata.png)
* 对于报告和查询，自定义元数据在`xdm.mediaReporting.customMetadata`下可用，并且也作为顶级拼合字段。 使用最适合您的用例的任何一个。
* 可用于区段、Journey Orchestration和Real-Time CDP激活

## 行为

* 所有自定义元数据值必须是&#x200B;**字符串**。 发送之前转换数字和布尔值。
* `sessionStart`元数据在整个会话中持续存在；更新需要新会话
* 每个`adStart`和`chapterStart`事件都可以携带不同的自定义元数据
* 存在标准字段时，首选标准XDM字段(`sessionDetails`、`advertisingDetails`、`chapterDetails`)而不是自定义元数据

>[!MORELIKETHIS]
>
>* [媒体收集API自定义元数据支持](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
>* [媒体收集详细信息数据类型](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-collection-details)
>* [Adobe Experience Platform Edge Network的数据变量映射](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/aep-edge/data-var-mapping)

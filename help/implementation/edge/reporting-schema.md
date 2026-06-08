---
title: XDM报告架构
description: 了解哪些Media Edge API事件在Adobe Experience Platform中生成Experience事件，以及如何使用mediaReporting XDM架构验证您的实施。
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85eid: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 763
ht-degree: 4%

---


# XDM报告架构

使用Adobe Experience Platform Edge Network发送媒体跟踪事件时，Media Analytics后端会处理这些事件，并将计算后的Experience事件写入Platform数据集。 了解哪些事件可到达Platform以及后端为您计算的内容，可帮助您验证实施并在Customer Journey Analytics或Adobe Analytics中构建准确的报告。

收集和报表管道的不同部分使用了两个不同的XDM架构：

| 架构 | 命名空间 | 方向 | 用途 |
|---|---|---|---|
| 媒体收集 | `xdm.mediaCollection` | →客户端 | 播放器为每个跟踪事件发送的内容。 由[变量](/help/implementation/variables/)使用。 |
| 媒体报告 | `xdm.mediaReporting` | Adobe → Platform | 后端在处理之后写入数据集的内容。 由[维度](/help/reporting/dimensions/overview.md)和[量度](/help/reporting/metrics/overview.md)使用。 |

`mediaReporting`中存在但`mediaCollection`有效负载中不存在的字段是从会话中的完整事件序列派生的。 您从不发送这些字段；Adobe会生成它们。

## 写入Platform数据集的事件

在12种可跟踪的事件类型中，只有5种会生成将单个体验事件写入数据集的操作：

| 事件类型 | 包含在数据集中 | 注释 |
|---|---|---|
| [会话开始](/help/implementation/events/session/session-start.md) | 是 | 会话初始化时写入 |
| [广告开始](/help/implementation/events/ads/ad-start.md) | 是 | 在单个广告开始时写入 |
| [广告完成](/help/implementation/events/ads/ad-complete.md) | 是 | 在广告播放到完成时写入 |
| [章节结束](/help/implementation/events/chapters/chapter-complete.md) | 是 | 在章节播放到完成时写入 |
| [会话完成](/help/implementation/events/session/session-complete.md) | 是 | 会话结束时写入；最丰富的计算字段集 |
| [播放](/help/implementation/events/playback/play.md) | 否 | 用于计算`timePlayed` |
| [暂停开始](/help/implementation/events/playback/pause-start.md) | 否 | 用于计算`pauseCount`和`pauseTime` |
| [Ping](/help/implementation/events/playback/ping.md) | 否 | 心率；用于检测会话不活动 |
| [缓冲开始](/help/implementation/events/playback/buffer-start.md) | 否 | 用于计算QoE缓冲量度 |
| [比特率更改](/help/implementation/events/playback/bitrate-change.md) | 否 | 用于计算QoE比特率量度 |
| [状态开始](/help/implementation/events/player-state/state-start.md) | 否 | 用于计算播放器状态量度 |
| [错误](/help/implementation/events/error.md) | 否 | 用于计算QoE中的`errorCount` |

## 后端计算字段

以下字段显示在`mediaReporting`有效负载中，但绝不是集合有效负载的一部分。 后端从完整的事件序列派生它们。

**会话级别** （出现在`sessionComplete`）：

| 字段 | 描述 |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | 已播放主内容的总秒数，不包括广告 |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | 经过的总秒数，包括广告 |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | 删除了重复项秒数。 多次查看的间隔只计算一次 |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed`除以内容长度 |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | 估计的并发流 |
| `xdm.mediaReporting.sessionDetails.adCount` | 开始的广告数 |
| `xdm.mediaReporting.sessionDetails.chapterCount` | 开始的章节数量 |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | 暂停频率和暂停总持续时间 |
| `xdm.mediaReporting.sessionDetails.hasProgress10` ... `xdm.mediaReporting.sessionDetails.hasProgress95` | 进度里程碑标记(10%、25%、50%、75%、95%) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | 是否查看了至少一个内容帧 |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | 完成和开始标记 |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | 上次ping和会话关闭之间的时间 |
| `xdm.mediaReporting.sessionDetails.segment` | 内容区段括号（例如，`[0-1]`） |

**广告级别** （出现在`adComplete`）：

| 字段 | 描述 |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | 广告内容播放的秒数 |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | 广告是否播放到结束 |

**章节级别** （出现在`chapterComplete`上）：

| 字段 | 描述 |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | 章节内容播放的秒数 |
| `xdm.mediaReporting.chapterDetails.isCompleted` | 章节是否播放到结束 |
| `xdm.mediaReporting.chapterDetails.isStarted` | 章节是否开始 |

**QoE** （聚合于`sessionComplete`）：

| 字段 | 描述 |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | 整个会话的平均比特率 |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | 分段平均比特率范围 |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | 比特率更改的次数 |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | 错误数 |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | 丢帧总数 |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | 播放器错误代码数组 |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | 是否发生任何错误 |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | 是否发生丢帧 |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | 是否发生比特率更改 |

## 下载的内容

对于使用[下载的终结点](/help/use-cases/track-downloaded-content.md)跟踪的会话，后端在`sessionStart`报告事件上自动将`xdm.mediaReporting.sessionDetails.isDownloaded`设置为`true`。 已下载会话的所有其他报表事件遵循与实时会话相同的架构。 在CJA或Adobe Analytics中使用此字段来过滤或划分下载的播放。

有关集合实现详细信息，请参阅Media Edge API引用中的[已下载端点](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/)。

## 验证您的实施

通过Media Edge API发送事件后，使用以下方法之一验证数据是否正确着陆：

**Adobe Experience Platform数据集预览**

1. 在[CX Enterprise](https://experience.adobe.com)中，导航到&#x200B;**[!UICONTROL 数据集]**&#x200B;并选择您的流媒体数据集。
2. 选择&#x200B;**[!UICONTROL 预览数据集]**&#x200B;以查看最近摄取的体验事件。
3. 确认`eventType`值（如`media.sessionStart`和`media.sessionComplete`）显示填充了`mediaReporting`字段。

**Customer Journey Analytics数据集检查**

1. 在CJA中，打开与您的流媒体数据集关联的连接。
2. 选择&#x200B;**添加数据集**&#x200B;并检查架构以确认`mediaReporting`字段映射到预期的维度和量度。

**Adobe Analytics处理规则（如果使用Analytics目标）**

对于通过Adobe Analytics源连接器接收数据的Analytics报表包，您可以使用处理规则将`mediaReporting`上下文数据变量映射到自定义prop或eVar。 `isDownloaded`标记可用作`a.media.downloaded`。

## XDM有效负载示例

以下示例显示写入Platform数据集的每个报表事件的完整`mediaReporting` XDM结构。 `_{tenantName}`属性表示您组织的任何自定义字段的租户命名空间。

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart（下载的内容）

使用[下载的终结点](/help/use-cases/track-downloaded-content.md)跟踪的会话遵循相同的报告架构，其中一个关键差异： `sessionStart`报告事件中的`xdm.mediaReporting.sessionDetails.isDownloaded`设置为`true`。 所有其他事件类型与上面的实时内容示例相同。

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++

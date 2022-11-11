---
title: 了解媒体跟踪时间轴
description: 深入了解播放头时间轴和相应用户的操作。 了解每个操作的详细信息及其随附的请求。
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
exl-id: 16b15e03-5581-471f-ab0c-077189dd32d6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 98%

---

# 时间线 1 — 查看到内容的结尾{#timeline-view-to-end-of-content}

## VOD、前置广告、暂停、缓冲、观看到内容的结尾

下图说明了播放头时间轴和用户操作的相应时间轴。每项操作及其随附请求的详细信息如下所述。

![API内容](assets/va_api_content.png)

![API操作](assets/va_api_actions.png)

## 操作详细信息

### 操作 1 - 开始会话 {#Action-1}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 按下“自动播放”或“播放”按钮，将开始加载视频。 | 0 | 0 | `/api/v1/sessions` |

此调用表示&#x200B;_用户播放视频的意图_。

它会向客户端返回一个会话 ID (`{sid}`)，用于标识会话中的所有后续跟踪调用。播放器状态不是“正在播放”，而是“正在启动”。

[强制会话参数](../mc-api-ref/mc-api-sessions-req.md)必须包含在请求正文中的 `params` 映射中。

在后端，此调用会生成一个 Adobe Analytics 启动调用。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"sessionStart, params" {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### 操作 2 - Ping 计时器启动 {#Action-2}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序启动 Ping 事件计时器 | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

启动应用程序的 Ping 计时器。如果有前置广告，则第一个 Ping 事件应在 1 秒后触发，否则应在 10 秒后触发。

### 操作 3 - 广告时间开始 {#Action-3}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告时间开始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

只能在广告时间期间跟踪广告。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### 操作 4 - 广告开始 {#Action-4}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告 1 开始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

开始跟踪第一个前置广告，其时长为 15 秒。包括含此 `adStart` 的自定义元数据。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement"
    },
    "customMetadata": {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

**请注意：在 AdBreakStart 和 AdStart 事件之间不应有任何额外的播放事件。**

### 操作 5 - 广告 Ping {#Action-5}

#### 操作 5.1 - 广告 Ping 1 {#Action-5-1}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 1 | 0 | `/api/v1/sessions/{sid}/events` |

在广告中，每 1 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### 操作 5.2 - 广告 Ping 2 {#Action-5-2}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 2 | 0 | `/api/v1/sessions/{sid}/events` |

在广告中，每 1 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### 操作 5.3 - 广告 Ping 3 {#Action-5-3}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 3 | 0 | `/api/v1/sessions/{sid}/events` |

在广告中，每 1 秒对后端执行一次 Ping 操作。

>[!NOTE]
>
>时间轴中的后续广告将跳过显示一秒钟 Ping 系列
>（这是为了简短起见）……

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 操作 6 - 广告结束 {#Action-6}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告 1 结束 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

跟踪第一个前置广告的结束。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### 操作 7 - 广告开始 {#Action-7}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告 2 开始 | 15 | 0 | `/api/v1/sessions/{sid}/events` |

跟踪第二个前置广告的开始，其时长为 7 秒。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 操作 8 - 广告 Ping {#Action-8}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 20 | 0 | `/api/v1/sessions/{sid}/events` |

每 1 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 操作 9 - 广告结束 {#Action-9}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告 2 结束 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

跟踪第二个前置广告的结束。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### 操作 10 - 广告时间结束 {#Action-10}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告时间结束 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

广告时间结束。在整个广告时间内，播放状态一直保持为“正在播放”。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### 操作 11 - 播放内容 {#Action-11}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪播放事件 | 22 | 0 | `/api/v1/sessions/{sid}/events` |

在 `adBreakComplete` 事件后，使用 `play` 事件将播放器置于“正在播放”状态。

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### 操作 12 - Ping {#Action-12}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 30 | 8 | `/api/v1/sessions/{sid}/events` |

每 10 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 8,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 操作 13 - 缓冲开始 {#Action-13}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 发生缓冲开始事件 | 33 | 11 | `/api/v1/sessions/{sid}/events` |

跟踪播放器向“正在缓冲”状态的转变

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    }, "eventType": "bufferStart"
}
```

### 操作 14 - 缓冲结束 {#Action-14}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 缓冲结束后，应用程序将跟踪内容的恢复 | 36 | 11 | `/api/v1/sessions/{sid}/events` |

缓冲在 3 秒后结束，因此请将播放器恢复到“正在播放”状态。您必须发送来自缓冲的另一个跟踪播放事件。**`bufferStart` 后的 `play` 调用一定会对后端进行“bufferEnd”调用**，因此不需要 `bufferEnd` 事件。

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### 操作 15 - Ping {#Action-15}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 40 | 15 | `/api/v1/sessions/{sid}/events` |

每 10 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 15,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 操作 16 - 广告时间开始 {#Action-16}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪中置广告时间开始 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

持续时间为 8 秒的中置广告：发送 `adBreakStart`。

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### 操作 17 - 广告开始 {#Action-17}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪中置广告 3 开始 | 46 | 21 | `/api/v1/sessions/{sid}/events` |

跟踪中置广告。

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### 操作 18 - 广告 Ping {#Action-18}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 50 | 21 | `/api/v1/sessions/{sid}/events` |

每 10 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 操作 19 - 广告结束 {#Action-19}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪中置广告 1 结束 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

中置广告完成。

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### 操作 20 - 广告时间结束 {#Action-20}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪中置广告时间结束 | 54 | 21 | `/api/v1/sessions/{sid}/events` |

广告时间结束。

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### 操作 21 - Ping {#Action-21}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 60 | 27 | `/api/v1/sessions/{sid}/events` |

每 10 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 27,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### 操作 22 - 暂停 {#Action-22}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 用户按下“暂停” | 64 | 31 | `/api/v1/sessions/{sid}/events` |

用户的操作将播放状态转变为“已暂停”。

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    },
    "eventType": "pauseStart"
}
```

### 操作 23 - Ping {#Action-23}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 70 | 31 | `/api/v1/sessions/{sid}/events` |

每 10 秒对后端执行一次 Ping 操作。播放器仍处于“正在缓冲”状态；用户停滞在内容的第 20 秒处。用户非常恼火...

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 操作 24 - 播放 {#Action-24}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 用户按“播放”恢复主内容 | 74 | 31 | `/api/v1/sessions/{sid}/events` |

将播放状态转变为“正在播放”。**`pauseStart` 后的 `play` 调用一定会对后端进行“resume”调用**，因此不需要 `resume` 事件。

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "play"
}
```

### 操作 25 - Ping {#Action-25}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 80 | 37 | `/api/v1/sessions/{sid}/events` |

每 10 秒对后端执行一次 Ping 操作。

```json
{
    "playerTime": {
        "playhead": 37,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### 操作 26 - 会话结束 {#Action-26}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 用户完成对内容的观看。 | 88 | 45 | `/api/v1/sessions/{sid}/events` |

将 `sessionComplete` 发送到后端，以表明用户完成了对整个内容的观看。

```json
{
    "playerTime": {
        "playhead": 45,
        "ts": "<timestamp>"
    }, "eventType": "sessionComplete"
}
```

>[!NOTE]
>
>**无搜寻事件？-** 媒体收集 API 中没有明确支持 `seekStart` 或 `seekComplete` 事件。这是因为在终端用户进行清理时，某些播放器会生成大量此类事件，而几百个用户很容易就会阻塞后端服务的网络带宽。Adobe 根据设备时间戳而不是播放头位置来计算心率持续时间，以明确支持搜寻事件。

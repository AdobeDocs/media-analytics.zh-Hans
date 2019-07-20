---
seo-title: 时间轴 2 - 用户放弃会话
title: 时间轴 2 - 用户放弃会话
uuid: 74b89e8f-ef56-4e0 c-b9 a8-40739e15 b4 cf
translation-type: tm+mt
source-git-commit: 69057b2abf7140d52b1897af3dc9d9fd01ca87ad

---


# 时间轴 2 - 用户放弃会话 {#timeline--2-user-abandons-session}

## VOD、前置广告、中置广告、用户提前放弃内容

以下示意图说明了用户操作的播放头时间线和相应的时间线。下面介绍了每个操作及其附带请求的详细信息。


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## 操作详细信息

### Action 1 - Start session {#Action-1}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 自动播放或按“播放”按钮 | 0 | 0 | `/api/v1/sessions` |

**实施详细信息**

此调用表示&#x200B;_用户播放视频的意图_。It returns a Session ID ( `{sid}` ) to the client that is used to identify all subsequent tracking calls within the session. 播放器状态不是“正在播放”，而是“正在启动”。[强制会话参数](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md)必须包含在请求正文中的 `params` 映射中。在后端，此调用会生成一个 Adobe Analytics 启动调用。

**请求主体示例**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Action 2 - Ping timer start {#Action-2}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序启动 Ping 时间计时器 | 0 | 0 |  |

**实施详细信息**

启动应用程序的ping定时器。然后，首次ping事件应在有前置广告时触发秒，否则为10秒。

### Action 3 - Ad break start {#Action-3}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告时间开始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

必须跟踪前置广告。只能在广告时间期间跟踪广告。

**请求主体示例**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Action 4 - Ad start {#Action-4}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告 #1 开始 | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

一个时长为 12 秒的广告开始。

**请求主体示例**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Action 5 - Ad pings {#Action-5}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

每秒ping后端。(没有显示随后的广告转换，因为很简单。)

**请求主体示例**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 6 - Ad complete {#Action-6}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告 #1 完成 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

第一个前置广告结束。

**请求主体示例**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Action 7 - Ad break complete {#Action-7}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪前置广告时间完成 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

广告时间结束。在整个广告时间内，播放器一直处于“正在播放”状态。

**请求主体示例**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Action 8 - Play content {#Action-8}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪播放事件 | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

将播放器转变为“正在播放”状态，开始跟踪内容播放的开始。

**请求主体示例**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play,
    qoeData: { bitrate: 10000 }
}
```

### Action 9 - Ping {#Action-9}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

每 10 秒对后端执行一次 Ping 操作。

**请求主体示例**

```
{
    playerTime: {
        playhead: 8ß,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 10 - Ping {#Action-10}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

每 10 秒对后端执行一次 Ping 操作。

**请求主体示例**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 11 - Error {#Action-11}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 发生错误，应用程序发送错误消息。 | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**


**请求主体示例**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:error
}
```

### Action 12 - Play content {#Action-12}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序从错误中恢复，用户按下“播放” | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**



**请求主体示例**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:play, qoeData: { bitrate: 10000 }
}
```

### Action 13 - Ping {#Action-13}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 应用程序发送 Ping 事件 | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

每 10 秒对后端执行一次 Ping 操作。

**请求主体示例**

```
{
    playerTime: {
        playhead: 28,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Action 14 - Ad break start {#Action-14}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪中置广告时间开始 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

持续时间为 8 秒的中置广告：发送 `adBreakStart`。

**请求主体示例**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Action 15 - Ad start {#Action-15}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 跟踪中置广告 #1 开始 | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

跟踪中置广告。

**请求主体示例**

```
{
    playerTime: { playhead: 33, ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 16 - Close app {#Action-16}

| 操作 | 操作时间轴（秒） | 播放头位置（秒） | 客户端请求 |
| --- | :---: | :---: | --- |
| 用户关闭应用程序。该应用程序确定用户已放弃观看并且没有返回到此会话。 | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**实施详细信息**

将 `sessionEnd` 发送到 VA 后端，以指示应立即关闭会话，无需进一步处理。

**请求主体示例**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:sessionEnd
}
```



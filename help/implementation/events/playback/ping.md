---
title: Ping
description: 发送心跳以保持媒体会话活动状态并定期跟踪播放进度。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# Ping

Ping事件是一种心率，用于保持会话活动状态并跟踪播放进度。 在整个播放过程中，通过计时器发送该报告。 在Mobile SDK上，Ping会自动发送；在所有其他平台上，均必须在指定的时间间隔内手动发送。

* **主内容**：开始播放后第一个ping 10秒，之后每10秒一次
* **广告内容**：在广告跟踪期间每1秒一次

请勿在Ping请求正文中包含`params`对象。

* **先决条件**： [会话开始](../session/session-start.md)
* **关联的量度**：无

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

计划与`eventType: "media.ping"`的定期`sendEvent`调用。 每次调用时将`playhead`更新到当前播放位置：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

>[!TAB iOS]

Mobile SDK会自动发送Ping事件。 不需要显式调用。

>[!TAB Android]

Mobile SDK会自动发送Ping事件。 不需要显式调用。

>[!TAB Roku Edge]

计划与`eventType: "media.ping"`的定期`sendMediaEvent`调用。 每次调用时将`playhead`更新到当前播放位置：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

>[!TAB Media Edge API]

在计时器上调用[ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/)终结点。 Adobe建议在主播放开始后第10秒执行首次ping操作，在此之后每10秒执行一次，在广告跟踪期间每1秒执行一次：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK会自动发送Ping事件。 不需要显式调用。

>[!TAB Chromecast]

Chromecast SDK会自动发送Ping事件。 不需要显式调用。

>[!TAB Roku 2.x]

只要您在事件循环中调用`processMediaMessages`，Media SDK就会自动发送Ping事件。 更新播放头，以便每次ping均报告当前位置：

```brightscript
ADBMobile().mediaUpdatePlayhead(10)
```

>[!TAB 媒体收集API]

向计时器上的[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`ping`个POST。 不包括`params`对象：

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```

>[!ENDTABS]

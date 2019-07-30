---
seo-title: 会话响应缓慢时对事件进行排队
title: 会话响应缓慢时对事件进行排队
uuid: 39ea59d9-89d3-4087a806-48a43ef0c98
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 会话响应缓慢时对事件进行排队{#queueing-events-when-sessions-response-is-slow}

媒体收集 API 是 RESTful：即，您发出 HTTP 请求并等待响应。This is an important point only for when you make a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) to obtain a Session ID at the beginning of video playback. 这很重要，因为所有后续跟踪调用都需要使用会话ID。

It is possible that your player may fire events _before the Sessions response returns_ (with the Session ID parameter) from the backend. If this occurs, your app must queue any tracking events that arrive between the [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) and its response. When the Sessions response arrives, you should first process any queued [events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md), then you can start processing _live_ events with the [Events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) calls.

>[!NOTE]
>
>[事件请求](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)不会将数据返回给 HTTP 响应代码之外的客户端。

在接收会话 ID 之前，请查看发行版中的引用播放器，以找到一种处理事件的方法。例如：

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**处理所有排队的事件 -**&#x200B;引用播放器处理排队的事件，如下所示：

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

在发生跟踪事件时继续进行处理。

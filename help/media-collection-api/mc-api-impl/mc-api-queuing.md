---
title: 会话响应缓慢时对事件进行排队
description: 了解在播放器触发事件后返回会话ID时要执行的操作。
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 92%

---

# 会话响应缓慢时对事件进行排队{#queueing-events-when-sessions-response-is-slow}

媒体收集 API 是 RESTful：即，您发出 HTTP 请求并等待响应。只有在视频播放开始时发出[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)以获取会话 ID 时，它才会发挥重要作用。这一点很重要，因为所有后续跟踪调用都需要会话 ID。

播放器可能会在从后端“返回会话响应之前”__（通过会话 ID 参数）触发事件。如果发生这种情况，应用程序必须对在发出[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)到获取其响应期间到达的任何跟踪事件进行排队。当会话响应到达时，您应该首先处理所有排队的[事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)，随后可以使用[事件](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)调用开始处理&#x200B;_实时_&#x200B;事件。

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

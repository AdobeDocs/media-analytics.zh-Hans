---
seo-title: 发送 Ping 事件
title: 发送 Ping 事件
uuid: c92c1a92-3af6-4444-9e42-ffb8 f6 c94 b33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# 发送 Ping 事件{#sending-ping-events}

**对于主内容，您必须每 10 秒触发一次 Ping 事件，从播放 10 秒之后开始，而不考虑已发送的其他 API 事件。For Ad tracking, you must fire ping events every 1 second.**

ping事件是媒体分析的“心跳”。Ping 调用所需的唯一参数是 `eventType: ping` 以及 `playerTime` 对象（播放头位置和时间戳）。

以下代码片段显示了一种为主内容实施定时 Ping 机制的方法（10 秒间隔）：

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```


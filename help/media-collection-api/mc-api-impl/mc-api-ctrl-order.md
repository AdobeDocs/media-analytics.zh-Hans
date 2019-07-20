---
seo-title: 控制事件的顺序
title: 控制事件的顺序
uuid: 007fcc6-be72-4b79-826d-588c957 cf15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# 控制事件的顺序{#controlling-the-order-of-events}

由于Media Collection API是RESTful，且视频跟踪是一个高度时间依赖的操作、一个实现程序，因此可能会担心到达后端的Media Collection API跟踪调用的顺序。后端“确实”**&#x200B;会尝试根据 `playerTime` 对象中提供的时间戳对事件进行排队和重新排序。但是，这种功能有一定的限制。当前，如果乱序执行的调用之间的延迟超过了一秒，则重新排序可能会失败。可能会在将来的更新中对这种“可接受的延迟时间”进行优化和/或配置。

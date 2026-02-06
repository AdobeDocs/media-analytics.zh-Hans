---
title: 跟踪应用程序操作
description: 应用程序操作是指在您要测量的应用程序中发生的事件。
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 100%

---

# 跟踪应用程序操作{#track-app-actions}

操作是指在您要测量的应用程序中发生的事件。

每个操作均具有一个或多个对应的量度，每当发生事件时，这些量度的数量都会递增。例如，您可为每次新订阅，或者每当评定内容或完成某个级别时，发送一个 `trackAction` 调用。

系统不会自动跟踪操作，因此在发生要跟踪的事件时调用 `trackAction`，并将操作映射到一个自定义事件。

1. 在发生要跟踪的事件时，调用 `trackAction`。

   * **Roku:**

     ```js
     ADBMobile().trackAction("myapp.ActionName", {})
     ```

   * **Chromecast:**

     ```js
     ADBMobile.analytics.trackAction("myapp.ActionName", {});
     ```

1. 将操作映射到一个自定义事件。

   * **Roku:**

     ```js
     dictionary = {} 
     dictionary["myapp.social.SocialSource"] = "Twitter"  
     ADBMobile().trackAction("myapp.SocialShare", dictionary)
     ```

   * **Chromecast:**

     ```js
     var dictionary = {}; 
     dictionary["myapp.social.SocialSource"] = "Twitter"; 
     ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
     ```

您还可以通过每个跟踪操作调用发送其他上下文数据。

---
seo-title: 跟踪应用程序操作
title: 跟踪应用程序操作
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# 跟踪应用程序操作{#track-app-actions}

操作是指在您要测量的应用程序中发生的事件。

每个操作均具有一个或多个对应的量度，每当发生事件时，这些量度的数量都会递增。For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

系统不会自动跟踪操作，因此在发生要跟踪的事件时调用 `trackAction`，并将操作映射到一个自定义事件。

1. When an event that you want to track occurs, call `trackAction`.

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


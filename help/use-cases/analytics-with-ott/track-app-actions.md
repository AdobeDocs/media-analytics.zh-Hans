---
title: 跟踪应用程序操作
description: 应用程序操作是指在您要测量的应用程序中发生的事件。
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ahqWp2yjs-zkd9dTRWTkE7b6KE-WpwVR0OH9vCqTPjI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 100%

---

# 跟踪应用程序操作{#track-app-actions}

操作是指在您要测量的应用程序中发生的事件。

每个操作均具有一个或多个对应的量度，每当发生事件时，这些量度的数量都会递增。 例如，您可为每次新订阅，或者每当评定内容或完成某个级别时，发送一个 `trackAction` 调用。

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

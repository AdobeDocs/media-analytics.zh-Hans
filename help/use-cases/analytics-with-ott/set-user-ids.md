---
title: 设置用户 ID
description: 用于设置用户 ID 的 API，用户 ID 用作唯一客户标识符。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Media Analytics, API"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 100%

---

# 设置用户 ID{#set-user-ids}

用户 ID 是应用程序为用户定义的唯一自定义访客标识符。

在 ADBMobile SDK 上设置并获取唯一的用户 ID，如下所示：

* **已设置:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **获取：**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```

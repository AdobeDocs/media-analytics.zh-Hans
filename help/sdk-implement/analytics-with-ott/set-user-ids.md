---
title: 设置用户 ID
description: 用于设置用户ID的API，将哪台服务器设置为唯一客户标识符。
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 设置用户 ID{#set-user-ids}

用户 ID 是应用程序为用户定义的唯一自定义访客标识符。

在 ADBMobile SDK 上设置并获取唯一的用户 ID，如下所示：

* **设置：**

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

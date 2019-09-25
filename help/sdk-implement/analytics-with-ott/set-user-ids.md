---
seo-title: 设置用户 ID
title: 设置用户 ID
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

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

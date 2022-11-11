---
title: 关于流媒体分析和安全
description: 了解流媒体分析和安全性
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---



# 安全性 {#security}

在Adobe中，我们十分重视您的数字资产的安全性和隐私性。 从将安全性严格整合到内部软件开发流程和工具，到跨职能的事件响应团队，我们都努力做到主动和灵活。此外，我们与合作伙伴、研究人员和其他行业组织的协作工作有助于我们了解最新的威胁和安全最佳实践。 我们的主动预防性方法允许我们持续将安全性构建到我们提供的产品和服务中。


## 传输层安全性 {#transport-layer-security}

**传输层安全通知 —** Adobe有安全合规标准，要求终止使用旧版安全协议。 为了继续满足不断演变的安全协议标准，Adobe正在转向使用传输层安全性(TLS)1.2，以便使用最新且最安全的版本。 从 2019 年 2 月 20 日起，Adobe 将仅支持 TLS 1.1 或更高版本。伴随这项变化，对于使用部署了 TLS 1.0 的较旧设备或 Web 浏览器的最终用户，Adobe 将不再收集他们的数据。迁移到 TLS 1.2 可提高安全性。您应务必了解具体细节，并且针对更改做出规划以实现顺利迁移。

>[!NOTE]
>
>TLS 是目前最广泛部署的安全协议，适用于 Web 浏览器和其他需要通过网络安全交换数据的应用程序。

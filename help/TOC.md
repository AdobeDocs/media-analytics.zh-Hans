---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics for Streaming Media
breadcrumb-title: Media Analytics 指南
user-guide-description: 实施 Adobe Analytics for Streaming Media。包括 Media SDK 和 Media Collection API。
sub-product: media analytics
source-git-commit: a26e4e283646e5ceb352f357789748f376f5c747
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 96%

---


# Adobe Analytics for Streaming Media {#using}

+ [流媒体 Analytics 指南](media-overview.md)
+ 发行说明 {#release-notes}
   + [流媒体发行说明](additional-resources/release-notes.md)
+ 快速入门 {#getting-started}
   + [概述](getting-started/getting-started.md)
   + [先决条件](getting-started/prereqs.md)
   + [支持的设备](getting-started/supported-devices.md)
   + [流媒体文档](getting-started/implementation-documentation.md)
   + [SDK、库和扩展](getting-started/download-sdks.md)
   + 终止支持 {#end-of-support}
      + [Media Analytics Mobile SDK 终止支持](additional-resources/end-of-support-faqs.md)
      + 旧版 - 从独立媒体 SDK 迁移到 Launch {#sdk-to-launch}
         + [概述](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - 从 Media SDK 到 Launch ](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - 从 Media SDK 到 Launch ](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - 从 Media SDK 到 Launch ](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ 实施 {#implementation}
   + [实施概述](implementation/overview.md)
   + [Media SDK 概述](/help/implementation/media-sdk-overview.md)
   + Edge实施（推荐） {#edge-recommended}
      + Media Edge SDK/扩展 {#media-edge-sdk}
         + [Media Edge SDK/扩展设置](/help/implementation/edge/implementation-edge.md)
         + [Media Edge Mobile SDK](/help/implementation/edge/edge-mobile-sdk.md)
      + [Media Edge API](/help/implementation/edge/implementation-edge-api.md)
   + 仅限Adobe Analytics的实施 {#analytics-only}
      + Media SDK/扩展 {#media-sdk}
         + [JavaScript Web SDK](implementation/media-sdk/setup/web-implementation.md)
         + [Media Analytics扩展](implementation/media-sdk/setup/web-implementation-tags.md)
         + [Mobile SDK](implementation/media-sdk/setup/mobile-implementation.md)
         + OTT SDK {#ott-setup}
            + [安装 Chromecast SDK](implementation/media-sdk/setup/set-up-chromecast.md)
            + [安装 Roku SDK](implementation/media-sdk/setup/set-up-roku.md)
      + 媒体收集 API - 实施 {#streaming-media-apis}
         + [媒体收集](implementation/media-collection-api/mc-api-overview.md)
         + [API 快速入门](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [会话请求](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [事件请求](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [请求参数](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [事件类型和描述](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + 实施 API {#mc-api-impl}
            + [在播放器中设置 HTTP 请求类型](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [获取会话 ID](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [实施事件请求](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [JSON 验证架构](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [验证事件请求](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [发送 Ping 事件](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [发送 QoE 数据](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [自定义元数据支持](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [超时情况](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [控制事件的顺序](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [会话响应缓慢时对事件进行排队](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + 变量 {#variables}
      + [流媒体参数](implementation/variables/audio-video-parameters.md)
      + [广告参数](implementation/variables/ad-parameters.md)
      + [章节参数](implementation/variables/chapter-parameters.md)
      + [播放器状态参数](implementation/variables/player-state-parameters.md)
      + [质量参数](implementation/variables/quality-parameters.md)
      + [计算指标](implementation/variables/calculated-metrics.md)
+ 报告 {#media-reports}
   + [媒体报表启用](reporting/media-reports-enable.md)
   + [关于区段](reporting/segments.md)
   + 媒体默认报表 {#media-default-reports}
      + [默认报表概述](reporting/reports-and-analytics/default-reports-overview.md)
      + [媒体概述](reporting/reports-and-analytics/media-reports-overview.md)
      + [媒体详细信息](reporting/reports-and-analytics/media-reports-detail.md)
      + [“媒体时段”报告](reporting/reports-and-analytics/media-reports-daypart.md)
      + [“媒体并行查看者”报告](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + 媒体工作区面板 {#media-workspace-panels}
      + [“媒体平均受众访问分钟数”面板](reporting/workspace/average-minute-audience.md)
      + [“媒体并行查看者”面板](reporting/workspace/media-concurrent-viewers-overview.md)
      + [“Media Playback 耗时”面板](reporting/workspace/media-playback-time-spent.md)
   + [媒体工作区模板](reporting/workspace/media-workspace-templates.md)
   + [通过 API 获取并行查看者数据](reporting/reports-and-analytics/get-concurrent-json20.md)
   + [通过 API 获取 Media Playback 耗时数据](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ 用例 {#media-use-cases}
   + [Media SDK 用例](use-cases/cookbook/sdk-cookbook-overview.md)
   + 播放器状态跟踪 {#player-state-tracking}
      + [概述](use-cases/player-state-tracking/player-state-overview.md)
      + [标准状态和自定义状态](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [实施与报表](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [多个播放器状态跟踪](use-cases/player-state-tracking/multiple-player-states.md)
      + [播放器状态跟踪示例](use-cases/player-state-tracking/player-state-examples.md)
   + [跟踪离线下载的内容](use-cases/track-downloaded-content.md)
   + [Federated Analytics](use-cases/federated-analytics.md)
   + [处理播放期间的应用程序中断](use-cases/cookbook/app-interrupts.md)
   + [媒体流归因](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [恢复不活动的会话](use-cases/cookbook/resuming-inactive.md)
   + [Roku - SceneGraph 中的跟踪](use-cases/cookbook/sdk-track-scenegraph.md)
   + [处理广告之间的间隔](use-cases/cookbook/fix-ad-play-ad.md)
   + 时间线 {#timelines}
      + [章节开始和结束](use-cases/timelines/chapter-start-end.md)
      + [查看到内容结束](use-cases/timelines/view-to-end-of-content.md)
      + [放弃会话](use-cases/timelines/user-abandons-session.md)
   + 在 OTT 应用程序中使用 Analytics {#analytics-with-ott}
      + [跟踪应用程序状态](use-cases/analytics-with-ott/track-app-states.md)
      + [跟踪应用程序操作](use-cases/analytics-with-ott/track-app-actions.md)
      + [设置用户 ID](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT 和 Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT 和 Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ 跟踪 {#tracking}
   + 跟踪 {#track-av-playback}
      + [概述](use-cases/track-av-playback/track-core-overview.md)
      + 跟踪核心流媒体播放{#track-core}
         + [在 JavaScript 3.x 中跟踪核心播放](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [在 Chromecast 中跟踪核心播放](use-cases/track-av-playback/track-core/track-core-chromecast.md)
         + [在 Roku 中跟踪核心播放](use-cases/track-av-playback/track-core/track-core-roku.md)
      + 跟踪缓冲 {#track-buffering}
         + [在 JavaScript 3.x 中跟踪缓冲](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [在 Chromecast 中跟踪缓冲](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [在 Roku 中跟踪缓冲](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
      + 跟踪搜寻 {#track-seeking}
         + [在 JavaScript 3.x 中跟踪搜寻](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [在 Chromecast 中跟踪搜寻](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [在 Roku 中跟踪搜寻](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
      + 实施标准元数据 {#impl-std-metadata}
         + [在 JavaScript 3.x 中实施标准元数据](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [在 Chromecast 中实施标准元数据](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [标准元数据参数 — Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [在 Roku 中实施标准元数据](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [标准元数据参数 — Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
      + 跟踪广告 {#track-ads}
         + [概述](use-cases/track-ads/track-ads-overview.md)
         + [在 JavaScript 3.x 中跟踪广告](use-cases/track-ads/track-ads-js/track-ads-js3.md)
         + [在 Chromecast 中跟踪广告](use-cases/track-ads/track-ads-chromecast.md)
         + [在 Roku 中跟踪广告](use-cases/track-ads/track-ads-roku.md)
         + 实施标准广告元数据 {#impl-std-ad-metadata}
            + [在 JavaScript 3.x 中实施标准广告元数据](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
            + [在 Roku 中实施标准广告元数据](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
      + 跟踪章节和区段 {#track-chapters}
         + [概述](use-cases/track-chapters/track-chapters-overview.md)
         + [在 JavaScript 3.x 中跟踪章节和区段](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
         + [在 Chromecast 中跟踪章节和区段](use-cases/track-chapters/track-chapters-chromecast.md)
         + [在 Roku 中跟踪章节和区段](use-cases/track-chapters/track-chapters-roku.md)
      + 跟踪体验质量 {#track-qos}
         + [概述](use-cases/track-qos/track-qos-overview.md)
         + [在 JavaScript 3.x 中跟踪体验质量](use-cases/track-qos/track-qos-js/track-qos-js3.md)
         + [在 Chromecast 中跟踪体验质量](use-cases/track-qos/track-qos-chromecast.md)
         + [在 Roku 中跟踪体验质量](use-cases/track-qos/track-qos-roku.md)
      + 跟踪错误 {#track-errors}
         + [概述](use-cases/track-errors/track-errors-overview.md)
         + [在 JavaScript 3.x 中跟踪错误](use-cases/track-errors/track-errors-js/track-errors-js3.md)
         + [在 Chromecast 中跟踪错误](use-cases/track-errors/track-errors-chromecast.md)
         + [在 Roku 中跟踪错误](use-cases/track-errors/track-errors-roku.md)
+ 隐私和安全性 {#streaming-media-privacy}
   + [选择禁用和隐私设置](privacy/opt-out-privacy.md)
   + [安全性](privacy/security.md)
+ 旧版实施 {#legacy-implementations}
   + [旧版 - 概述](legacy/setup/legacy-setup-overview.md)
   + [旧版 - 下载 SDK](legacy/legacy-download-sdks.md)
   + 旧版 – Media SDK{#legacy-media-sdks}
      + [旧版 - Media SDK 概述](legacy/media-sdk/setup/setup-overview.md)
      + [设置 Android](legacy/media-sdk/setup/set-up-android.md)
      + [设置 iOS](legacy/media-sdk/setup/set-up-ios.md)
      + 设置 JavaScript {#setup-javascript}
         + [设置 JavaScript 3.x](legacy/media-sdk/setup/setup-javascript/set-up-js-3.md)
   + [有关心跳测量](legacy/heartbeat-measurement.md)
   + [Adobe Primetime 和 Streaming Media Analytics](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Adobe 受众管理启用](legacy/intro-to-ava/am-enablement.md)
   + [自定义链接实施](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + 旧版里程碑跟踪 {#legacy-milestone-tracking}
      + [旧版里程碑跟踪](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [将里程碑迁移到 VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [将里程碑迁移到 CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + 验证 {#validation}
      + [验证概述](legacy/validation/validation-overview.md)
      + [测试 1：标准播放](legacy/validation/test1-standard-playback.md)
      + [测试 2：媒体中断](legacy/validation/test2-media-interrupt.md)
      + [测试调用详细信息](legacy/validation/test-call-details.md)
      + [心跳参数描述](legacy/validation/heartbeat-params.md)
      + 调试 {#debugging}
         + [SDK 调试](legacy/validation/debugging/sdk-debugging.md)
   + [旧版迁移：VHL 1.x 到 VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [设置 JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [代码对比 v1.x 到 v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [跟踪 API 1x 到 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [旧版 – AVA 简介](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [客户端路径](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + 旧版跟踪 {#track-av-playback}
      + [在 Android 中跟踪核心播放](use-cases/track-av-playback/track-core/track-core-android.md)
      + [在 iOS 中跟踪核心播放](use-cases/track-av-playback/track-core/track-core-ios.md)
      + 在 JavaScript 中跟踪核心播放 {#track-core-javascript}
         + [在 JavaScript 2.x 中跟踪核心播放](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [在 Android 中跟踪缓冲](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [在 iOS 中跟踪缓冲](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + 在 JavaScript 中跟踪缓冲 {#track-buffering-js}
            + [在 JavaScript 2.x 中跟踪缓冲](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [在 Android 中跟踪搜寻](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [在 iOS 中跟踪搜寻](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + 在 JavaScript 中跟踪搜寻 {#track-seeking-js}
            + [在 JavaScript 2.x 中跟踪搜寻](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [在 Android 中实施标准元数据](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [在 iOS 中实施标准元数据](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS 元数据键](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + 在 JavaScript 中实施标准元数据 {#impl-std-md-js}
            + [在 JavaScript 2.x 中实施标准元数据](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + 跟踪广告 {#track-ads}
         + [在 Android 中跟踪广告](use-cases/track-ads/track-ads-android.md)
         + [在 iOS 中跟踪广告](use-cases/track-ads/track-ads-ios.md)
         + 在 JavaScript 中跟踪广告 {#track-ads-js}
            + [在 JavaScript 2.x 中跟踪广告](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [在 Android 中实施标准广告元数据](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [在 iOS 中实施标准广告元数据](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + 在 JavaScript 中实施标准广告元数据 {#impl-std-ad-md-js}
               + [在 JavaScript 2.x 中实施标准广告元数据](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + 跟踪章节和区段 {#track-chapters}
         + [在 Android 中跟踪章节和区段](use-cases/track-chapters/track-chapters-android.md)
         + [在 iOS 中跟踪章节和区段](use-cases/track-chapters/track-chapters-ios.md)
         + 在 JavaScript 中跟踪章节和区段 {#track-chapters-js}
            + [在 JavaScript 2.x 中跟踪章节和区段](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [在 Android 中跟踪体验质量](use-cases/track-qos/track-qos-android.md)
         + [在 iOS 中跟踪体验质量](use-cases/track-qos/track-qos-ios.md)
         + 在 JavaScript 中跟踪体验质量 {#track-qos-js}
            + [在 JavaScript 2.x 中跟踪体验质量](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + 跟踪错误 {#track-errors}
         + [在 Android 中跟踪错误](use-cases/track-errors/track-errors-android.md)
         + [在 iOS 中跟踪错误](use-cases/track-errors/track-errors-ios.md)
         + 在 JavaScript 中跟踪错误 {#track-errors-js}
            + [在 JavaScript 2.x 中跟踪错误](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + 跟踪场景 {#tracking-scenarios}
         + [不含广告的 VOD 播放](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [包含前置式广告的 VOD 播放](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [跳过广告的 VOD 播放](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [包含一个章节的 VOD 播放](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [跳过一个章节的 VOD 播放](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [在主内容中进行搜寻的 VOD 播放](use-cases/tracking-scenarios/vod-seeking.md)
         + [带有缓冲的 VOD 播放](use-cases/tracking-scenarios/vod-buffering.md)
         + [多个并行的 VOD 跟踪器](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [一个 VOD 跟踪器用于多个会话](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [实时主内容](use-cases/tracking-scenarios/live-main-content.md)
         + [具有连续跟踪的实时主内容](use-cases/tracking-scenarios/live-sequential.md)

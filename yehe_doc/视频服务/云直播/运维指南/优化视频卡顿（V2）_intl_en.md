![](https://main.qcloudimg.com/raw/db29f65a777b1e445b5c9c7e0e694457.png)
There are three main reasons for playback stuttering.

- **Reason 1: low upstream frame rate**
Low upstream frame rate may be a result of poor performance of the host’s mobile phone or the running of CPU-intensive apps in the background. Normally, to ensure smooth playback, the upstream frame rate must be 15 FPS or higher. Frame rate lower than 10 FPS is deemed **too low**, which will cause **all viewers** to experience stuttering. However, when the host’s video image changes little, for example, when the host is showing a static image or PowerPoint, low frame rate will not cause stuttering.
- **Reason 2: upstream congestion**
The host's mobile phone keeps pushing audio and video data during live streaming. If the phone’s upstream bandwidth is too low, the data waiting to be pushed will accumulate, causing congestion in data transfer and stuttering playback experience for **all viewers**.

 Even though **ISPs in the Chinese mainland** offer broadband packages with downstream bandwidth as high as 10 Mbps or 20 Mbps, or even 100 Mbps or 200 Mbps, upstream bandwidth remains small. In many small cities, upstream bandwidth is up to 512 Kbps, which means that a maximum of 64 KB data can be uploaded per second.
 **Wi-Fi** uses the carrier-sense multiple access and collision avoidance (CSMA/CA) strategy specified in IEEE 802.11. To put it simply, a Wi-Fi hotspot can communicate with only one phone at a time, and other phones must query if communication is possible before initiating a connection to a hotspot. Therefore, the more people using a Wi-Fi hotspot, the slower the connection is. Furthermore, Wi-Fi signals are weakened significantly when passing through walls. Among average Chinese households, few take this into consideration when designing and decorating their houses, and hosts probably pay little attention to how many walls they are apart from their routers when they stream at home.

- **Reason 3: poor downstream connection**
Poor downstream connection means slow download speed or network instability for viewers. A bitrate of 2 Mbps in live streaming means 2 Mb of data needs to be downloaded per second. Viewers will experience stuttering if their network bandwidth is low, but those with sufficient bandwidth will not.

## Checking SDK Performance Metrics
The MLVB SDK has a feedback mechanism that reports different performance metrics every 2 seconds. If you use the MLVB SDK for push, you can register a [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html) listener and get the statistics in the `onStatisticsUpdate` callback. The table below lists the metrics included in `V2TXLivePusherStatistics` and their meanings.

| Metric                | Description                    |
| :------------------------  |  :------------------------ |
| appCpu | CPU usage of the application (%) |
| systemCpu | CPU usage of the system (%) |
| width | Video width |
| height | Video height |
| fps | Frame rate (FPS) |
| audioBitrate | Audio bitrate in Kbps |
| videoBitrate | Video bitrate in Kbps |

## Fixing Low Frame Rate
### 1. How to know whether the frame rate is too low
The **V2TXLivePusherStatistics.fps** field in the [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af01be7a0bf0ed619cce63f49959ea8be) callback of `V2TXLivePusherObserver` indicates the frame rate for push. Normally, the frame rate must be 15 FPS or higher to ensure smooth playback. Viewers usually experience obvious stuttering when the push frame rate is lower than 10 FPS.

### 2. How to fix the problem
- **2.1 Monitoring `appCpu` and `systemCpu`**
You can learn about the **CPU usage of the app and system** from the **V2TXLivePusherStatistics.appCpu** and **V2TXLivePusherStatistics.systemCpu** fields in the [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af01be7a0bf0ed619cce63f49959ea8be) callback of `V2TXLivePusherObserver`. If the system CPU usage exceeds 80%, both video capturing and encoding may be affected; if it reaches 100%, it is difficult to even ensure smooth push, let alone playback experience for viewers.

- **2.2 Identifying CPU consumers**
The MLVB SDK is not the only CPU consumer in a live streaming application. Leaving on-screen comments, sending hearts, and text messaging all consume CPU. To monitor the CPU usage of the MLVB SDK only, you may use its [demo](https://intl.cloud.tencent.com/document/product/1071/38147).

- **2.3 Choosing an appropriate resolution**
High resolution does not necessarily result in high video quality. To begin with, high resolution translates into improved video quality only when the bitrate is also high. Low bitrate and high resolution usually produce lower video quality than high bitrate and low resolution. In addition, viewers may be able to sense obvious differences between a resolution of 1280 x 720 px and 960 x 540 px when watching videos full screen on PCs, but not on mobile phones, whose average screen size is only around 5 inches. High resolution increases the CPU usage of the SDK significantly. Therefore, you are advised to set video quality to **HD** using the [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02) API in `V2TXLivePusher` of the MLVB SDK. You may not get the high video quality expected by setting the resolution too high.

## Fixing Upstream Congestion
Statistics show that upstream congestion at the host end is responsible for over 80% of playback stuttering in live streaming.

###1. Informing hosts of poor network conditions
In scenarios where video quality is important, you are advised to inform the hosts of bad network conditions through UI notifications. For example, you may send this notification to hosts: **Bad network conditions. Please move closer to your router or make sure that your Wi-Fi signal does not have to pass through walls.**
For more information on how to do this, please see **Mobile Live Video Broadcasting > Basic Features > Camera Push > Event Handling**. You are advised to remind hosts to check their network conditions if your application receives the [V2TXLIVE_WARNING_NETWORK_BUSY](https://intl.cloud.tencent.com/zh/document/product/1071) event multiple times within a short period of time. Hosts are often unable to notice upstream congestion until reminded by viewers or an application message.

### 2. Using the recommended encoding settings
We recommend the following encoding settings (for more information, please see [Setting Video Quality](https://intl.cloud.tencent.com/zh/document/product/1071)). You can use the [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02) API in `V2TXLivePusher` to set the parameters.

|Scenario |`resolution` |`resolutionMode` |
| :------------------------  |  :------------------------ | :------------------------ |
|Live showroom|<li/>V2TXLiveVideoResolution960x540<li/>V2TXLiveVideoResolution1280x720 |Landscape or portrait |
|Live game streaming |V2TXLiveVideoResolution1280x720 |Landscape or portrait |
|Mic connect (primary image) |V2TXLiveVideoResolution640x360 |Landscape or portrait |
|Mic connect (small image) |V2TXLiveVideoResolution480x360 |Landscape or portrait |
|Blue-ray live streaming |V2TXLiveVideoResolution1920x1080 |Landscape or portrait |

## Fixing Player-End Issues
![](https://main.qcloudimg.com/raw/c2c88d9bbf8f72c77eb778d7f2d5e993.png)

### 1. Stuttering and latency
As shown in the figure above, both downstream network fluctuations and insufficient downstream bandwidth can result in **unfed periods** (during which the application cannot get any audio/video data for playback) in the playback process. To avoid playback stuttering, the application needs to cache video data enough to cover the unfed periods. However, caching too much data causes a new problem: **high latency**, which is undesirable for interactive scenarios. The latency could **build up** over time if not fixed, meaning that it increases as the playback continues. The capability to fix latency is a key performance indicator for players. **Latency and playback smoothness are like the two ends of a scale**. To ensure low latency, you may have to compromise network stability, which causes playback stuttering, and to ensure smooth playback, you must deal with high latency. A typical example of the latter is the introduction of a 20-30 second delay in the playback of HLS (M3U8) streams to ensure smooth playback experience.

### 2. How to fix the problem
To allow you to deliver superior playback experience without having to learn QoS control, we have developed an automatic latency control technology, which we optimized from version to version, and launched three [latency control schemes](https://intl.cloud.tencent.com/document/product/1071). You can use the [setCacheParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a8a4f8f8e220a6e4aa2a04ca3e866efcb) API in `V2TXLivePlayer` to select one of the schemes.

-  **Auto mode**: use this mode if you are not sure what scenarios you will deal with.
>? In this mode, the player adjusts latency automatically based on network conditions to minimize the latency between hosts and viewers and ensure host-viewer interaction quality while delivering smooth playback experience. By default, the player adjusts latency in the range of 1-5 seconds, which you can modify using the `setCacheParams` API.

-  **Speedy mode**: suitable for **live showroom** and other interactive scenarios that require low latency.
>? You can switch to this mode by **setting both `minTime` and `maxTime` to 1 second**. The auto and speedy modes differ only in terms of `maxTime`, whose value is generally lower in the speedy mode. This flexibility is made possible by the SDK’s automatic latency control technology, which can automatically adjust latency without causing stuttering. `maxTime` is associated with adjustment speed. The higher the `maxTime` value, the more conservative the adjustment is, and the less likely stuttering will occur.

- **Smooth mode**: suitable for **live game streaming** and other high-bitrate and high-definition scenarios.
>?
>- In this mode, the player adopts a strategy similar to the caching policy of Adobe Flash Player. When stuttering occurs, the player switches to the loading mode, and when enough data is cached, it returns to the playing mode, until the network connection fluctuates again. By default, 5 seconds of video data is cached, which you can change using the `setCacheParams` API.
>- This seemingly simple mode reduces playback stuttering by moderately increasing latency and is therefore the more reliable option for scenarios that do not require low latency.

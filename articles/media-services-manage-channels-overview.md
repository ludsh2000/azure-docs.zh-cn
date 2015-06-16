﻿<properties 
	pageTitle="管理频道和节目" 
	description="本主题介绍了如何为实时流创建媒体服务频道和节目。" 
	services="media-services" 
	documentationCenter="" 
	authors="juliako" 
	manager="dwrede" 
	editor=""/>

<tags ms.service="media-services" ms.date="03/22/2015" wacn.date="04/11/2015"/>


# 管理频道和节目

## 概述

在 Azure 媒体服务 (AMS) 中，频道实体表示用于处理实时流内容的管道。使用"节目"，你可以控制实时流中的片段的发布和存储。频道管理着节目。频道和节目的关系非常类似于传统媒体，频道具有恒定的内容流，而节目的范围限定为该频道上的一些定时事件。 

频道从输出多比特率 RTMP、平滑流（分片 MP4）的第三方编码器接收实时输入流。然后，内容能够以流形式通过一个或多个流式传输终结点传输到客户端播放应用程序，使用下列自适应流式传输协议之一：HLS、Smooth Stream、MPEG DASH、HDS。

流式传输终结点表示一个流服务，该服务可以直接将内容传递给客户端播放器应用程序，也可以传递给内容交付网络 (CDN) 以进一步分发。流式传输终结点服务的出站流可以是实时流，也可以是你的媒体服务帐户中的视频点播资产。此外，还可以通过调整流式传输保留单元来控制 StreamingEndpoint 服务处理不断增长的带宽需求的能力。建议为生产环境中的应用程序分配一个或多个流式传输保留单元。有关更多信息，请参阅[如何缩放媒体服务](/documentation/articles/media-services-manage-origins#scale_streaming_endpoints)。

### 使用本地实时编码器的实时流式传输

下图表示的是一个使用本地实时编码器的实时流式传输工作流，该实时编码器输出多比特率 RTMP 或 Smooth Streaming（分片 MP4）。当使用本地编码器时，传入的流通过流式传输终结点时不进行任何编码。

请注意，对于要发送的单比特率 RTMP 或 Smooth Streaming 实时流而言，这有效但不合意。流也将通过，但客户端应用程序将获得单比特率流。


![Live workflow][live-overview]


## 概念

有关概念的信息，请参阅[媒体服务概念](/documentation/articles/media-services-concepts#live-streaming)。 

## 基本方案

本部分介绍了在创建最基本的实时流式传输应用程序时涉及的步骤。

### 使用本地编码器提供实时流式传输媒体

1. 创建并启动频道。
1. 检索频道摄取（输入）URL。
1. 启动并配置所选的实时转码器。有关更多信息，请参阅[将第三方实时编码器与 Azure 媒体服务结合使用](https://msdn.microsoft.com/zh-CN/library/azure/dn783464.aspx)。
1. 检索频道的预览终结点，并确认你的频道正确接收实时流。
2. 创建资产并配置资产传送策略（由动态打包功能使用）。
3. 创建节目并指定使用你创建的资产。
1. 通过创建按需定位器发布与节目关联的资产。  

	确保你要从中以流形式传输内容的流式传输终结点上至少有一个流式传输保留单元。
1. 在准备好开始流式传输和存档时，启动节目。
1. 在要停止对事件进行流式传输和存档时，停止节目。
1. 删除节目（并选择性地删除资产）。 

此主题的剩余部分介绍了媒体服务频道和节目的主要组件。

## <a id="channel_input"></a>频道输入（摄取）配置

### <a id="ingest_protocols"></a>摄取流式传输协议

有效的流式传输协议选项包括：**多比特率 RTMP** 和**多比特率分片 MP4**.

- **多比特率 RTMP**。
	
	当选择了 **RTMP** 摄取流式传输协议时，会为频道创建两个摄取（输入）终结点： 
	
	- **主 URL**：指定频道的主 RTMP 摄取终结点的完全限定 URL。
	- **辅助 URL**（可选）：指定频道的辅助 RTMP 摄取终结点的完全限定 URL。 

	创建辅助 URL 的原因是提高你的摄取流的持久性和容错性并实现编码器故障转移和容错性。 
	
	- 若要提高摄取持久性和容错性，请执行以下操作：
		
		使用一个编码器向主摄取 URL 和辅助摄取 URL 发送相同的数据。大多数 RTMP 编码器（例如 Flash Media Encoder 或 Wirecast）都能够使用主 URL 和辅助 URL。
	- 若要处理编码器故障转移和容错性，请执行以下操作：
		
		使用多个编码器生成相同的数据并将其发送到主摄取 URL 和辅助摄取 URL。这种方法同时提高了摄取持久性和编码器高可用性。注意：编码器需要支持高可用性方案，并且还需要在内部在时间上是同步的（有关详细信息，请参阅你的编码器手册）。
	
	
	其他注意事项：
	
	- 	使用辅助摄取 URL 将需要额外的带宽。若要使用主/辅助摄取 URL，你需要确保你有足够的空闲 Internet 连接来将数据发送到摄取点。
	- 	当前，无法通过 SSL 摄取 RTMP。

- **多比特率分片 MP4** (Smooth Streaming)。
	
	可以通过 SSL 连接摄取实时分片 MP4 (Smooth Streaming) 内容。若要通过 SSL 进行摄取，请确保将摄取 URL 更新为 HTTPS

请注意，对于要发送的单比特率 RTMP 或 Smooth Streaming 实时流而言，这有效但不合意。流也将通过，但客户端应用程序将获得单比特率流。


当频道或其关联的节目正在运行时，无法更改输入协议。如果你需要不同的协议，应当针对每个输入协议创建单独的频道。 

### 允许的 IP 地址

你可以定义允许向此频道发布视频的 IP 地址。允许的 IP 地址可以指定为单个 IP 地址（例如 '10.0.0.1'）或指定为使用一个 IP 地址和 CIDR 子网掩码的 IP 范围（例如 '10.0.0.1/22'）或指定为使用一个 IP 地址和点分十进制子网掩码的 IP 范围（例如 '10.0.0.1(255.255.252.0)'）。 

如果未指定 IP 地址并且没有规则定义，则不会允许任何 IP 地址。若要允许任何 IP 地址，请创建一个规则并设置 0.0.0.0/0。

### 摄取 URL（终结点） 

频道提供了输入终结点（摄取 URL），然后你使用该终结点来摄取实时流。频道接收实时输入流并使输出流可供通过一个或多个流式传输终结点进行流式传输。 

当创建频道时，你可以获取摄取 URL。若要获取这些 URL，频道不一定要处于已启动状态。当准备好开始将数据发布到频道时，必须启动频道。在实时转码器开始摄取数据后，你可以通过预览 URL 来预览流。

使用媒体服务，你可以通过 SSL 连接摄取实时的 Smooth Streaming (FMP4) 内容。若要通过 SSL 进行摄取，请确保将摄取 URL 更新为 HTTPS。 

当前，无法通过 SSL 连接摄取 RTMP 实时流。

### <a id="keyframe_interval"></a>关键帧间隔

当使用本地实时编码器生成多比特率流时，关键帧间隔指定 GOP 持续时间（与该外部编码器使用的相同）。当频道收到此传入流后，你可以通过下列任意格式将你的实时流传送到客户端播放应用程序：Smooth Streaming、DASH 和 HLS。当执行实时流式传输时，HLS 始终是动态打包的。默认情况下，媒体服务根据从实时编码器收到的关键帧间隔（也称为图片组 - GOP）自动计算 HLS 段打包比率（每段的片数）。 

下表显示了段持续时间是如何计算的：

<table border="1">
<tr><th>关键帧间隔</th><th>HLS 段打包比率 (FragmentsPerSegment)</th><th>示例</th></tr>
<tr><td>小于或等于 3 秒</td><td>3:1</td><td>如果 KeyFrameInterval（或 GOP）为 2 秒长，则默认的 HLS 段打包比率将是 3:1，这将创建一个 6 秒的 HLS 段。</td></tr>
<tr><td>3 到 5 秒</td><td>2:1</td><td>如果 KeyFrameInterval（或 GOP）为 4 秒长，则默认的 HLS 段打包比率将是 2:1，这将创建一个 8 秒的 HLS 段。</td></tr>
<tr><td>大于 5 秒</td><td>1:1</td><td>如果 KeyFrameInterval（或 GOP）为 6 秒长，则默认的 HLS 段打包比率将是 1:1，这将创建一个 6 秒长的 HLS 段。</td></tr>
</table>

你可以通过配置频道的输出并设置 ChannelOutputHls 上的 FragmentsPerSegment 来更改每段的片数这一比率。 

你还可以通过设置 ChanneInput 上的 KeyFrameInterval 属性更改关键帧间隔值。 

如果你显式设置了 KeyFrameInterval，则会使用上面所述的规则计算 HLS 段打包比率 FragmentsPerSegment。  

如果你同时显式设置了 KeyFrameInterval 和 FragmentsPerSegment，则媒体服务将使用你设置的值。 

## 频道预览 

### 预览 URL

频道还提供了一个预览终结点（预览 URL），你可以使用它在进一步处理和传递流之前预览流并对其进行验证。

你可以在创建频道时获取预览 URL。若要获取该 URL，频道不一定要处于已启动状态。 

在频道开始摄取数据后，你可以预览流。

请注意，当前，不管指定了哪种输入类型，都只能以分片 MP4 (Smooth Streaming) 格式来传送预览流。你可以使用 [http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor) 播放器来测试平滑流。你还可以使用 Azure 管理门户中承载的播放器来查看你的流。


### 允许的 IP 地址

你可以定义允许连接到预览终结点的 IP 地址。如果未指定 IP 地址，则将允许任何 IP 地址。允许的 IP 地址可以指定为单个 IP 地址（例如 '10.0.0.1'）或指定为使用一个 IP 地址和 CIDR 子网掩码的 IP 范围（例如 '10.0.0.1/22'）或指定为使用一个 IP 地址和点分十进制子网掩码的 IP 范围（例如 '10.0.0.1(255.255.252.0)'）。

## 频道输出

有关更多信息，请参阅[设置关键帧间隔](#keyframe_interval) 部分。


## 频道的节目

频道与节目相关联，使用节目，你可以控制实时流中的段的发布和存储。频道管理着节目。频道和节目的关系非常类似于传统媒体，频道具有恒定的内容流，而节目的范围限定为该频道上的一些定时事件。

你可以通过设置 **ArchiveWindowLength** 属性，指定你希望保留多少小时的节目录制内容。此值的设置范围是最短 5 分钟，最长 25 小时。存储时间窗口长度还决定了客户端能够从当前实时位置按时间向后搜索的最长时间。超出指定时间长度后，节目也能够运行，但落在时间窗口长度后面的内容将全部被丢弃。此属性的这个值还决定了客户端清单能够增加多长时间。

每个节目都与某个资产关联。若要发布节目，必须为关联的资产创建按需定位符。创建此定位符后，你可以生成提供给客户端的流 URL。

一个通道最多支持三个并发运行的节目，因此你可以为同一传入流创建多个存档。这样，你便可以根据需要发布和存档事件的不同部分。例如，你的业务要求是存档 6 小时的节目，但只广播过去 10 分钟的内容。为了实现此目的，你需要创建两个同时运行的节目。一个节目设置为存档 6 小时的事件但不发布该节目。另一个节目设置为存档 10 分钟的事件，并且要发布该节目。

不应当将现有节目重用于新事件。而是应当为每个事件创建并启动一个新节目，如"对实时流式传输应用程序进行编程"部分中所述。

在准备好开始流式传输和存档时，启动节目。在要停止对事件进行流式传输和存档时，停止节目。 

若要删除存档的内容，请停止并删除节目，然后删除关联的资产。如果资产被某个节目使用，则无法将其删除，必须先删除该节目。 

即使你停止并删除了节目，只要你没有删除资产，用户也将能够按需将你的已存档内容作为视频进行流式传输。

如果希望保留已存档的内容但不希望其可供流式传输，请删除流式传输定位符。

如果希望保护你的资产，请遵循下面的步骤。你可以在[此处](/documentation/articles/media-services-live-streaming-workflow)找到相关文章的链接。 

- 配置内容密钥授权策略。
- 配置资产传送策略。 

## 频道状态

频道的当前状态。可能的值包括：

- 已停止。这是频道在创建后的初始状态。在此状态下，可以更新频道属性，但不允许进行流式传输。
- 正在启动。频道正在启动。在此状态下，不允许进行更新或流式传输。如果发生错误，则频道会返回到"已停止"状态。
- 正在运行。频道能够处理实时流。
- 正在停止。频道正在停止。在此状态下，不允许进行更新或流式传输。
- 正在删除。频道正被删除。在此状态下，不允许进行更新或流式传输。 

## 隐藏字幕和广告插入 

下表展示了支持的隐藏字幕和广告插入标准。

<table border="1">
<tr><th>标准</th><th>说明</th></tr>
<tr><td>CEA-708 和 EIA-608 (708/608)</td><td>CEA-708 和 EIA-608 是适用于美国和加拿大的隐藏字幕标准。<br/>当前，只有当编码的输入流中携带了该字幕时才支持该字幕。你需要使用能够向发送到媒体服务的编码流插入 608 或 708 字幕的实时媒体编码器。媒体服务会将带有插入的字幕的内容传送到你的显示器。</td></tr>
<tr><td>ismt 内的 TTML（Smooth Streaming 文本轨道）</td><td>媒体服务动态打包功能允许你的客户端对下列任何格式的内容进行流式传输：MPEG DASH、HLS 或 Smooth Streaming。不过，如果你摄取了 .ismt 内带有字幕（Smooth Streaming 文本轨道）的分片 MP4 (Smooth Streaming)，则只能将该流传送到 Smooth Streaming 客户端。</td></tr>
<tr><td>SCTE-35</td><td>用来提示广告插入的数字信号系统。下游接收器使用该信号来将广告接合到流中并使其占用规定的时间。SCTE-35 在输入流中必须作为稀疏轨道进行发送。<br/>请注意，当前唯一受支持的可以携带广告信号的输入流格式是分片 MP4 (Smooth Streaming)。唯一受支持的输出格式也是 Smooth Streaming.</td></tr>
</table>

## 注意事项

只有当你的频道处于正在运行状态时才会向你收费。

每当你重新配置转码器后，请对频道调用**重置**方法。在重置频道之前，必须停止节目。在重置频道后，重新启动节目。 

只有当频道处于"正在运行"状态且频道中的所有节目都已停止时才能停止频道。

默认情况下，你只能向你的媒体服务帐户添加 5 个频道。有关更多信息，请参阅[配额和限制](/documentation/articles/media-services-quotas-and-limitations)。


[live-overview]: ./media/media-services-overview/media-services-live-streaming-current.png


<!--HONumber=51-->
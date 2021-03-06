---
title: "ExpressRoute 位置 | Microsoft Docs"
description: "本文详细说明了服务的上市区域，以及如何连接到 Azure 区域。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
ms.assetid: feb67da3-5abc-4acb-bad4-f78e3c541ded
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/02/2016
ms.author: cherylmc
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: 86b7d396307761acb8baee5761f08a3e1120cddc


---
# <a name="expressroute-partners-and-peering-locations"></a>ExpressRoute 合作伙伴和对等位置
本文中的表格提供有关 ExpressRoute 连接提供商、ExpressRoute 地理覆盖范围、通过 ExpressRoute 支持的 Microsoft 云服务以及 ExpressRoute 系统集成商 (SI) 的信息。

## <a name="a-namepartnersaexpressroute-connectivity-providers"></a><a name="partners"></a>ExpressRoute 连接服务提供商
所有的 Azure 区域和位置都支持 ExpressRoute。 以下地图提供了 Azure 区域和 ExpressRoute 位置的列表。 ExpressRoute 位置是指 Microsoft 与多个服务提供商对等互连的位置。

![位置地图][0]

如果你至少与地缘政治区域内的一个 ExpressRoute 位置连接，你将有权访问地缘政治区域内所有区域中的 Azure 服务。 下表提供了地缘政治区域内 ExpressRoute 位置与 Azure 区域的映射。

| **地缘政治区域** | **Azure 区域** | **ExpressRoute 位置** |
| --- | --- | --- |
| **北美** |美国东部、美国西部、美国东部 2 区、美国中部、美国中南部、美国中北部、加拿大中部、加拿大东部 |亚特兰大、芝加哥、达拉斯、拉斯维加斯、洛杉矶、纽约、西雅图、硅谷、华盛顿特区、蒙特利尔+、魁北克市+、多伦多 |
| **南美洲** |巴西南部 |圣保罗 |
| **欧洲** |北欧、西欧、英国西部、英国南部 |阿姆斯特丹、都柏林、伦敦、纽波特（威尔士）+、巴黎 |
| **亚洲** |东亚、东南亚 |中国香港特别行政区、新加坡 |
| **日本** |日本西部、日本东部 |大坂、东京 |
| **澳大利亚** |澳大利亚东南部、澳大利亚东部 |墨尔本、悉尼 |
| **印度** |印度西部、印度中部、印度南部 |金奈、孟买 |

下表提供了国家/地区云的区域和地缘政治边界的信息。

| **地缘政治区域** | **Azure 区域** | **ExpressRoute 位置** |
| --- | --- | --- | --- |
| **美国政府云** |美国爱荷华州政府、美国弗吉尼亚州政府 |芝加哥、达拉斯、纽约、华盛顿特区 |
| **中国** |中国北部、中国东部 |北京、上海 |
| **德国** |德国中部、德国东部 |柏林、法兰克福 |

标准 ExpressRoute SKU 不支持跨地缘政治区域的连接。 你需要启用 ExpressRoute 高级版附加组件才能支持全球连接。 不支持连接到国家/地区云环境。 如有需要，请联系连接服务提供商。

## <a name="connectivity-provider-locations"></a>连接服务提供商位置
> [!div class="op_single_selector"]
> [按提供商划分的位置](expressroute-locations.md#connectivity-provider-locations)
> [按位置划分的提供商](expressroute-locations-providers.md#connectivity-provider-locations)
> 
> 

### <a name="production-azure"></a>生产 Azure
| **位置** | **服务提供商** |
| --- | --- |
| **阿姆斯特丹** |Aryaka Networks、AT&T NetBond、British Telecom、Colt、Equinix、euNetworks、GÉANT、InterCloud、Internet Solutions - Cloud Connect、Interxion、Level 3 Communications、Orange、Tata Communications、TeleCity Group、Telenor、Verizon |
| **亚特兰大** |Equinix |
| **金奈** |SIFY、Tata Communications |
| **芝加哥** |AT&T NetBond、Comcast、Equinix、Level 3 Communications、Zayo Group |
| **达拉斯** |Aryaka Networks、AT&T NetBond、Cologix、Equinix、Level 3 Communications、Megaport |
| **都柏林** |Colt、Telecity Group |
| **香港** |British Telecom、China Telecom Global、Equinix、Megaport、Orange、PCCW Global Limited、Tata Communications、Verizon |
| **伦敦** |AT&T NetBond、British Telecom、Colt、Equinix、InterCloud、Internet Solutions - Cloud Connect、Interxion、Jisc、Level 3 Communications、MTN、NTT Communications、Orange、Tata Communications、Telecity Group、Telenor、Verizon、Vodafone |
| **拉斯维加斯** |Level 3 Communications+、Megaport |
| **洛杉矶** |CoreSite、Equinix、Megaport、NTT、Zayo Group |
| **墨尔本** |AARNet、Equinix、Megaport、NEXTDC、Telstra Corporation |
| **纽约** |Equinix、Megaport、Zayo Group |
| **纽波特(威尔士)+** |Next Generation Data+ |
| **Montreal** |Cologix+ |
| **Mumbai** |Tata Communications |
| **大阪** |Equinix、Internet Initiative Japan Inc. - IIJ、NTT Communications、Softbank |
| **巴黎** |Interxion、Equinix+ |
| **圣保罗** |Equinix、Telefonica |
| **西雅图** |Equinix、Level 3 Communications、Megaport |
| **硅谷** |Aryaka Networks、AT&T NetBond、British Telecom、CenturyLink+、Comcast、Equinix、Level 3 Communications、Orange、Tata Communications、Verizon、Zayo Group |
| **新加坡** |Aryaka Networks、AT&T NetBond、British Telecom、Equinix、InterCloud、Megaport、NTT Communications、Orange、SingTel、Tata Communications、Verizon |
| **悉尼** |AARNet、AT&T NetBond、British Telecom、Equinix、Megaport、NEXTDC、Orange、Telstra Corporation、Verizon |
| **东京** |Aryaka Networks、British Telecom、Colt, Equinix、Internet Initiative Japan Inc. - IIJ、NTT Communications、Softbank、Verizon |
| **多伦多** |Cologix、Equinix、Zayo Group |
| **华盛顿特区** |Aryaka Networks、AT&T NetBond、British Telecom、Comcast、Equinix、InterCloud、Level 3 Communications、Megaport、NTT Communications、Orange、Tata Communications、Verizon、Zayo Group |

 **+** 表示即将推出

### <a name="national-cloud-environments"></a>国家/地区云环境
#### <a name="us-government-cloud"></a>美国政府云
| **位置** | **服务提供商** |
| --- | --- |
| **芝加哥** |AT&T NetBond、Equinix、Level 3 Communications、Verizon |
| **达拉斯** |Equinix、Verizon |
| **纽约** |Equinix、Level 3 Communications+、Verizon |
| **华盛顿特区** |AT&T NetBond、Equinix、Level 3 Communications、Verizon |

#### <a name="china"></a>中国
| **位置** | **服务提供商** |
| --- | --- |
| **北京** |中国电信 |
| **上海** |中国电信 |

若要了解详细信息，请参阅 [位于中国的 ExpressRoute](http://www.windowsazure.cn/home/features/expressroute/)

#### <a name="germany"></a>德国
| **位置** | **服务提供商** |
| --- | --- |
| **柏林** |Colt+、e-shelter |
| **法兰克福** |Colt、Equinix、Interxion |

## <a name="a-namenonpartnersaconnectivity-through-service-providers-not-listed"></a><a name="nonpartners"></a>通过未列出的服务提供商建立连接
如果前面部分中未列出你的连接服务提供商，你仍可以建立连接。

* 请咨询你的连接服务提供商，以确定他们是否已连接到上表中列出的任何 Exchange 提供商。 你可以访问以下链接，以收集 Exchange 提供商所提供的服务的详细信息。 已有多个连接提供商连接到以太网 Exchange。
  
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
  * [InterXion](http://www.interxion.com/)
  * [NextDC](http://www.nextdc.com/)
  * [CoreSite](http://www.coresite.com/)
  * [Cologix](http://www.cologix.com/)
* 让你的连接提供商将你的网络扩展到选择的对等互连位置。
  * 确保连接提供商以高可用性方式扩展你的连接，以防出现单点故障。
* 从 Exchange 连接服务提供商处订购一条 ExpressRoute 线路以连接到 Microsoft。
  * 根据 [创建 ExpressRoute 线路](expressroute-howto-circuit-classic.md) 中的步骤来设置连接。

| **位置** | **Exchange** | **连接提供商** |
| --- | --- | --- |
| **纽约** |Equinix |Lightower |
| **西雅图** |Equinix |Alaska Communications |
| **硅谷** |Equinix |XO Communications |
| **新加坡** |Equinix |1CLOUDSTAR |
| **华盛顿特区** |Equinix |Lightower |

## <a name="expressroute-system-integrators"></a>ExpressRoute 系统集成商
根据网络的规模，有时，很难启用专用连接来满足需要。 你可以与下表中列出的任一系统集成商合作，以帮助将你加入 ExpressRoute。

| **所在洲** | **系统集成商** |
| --- | --- |
| **亚洲** |Avanade Inc.、OneAs1a |
| **欧洲** |Avanade Inc.、Dotnet Solutions |
| **美国** |Avanade Inc.、Equinix Professional Services、Perficient、Project Leadership |

## <a name="next-steps"></a>后续步骤
* 有关 ExpressRoute 的详细信息，请参阅 [ExpressRoute 常见问题](expressroute-faqs.md)。
* 确保符合所有先决条件。 请参阅 [ExpressRoute 先决条件](expressroute-prerequisites.md)。

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "位置地图"



<!--HONumber=Nov16_HO2-->



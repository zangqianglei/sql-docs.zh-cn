---
title: "使用 Reporting Services 扩展保护身份验证 |Microsoft 文档"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb5c6f4a-3ed5-430b-a712-d5ed4b6b9b2b
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3d0ba0f40d1d93f03a08b762d379cbe1242f0cd1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---

# <a name="extended-protection-for-authentication-with-reporting-services"></a>Reporting Services 针对验证的扩展保护

  扩展保护是针对最新版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 操作系统的一组增强功能。 扩展保护增强了应用程序可用来保护凭据和身份验证的方式。 此功能自身并不直接提供保护机制来防止特定攻击（如凭据转发），但它为诸如 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的应用程序提供了一种基础结构来实施针对验证的扩展保护。  
  
 作为扩展保护一部分的主要身份验证增强功能是服务绑定和渠道绑定。 渠道绑定使用渠道绑定标记 (CBT)，以验证在两个端点之间建立的渠道不会受到危害。 服务绑定使用服务器主体名称 (SPN) 来验证身份验证标记的预期目的地。 有关扩展保护的详细背景信息，请参阅 [Integrated Windows Authentication with Extended Protection（将 Windows 身份验证与扩展保护相集成）](http://go.microsoft.com/fwlink/?LinkId=179922)。  
  
SQL Server Reporting Services (SSRS) 支持和实行已在操作系统中启用并配置中的扩展保护[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 默认情况下， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 接受指定 Negotiate 或 NTLM 身份验证的请求，因此，可能因操作系统中支持扩展保护以及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展保护功能而受益。  
  
> [!IMPORTANT]  
>  默认情况下，Windows 不启用扩展保护。 有关如何在 Windows 中启用扩展保护的信息，请参阅 [身份验证的扩展保护](http://go.microsoft.com/fwlink/?LinkID=178431)。 操作系统和客户端身份验证堆栈必须同时支持扩展保护，身份验证才能成功。 对于较早的操作系统，您可能需要安装多个更新，才能获得完整的支持扩展保护功能的计算机。 有关扩展保护的最新开发动态的信息，请参阅 [updated information with Extended Protection（扩展保护的更新信息）](http://go.microsoft.com/fwlink/?LinkId=183362)。  

## <a name="reporting-services-extended-protection-overview"></a>Reporting Services 扩展保护概述

SSRS 支持和实行已在操作系统中启用的扩展的保护。 如果操作系统不支持扩展保护或者尚未启用操作系统中的此功能， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展保护功能将无法进行身份验证。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展保护还需要 SSL 证书。 有关详细信息，请参阅 [配置本机模式报表服务器上的 SSL 连接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
> [!IMPORTANT]  
>  默认情况下， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不启用扩展保护。 可以通过修改 **rsreportserver.config** 配置文件或使用 WMI API 来更新此配置文件，以便启用此功能。 SSRS 不提供一个用户界面来修改或查看扩展保护设置。 有关详细信息，请参阅本主题中的 [配置设置](#ConfigurationSettings) 部分。  
  
 因更改扩展保护设置或所配置的设置不正确而导致的共同问题并不显示明显的错误消息或对话框窗口。 与扩展保护配置和兼容性相关的问题会导致身份验证失败并在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 跟踪日志中记录错误。  
  
> [!IMPORTANT]  
>  某些数据访问技术可能不支持扩展保护。 数据访问技术用于连接到 SQL Server 数据源和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 目录数据库。 未能实现支持扩展保护的数据访问技术将在以下方面影响 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ：  
>   
>  -   运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 目录数据库的 SQL Server 无法启用扩展保护，或者，报表服务器将无法成功地连接到目录数据库并且将返回身份验证错误。  
> -   所有用作 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表数据源的 SQL Server 都无法启用扩展保护，或者报表服务器尝试连接到报表数据源时将失败并且返回身份验证错误。  
>   
>  用于数据访问技术的文档应该具有与支持扩展保护有关的信息。  
  
### <a name="upgrade"></a>升级  
  
-   升级[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]到 SQL Server 2016 的服务器将使用默认值为配置设置添加**rsreportserver.config**文件。 如果设置已存在，则 SQL Server 2016 安装将保留在**rsreportserver.config**文件。  
  
-   将配置设置添加到 **rsreportserver.config** 配置文件时，默认行为是针对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 将扩展保护功能设置为关闭，必须按本主题所述启用此功能。 有关详细信息，请参阅本主题中的 [配置设置](#ConfigurationSettings) 部分。  
  
-   **RSWindowsExtendedProtectionLevel** 设置的默认值为 **Off**。  
  
-   **RSWindowsExtendedProtectionScenario** 设置的默认值为 **Proxy**。  
  
-   升级顾问不验证操作系统或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的当前安装是否启用了扩展保护支持。  
  
### <a name="what-reporting-services-extended-protection-does-not-cover"></a>Reporting Services 扩展保护不涵盖的内容  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展保护功能不支持以下功能区和方案：  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 自定义安全扩展插件的作者必须将对于扩展保护的支持添加到其自定义安全扩展插件。  
  
-   添加到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装或它使用的第三方组件必须由第三方供应商进行更新以支持扩展保护功能。 有关详细信息，请与第三方供应商联系。  
  
## <a name="deployment-scenarios-and-recommendations"></a>部署方案和建议  
 以下各方案说明各种不同部署和拓扑，以及使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展保护来对它们进行保护的建议配置。  
  
### <a name="direct"></a>直接  
 此方案介绍直接连接到报表服务器（例如 Intranet 环境）。  
  
|应用场景|方案图|保护方式|  
|--------------|----------------------|-------------------|  
|直接 SSL 通信。<br /><br /> 报表服务器将实行“客户端到报表服务器”渠道绑定。|![RS_ExtendedProtection_DirectSSL](../../reporting-services/security/media/rs-extendedprotection-directssl.gif "RS_ExtendedProtection_DirectSSL")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器|将 **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Direct**。<br /><br /> <br /><br /> - 服务绑定不是必需的，因为将使用 SSL 渠道来进行渠道绑定。|  
|直接 HTTP 通信。 报表服务器将实行“客户端到报表服务器”服务绑定。|![RS_ExtendedProtection_Direct](../../reporting-services/security/media/rs-extendedprotection-direct.gif "RS_ExtendedProtection_Direct")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器|将 **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Any**。<br /><br /> <br /><br /> - 没有 SSL 渠道，因此不可能实行渠道绑定。<br /><br /> - 可以使服务绑定生效，但是，由于没有渠道绑定，它将成为不完善的防御机制，服务绑定本身只能防止基本威胁。|  
  
### <a name="proxy-and-network-load-balancing"></a>代理和网络负载平衡  
 客户端应用程序连接到执行 SSL 并向服务器传递凭据以进行身份验证的设备或软件，例如，Extranet、Internet 或安全 Intranet。 客户端连接到代理，或者所有客户端都使用代理。  
  
 当您使用网络负载平衡 (NLB) 设备时，情形是相同的。  
  
|应用场景|方案图|保护方式|  
|--------------|----------------------|-------------------|  
|HTTP 通信。 报表服务器将实行“客户端到报表服务器”服务绑定。|![RS_ExtendedProtection_Indirect](../../reporting-services/security/media/rs-extendedprotection-indirect.gif "RS_ExtendedProtection_Indirect")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器<br /><br /> 3) 代理|将 **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Any**。<br /><br /> <br /><br /> - 没有 SSL 渠道，因此不可能实行渠道绑定。<br /><br /> - 必须对报表服务器进行配置，使之识别代理服务器的名称，以确保正确实行服务绑定。|  
|HTTP 通信。<br /><br /> 报表服务器将实行“客户端到代理”渠道绑定和“客户端到报表服务器”服务绑定。|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器<br /><br /> 3) 代理|将 <br />                    **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Proxy**。<br /><br /> <br /><br /> - 到代理的 SSL 渠道是可用的，因此，可以与代理之间实行渠道绑定。<br /><br /> - 还可以实行服务绑定。<br /><br /> - 报表服务器必须了解代理名称，报表服务器管理员应使用主机标头为它创建一个 URL 保留项，或在 Windows 注册表项 **BackConnectionHostNames**中配置代理名称。|  
|与安全代理之间的间接 HTTPS 通信。 报表服务器将实行“客户端到代理”渠道绑定和“客户端到报表服务器”服务绑定。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器<br /><br /> 3) 代理|将 <br />                    **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Proxy**。<br /><br /> <br /><br /> - 到代理的 SSL 渠道是可用的，因此，可以与代理之间实行渠道绑定。<br /><br /> - 还可以实行服务绑定。<br /><br /> - 报表服务器必须了解代理名称，报表服务器管理员应使用主机标头为它创建一个 URL 保留项，或在 Windows 注册表项 **BackConnectionHostNames**中配置代理名称。|  
  
### <a name="gateway"></a>网关  
 此方案介绍连接到执行 SSL 和对用户进行身份验证的设备或软件的客户端应用程序。 接着，此设备或软件模拟用户上下文或其他用户上下文，之后对报表服务器发出请求。  
  
|应用场景|方案图|保护方式|  
|--------------|----------------------|-------------------|  
|间接 HTTP 通信。<br /><br /> 网关将实行“客户端到网关”渠道绑定。 此时具有“网关到报表服务器”服务绑定。|![RS_ExtendedProtection_Indirect_SSL](../../reporting-services/security/media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器<br /><br /> 3) 网关设备|将 **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Any**。<br /><br /> <br /><br /> - 从客户端到报表服务器的渠道绑定是不可能的，因为网关模拟上下文，并因此创建一个新的 NTLM 标记。<br /><br /> - 此时，从网关到报表服务器没有 SSL，因此无法实行渠道绑定。<br /><br /> - 可以实行服务绑定。<br /><br /> - 应由管理员配置网关设备以实行渠道绑定。|  
|与安全网关之间的间接 HTTPS 通信。 网关将实行“客户端到网关”渠道绑定，报表服务器将实行“网关到报表服务器”渠道绑定。|![RS_ExtendedProtection_IndirectSSLandHTTPS](../../reporting-services/security/media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器<br /><br /> 3) 网关设备|将 **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Direct**。<br /><br /> <br /><br /> - 从客户端到报表服务器的渠道绑定是不可能的，因为网关模拟上下文，并因此创建一个新的 NTLM 标记。<br /><br /> - 从网关到报表服务器的 SSL 意味着可以实行渠道绑定。<br /><br /> - 不需要服务绑定。<br /><br /> - 应由管理员配置网关设备以实行渠道绑定。|  
  
### <a name="combination"></a>组合  
 此方案介绍客户端连接到代理的 Extranet 或 Internet 环境。 这种环境与客户端在其中连接到报表服务器的 Intranet 环境相结合。  
  
|应用场景|方案图|保护方式|  
|--------------|----------------------|-------------------|  
|从客户端间接和直接访问报表服务器服务，在客户端到代理或客户端到报表服务器连接中均没有 SSL。|1) 客户端应用程序<br /><br /> 2) 报表服务器<br /><br /> 3) 代理<br /><br /> 4) 客户端应用程序|将 **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Any**。<br /><br /> <br /><br /> - 可以实行从客户端到报表服务器的服务绑定。<br /><br /> - 报表服务器必须了解代理名称，报表服务器管理员应使用主机标头为它创建一个 URL 保留项，或在 Windows 注册表项 **BackConnectionHostNames**中配置代理名称。|  
|从客户端间接和直接访问报表服务器，其中，客户端与代理或报表服务器建立 SSL 连接。|![RS_ExtendedProtection_CombinationSSL](../../reporting-services/security/media/rs-extendedprotection-combinationssl.gif "RS_ExtendedProtection_CombinationSSL")<br /><br /> 1) 客户端应用程序<br /><br /> 2) 报表服务器<br /><br /> 3) 代理<br /><br /> 4) 客户端应用程序|将 **RSWindowsExtendedProtectionLevel** 设置为 **Allow** 或 **Require**。<br /><br /> 将 **RSWindowsExtendedProtectionScenario** 设置为 **Proxy**。<br /><br /> <br /><br /> - 可以使用渠道绑定<br /><br /> - 报表服务器必须了解代理名称，报表服务器管理员应使用主机标头为代理创建一个 URL 保留项，或在 Windows 注册表项 **BackConnectionHostNames**中配置代理名称。|  
  
## <a name="configuring-reporting-rervices-extended-protection"></a>配置 Reporting Rervices 扩展保护  
 **rsreportserver.config** 文件包含的配置值用于控制 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 扩展保护的行为。  
  
 有关使用和编辑 **rsreportserver.config** 文件的详细信息，请参阅 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。 还可以使用 WMI API 更改和检查扩展保护设置。 有关详细信息，请参阅 [SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)。  
  
 当对配置设置进行验证失败时，将在报表服务器上禁用身份验证类型 **RSWindowsNTLM**、 **RSWindowsKerberos** 和 **RSWindowsNegotiate** 。  
  
###  <a name="ConfigurationSettings"></a> Reporting Services 扩展保护的配置设置  
 下表提供有关在 **rsreportserver.config** 中显示的扩展保护配置设置的信息。  
  
|设置|Description|  
|-------------|-----------------|  
|**RSWindowsExtendedProtectionLevel**|指定扩展保护的实行程度。 有效值包括：<br /><br /> **Off**：默认值。 指定没有渠道绑定或服务绑定验证。<br /><br /> **Allow** 支持扩展保护，但并不需要此功能。  指定：<br /><br /> - 将为在支持扩展保护的操作系统上运行的客户端应用程序实行扩展保护。 实行保护的方式通过设置 **RsWindowsExtendedProtectionScenario**来确定<br /><br /> - 对于在不支持扩展保护的操作系统上运行的应用程序而言，将允许进行身份验证。<br /><br /> **Require** 指定：<br /><br /> - 将为在支持扩展保护的操作系统上运行的客户端应用程序实行扩展保护。<br /><br /> - 对于在不支持扩展保护的操作系统上运行的应用程序而言，将 **不** 允许进行身份验证。|  
|**RsWindowsExtendedProtectionScenario**|指定使哪种格式的扩展保护生效：渠道绑定、服务绑定或这两者。 有效值包括：<br /><br /> **Proxy**：默认值。 指定：<br /><br /> - 当存在渠道绑定标记时，使用 Windows NTLM、Kerberos 和 Negotiate 身份验证。<br /><br /> - 实行服务绑定。<br /><br /> **Any** 指定：<br /><br /> - 不要求 Windows NTLM、Kerberos 和 Negotiate 身份验证以及渠道绑定。<br /><br /> - 实行服务绑定。<br /><br /> **Direct** 指定：<br /><br /> - 当 CBT 存在、与当前服务之间存在 SSL 连接并且用于 SSL 连接的 CBT 与 NTLM、Kerberos 或 Negotiate 标记的 CBT 匹配时，应使用 Windows NTLM、Kerberos 和 Negotiate 身份验证。<br /><br /> - 不实行服务绑定。<br /><br /> <br /><br /> 注意：如果 **RsWindowsExtendedProtectionLevel** 设置为 **OFF** ，则忽略 **RsWindowsExtendedProtectionScenario**设置。|  
  
 **rsreportserver.config** 配置文件中的示例条目：  
  
```  
<Authentication>  
         <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
         <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionLevel>  
</Authentication>  
```  
  
## <a name="service-binding-and-included-spns"></a>服务绑定和所包含的 SPN  
 服务绑定使用服务器主体名称或 SPN 来验证身份验证标记的预期目标。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用现有的 URL 保留项信息来生成视为有效的 SPN 的列表。 使用 URL 保留项信息来验证 SPN 和 URL 保留项使系统管理员能够从单个位置管理这两者。  
  
 当报表服务器启动、扩展保护的配置设置更改或回收应用程序域时，将更新有效 SPN 的列表。  
  
 SPN 的有效列表特定于每个应用程序。 例如，报表管理器和报表服务器每个都将计算不同的有效 SPN 列表。  
  
 为应用程序计算的有效 SPN 列表由以下元素确定：  
  
-   每个 URL 保留项。  
  
-   从域控制器为 Reporting Services 服务帐户检索的每个 SPN。  
  
-   如果 URL 保留项包含通配符（“*”或“+”），则报表服务器将从 Hosts 集合添加每个条目。  
  
### <a name="hosts-collection-sources"></a>Hosts 集合来源。  
 下表列出了 Hosts 集合的潜在来源。  
  
|源类型|Description|  
|--------------------|-----------------|  
|ComputerNameDnsDomain|分配给本地计算机的 DNS 域的名称。 如果本地计算机为群集中的节点，则将使用群集虚拟服务器的 DNS 域名。|  
|ComputerNameDnsFullyQualified|唯一标识本地计算机的完全限定 DNS 名称。 此名称是 DNS 主机名和 DNS 域名的组合，格式为 *HostName*.*DomainName*。 如果本地计算机为群集中的节点，则将使用群集虚拟服务器的完全限定 DNS 名称。|  
|ComputerNameDnsHostname|本地计算机的 DNS 主机名。 如果本地计算机为群集中的节点，则将使用群集虚拟服务器的 DNS 主机名。|  
|ComputerNameNetBIOS|本地计算机的 NetBIOS 名称。 如果本地计算机为群集中的节点，则将使用群集虚拟服务器的 NetBIOS 主机名。|  
|ComputerNamePhysicalDnsDomain|分配给本地计算机的 DNS 域的名称。 如果本地计算机为群集中的节点，则将使用本地计算机的 DNS 域名，而不使用群集虚拟服务器的名称。|  
|ComputerNamePhysicalDnsFullyQualified|唯一标识计算机的完全限定 DNS 名称。 如果本地计算机为群集中的节点，则将使用本地计算机的完全限定 DNS 名称，而不使用群集虚拟服务器的名称。<br /><br /> 此完全限定的 DNS 名称是 DNS 主机名和 DNS 域名的组合，格式为 *HostName*.*DomainName*。|  
|ComputerNamePhysicalDnsHostname|本地计算机的 DNS 主机名。 如果本地计算机为群集中的节点，则将使用本地计算机的 DNS 主机名，而不使用群集虚拟服务器的名称。|  
|ComputerNamePhysicalNetBIOS|本地计算机的 NetBIOS 名称。 如果本地计算机为群集中的节点，则将使用本地计算机的 NetBIOS 主机名，而不使用群集虚拟服务器的名称。|  
  
 当添加 SPN 时，将向跟踪日志添加类似如下内容的条目：  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalNetBIOS> - <theservername>.`  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalDnsHostname> - <theservername>.`  
  
 有关详细信息，请参阅[为报表服务器注册服务主体名称 (SPN)](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)和[关于 URL 保留项和注册（SSRS 配置管理器）](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)。  
  
## <a name="next-steps"></a>后续步骤

[使用扩展保护连接到数据库引擎](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)   
[针对验证的扩展保护概述](http://go.microsoft.com/fwlink/?LinkID=177943)   
[Integrated Windows Authentication with Extended Protection（将 Windows 身份验证与扩展保护相集成）](http://go.microsoft.com/fwlink/?LinkId=179922)   
[Microsoft 安全建议：针对验证的扩展保护](http://go.microsoft.com/fwlink/?LinkId=179923)   
[报表服务器服务跟踪日志](../../reporting-services/report-server/report-server-service-trace-log.md)   
[RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[SetExtendedProtectionSettings 方法 (WMI MSReportServer_ConfigurationSetting)](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)  

更多问题？ [尝试的 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
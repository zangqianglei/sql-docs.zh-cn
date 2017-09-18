---
title: "WMI 连接管理器 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.wmiconnection.f1
helpviewer_keywords:
- connections [Integration Services], WMI
- connection managers [Integration Services], WMI
- WMI connection manager [Integration Services]
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 6e314655d6a230bde897ffceb54fadb8d180d1db
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="wmi-connection-manager"></a>WMI 连接管理器
  WMI 连接管理器使得包可以使用 Windows Management Instrumentation (WMI) 来管理企业环境中的信息。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 Web 服务任务使用 WMI 连接管理器。  
  
 将 WMI 连接管理器添加到包时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 WMI 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包的 **Connections** 集合。 该连接管理器的 **ConnectionManagerType** 属性设置为 **WMI**。  
  
## <a name="configuration-of-the-wmi-connection-manager"></a>配置 WMI 连接管理器  
 可按下列方式配置 WMI 连接管理器：  
  
-   指定服务器名称。  
  
-   指定服务器上的命名空间。  
  
-   为连接到服务器选择身份验证模式。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的信息，请参阅 [WMI 连接管理器编辑器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="wmi-connection-manager-editor"></a>WMI 连接管理器编辑器
  可以使用“WMI 连接管理器”对话框指定到服务器的 Microsoft Windows Management Instrumentation (WMI) 连接。  
  
 若要了解有关 WMI 连接管理器的详细信息，请参阅 [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **名称**  
 为连接管理器提供唯一的名称。  
  
 **Description**  
 描述连接管理器。 最好按照连接管理器的用途对其进行说明，使包的说明一目了然，且更便于维护。  
  
 **服务器名称**  
 提供要进行 WMI 连接的服务器的名称。  
  
 **命名空间**  
 指定 WMI 命名空间。  
  
 **使用 Windows 身份验证**  
 选择此项可以使用 Windows 身份验证。 如果使用 Windows 身份验证，则不需要提供连接所用的用户名或密码。  
  
 **用户名**  
 如果不使用 Windows 身份验证，则必须提供连接所用的用户名。  
  
 **密码**  
 如果不使用 Windows 身份验证，则必须提供连接所用的密码。  
  
 **测试**  
 测试连接管理器设置。  
  
## <a name="see-also"></a>另请参阅  
 [Web 服务任务](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS &#41;连接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  

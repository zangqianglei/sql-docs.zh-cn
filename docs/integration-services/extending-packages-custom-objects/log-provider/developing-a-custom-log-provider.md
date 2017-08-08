---
title: "开发自定义日志提供程序 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9d5dee6649539d340fd9954798db913136553aae
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-custom-log-provider"></a>开发自定义日志提供程序
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所具有的广泛的日志记录功能使其可捕获在包执行过程中发生的事件。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]包括各种启用日志，以创建和存储在格式，如 XML、 文本、 数据库或在 Windows 事件日志中的日志提供程序。 如果提供的日志提供程序和输出格式不能完全满足您的需要，您可以创建自定义日志提供程序。  
  
 若要创建自定义日志提供程序，必须创建从 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基类继承的类，再将 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 属性应用到新类，然后重写基类的重要方法和属性，包括 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 属性和 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 方法。  
  
## <a name="in-this-section"></a>本節內容  
 本节介绍如何创建、配置和编写自定义日志提供程序代码。  
  
 [创建自定义日志提供程序](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)  
 介绍如何为自定义日志提供程序项目创建类。  
  
 [编码的自定义日志提供程序](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
 介绍如何通过重写基类的方法和属性实现自定义日志提供程序。  
  
 [开发的自定义日志提供程序的用户界面](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
 中不支持自定义日志提供程序的自定义用户界面[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]。  
  
## <a name="related-topics"></a>相关主题  
  
### <a name="information-common-to-all-custom-objects"></a>所有自定义对象的通用信息  
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的所有类型自定义对象的通用信息，请参阅以下主题：  
  
 [开发 Integration Services 的自定义对象](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 描述中实现的自定义对象的所有类型的基本步骤[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]。  
  
 [使自定义对象持久化](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 介绍自定义持久性并在必要时作出解释。  
  
 [生成、部署和调试自定义对象](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 介绍生成、签名、部署和调试自定义对象的技术。  
  
### <a name="information-about-other-custom-objects"></a>其他自定义对象的信息  
 有关可以在中创建的自定义对象的其他类型的信息[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]，请参阅以下主题：  
  
 [开发自定义任务](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 讨论如何对自定义任务进行编程。  
  
 [开发自定义连接管理器](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 讨论如何对自定义连接管理器进行编程。  
  
 [开发自定义 ForEach 枚举器](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 讨论如何对自定义枚举器进行编程。  
  
 [开发自定义数据流组件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 讨论如何对自定义数据流源、转换和目标进行编程。  
  
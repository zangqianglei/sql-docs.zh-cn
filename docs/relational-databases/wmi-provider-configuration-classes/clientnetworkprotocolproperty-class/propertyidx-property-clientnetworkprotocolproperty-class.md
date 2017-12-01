---
title: "PropertyIdx 属性 （ClientNetworkProtocolProperty 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: PropertyIdx Property (ClientNetworkProtocolProperty Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c7cc1311b307fec6cb78137c780f105e2bace24
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx 属性（ClientNetworkProtocolProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]获取或设置该属性的索引值引用的属性数组中[Properties 属性 （ClientNetworkProtocol 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md)的[ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)表示使用的网络协议的属性的对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 A **uint32**值，该值指定当前属性的数组索引值。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
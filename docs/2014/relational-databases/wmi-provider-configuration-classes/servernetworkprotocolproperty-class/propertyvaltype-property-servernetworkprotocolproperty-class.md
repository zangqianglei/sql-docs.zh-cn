---
title: PropertyValType 属性 （ServerNetworkProtocolProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- PropertyValType Property (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ef74e701a4c940d25717752346eab5edf50f59e7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115817"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 属性（ServerNetworkProtocolProperty 类）
  获取存储在所引用属性中的值的数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ServerNetworkProtocolProperty 类](servernetworkprotocolproperty-class.md)表示的实例上的网络协议的属性的对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定属性值的数据类型的 `uint32` 值。 如果是字符串值类型，则返回 0；如果是数值类型，则返回 1。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  

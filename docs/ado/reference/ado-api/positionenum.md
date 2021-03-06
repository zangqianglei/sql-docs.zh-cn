---
title: PositionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21a2ea98ea4592d9900cd9623502a8d918b34c9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774185"
---
# <a name="positionenum"></a>PositionEnum
指定在记录指针的当前位置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|指示当前记录指针位于 BOF (即[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性是**True**)。|  
|**adPosEOF**|-3|指示当前记录指针位于 EOF (即[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)属性是**True**)。|  
|**adPosUnknown**|-1|指示**记录集**是空的当前的位置是未知的或提供程序不支持[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)或[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)属性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[AbsolutePage 属性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition 属性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|

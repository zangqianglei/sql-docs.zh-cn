---
title: "LastDataUpdate 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- LastDataUpdate Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.lastdataupdate
- http://schemas.microsoft.com/analysisservices/2003/engine#LastDataUpdate
- urn:schemas-microsoft-com:xml-analysis#LastDataUpdate
helpviewer_keywords:
- LastDataUpdate element
ms.assetid: 66e43b17-844f-4ec2-bd1d-35608e7b6524
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 160e0792348cc47ebea64a8b19d0b9e8464900f8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lastdataupdate-element-xmla"></a>LastDataUpdate 元素 (XMLA)
  包含的日期和时间的数据的多维数据集表示通过父[多维数据集](../../../analysis-services/xmla/xml-elements-properties/cube-element-olapinfo-xmla.md)上次更新元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube>  
   ...  
   <LastDataUpdate>...</LastDataUpdate>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|dateTime|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Cube](../../../analysis-services/xmla/xml-elements-properties/cube-element-olapinfo-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
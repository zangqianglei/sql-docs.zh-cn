---
title: STMPointFromWKB（geography 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPointFromWKB (geography Data Type)
- STMPointFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromWKB method
ms.assetid: eeb7d806-3cbb-405d-8199-8b82282c53df
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f5dc6b841fd0f19f418a6c1b479231fe2cbc3539
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47661095"
---
# <a name="stmpointfromwkb-geography-data-type"></a>STMPointFromWKB（geography 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

从开放地理空间信息联盟 (OGC) 已知二进制 (WKB) 表示形式返回 geographyMultiPoint 实例。
  
## <a name="syntax"></a>语法  
  
```  
  
STMPointFromWKB ( 'WKB_multipoint' , SRID )  
```  
  
## <a name="arguments"></a>参数  
 WKB_multipoint  
 希望返回的 geographyMultiPoint 实例的 WKB 表示形式。 WKB_multipoint 是一个 varbinary(max) 表达式。  
  
 SRID  
 一个 int 表达式，表示希望返回的 geographyMultiPoint 实例的空间引用 ID (SRID)。  
  
## <a name="return-types"></a>返回类型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：geography  
  
 CLR 返回类型：SqlGeography  
  
 OGC 类型：MultiPoint  
  
## <a name="remarks"></a>Remarks  
 如果输入的格式不正确，此方法将引发 FormatException。  
  
## <a name="examples"></a>示例  
 下面的示例使用 `STMPointFromWKB()` 创建 `geography` 实例。  
  
```  
DECLARE @g geography;   
SET @g = geography::STMPointFromWKB(0x0104000000020000000101000000D7A3703D0A975EC08716D9CEF7D347400101000000CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另请参阅  
 [OGC 静态地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

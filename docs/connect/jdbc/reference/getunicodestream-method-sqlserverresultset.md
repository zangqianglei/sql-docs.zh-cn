---
title: getUnicodeStream 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0dd61865-663b-47e2-b417-e9df418894cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80a3b4ae3f35bd1e53d7fba68794e177ac855431
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717995"
---
# <a name="getunicodestream-method-sqlserverresultset"></a>getUnicodeStream 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列的值作为 Unicode 字符流。  
  
> [!NOTE]  
>  此方法在 JDBC 规范中已不推荐使用，调用它将导致引发“尚未实现”异常。 应改用 [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 方法。  
  
## <a name="overload-list"></a>重载列表  
  
|名称|描述|  
|----------|-----------------|  
|[getUnicodeStream 方法 &#40;int&#41;](../../../connect/jdbc/reference/getunicodestream-method-int.md)|检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列索引作为 Unicode 字符流的值。|  
|[getUnicodeStream 方法 &#40;java.lang.String&#41;](../../../connect/jdbc/reference/getunicodestream-method-java-lang-string.md)|检索此 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 对象的当前行中指定列名称作为 Unicode 字符流的值。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSet 成员](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 类](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

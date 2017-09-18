---
title: "FOR JSON 如何转义特殊字符和控制字符 (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 21d0e35636e7c34c395f8c2bfe4f5c7ea07a4d9b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>FOR JSON 如何转义特殊字符和控制字符 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主题介绍了 SQL Server **SELECT** 语句的 **FOR JSON** 子句在 JSON 输出中如何转义特殊字符以及如何表示控制字符。  

> [!IMPORTANT]
> 此页介绍了 Microsoft SQL Server 中对 JSON 的内置支持。 有关 JSON 中的转义和编码的常规信息，请参阅 JSON RFC - [http://www.ietf.org/rfc/rfc4627.txt](http://www.ietf.org/rfc/rfc4627.txt) 中的 2.5 部分。

## <a name="escaping-of-special-characters"></a>特殊字符转义  
如果源数据包含特殊字符，则 **FOR JSON** 子句在 JSON 输出中会使用 `\` 对其进行转义，如下表中所示。 在属性名称及其值中，均会发生这种转义。  
  
|**特殊字符**|**转义后的输出**|  
|---------------------------|--------------------------|  
|引号 (")|\\"|  
|反斜杠 (\\)|\\\|  
|正斜杠 (/)|\\/|  
|退格键|\b|  
|换页符|\f|  
|换行符|\n|  
|回车符|\r|  
|水平制表符|\t|  
  
## <a name="control-characters"></a>控制字符  
如果源数据包含控制字符，则 **FOR JSON** 子句在 JSON 输出中会使用 `\u<code>` 格式对其进行转义，如下表中所示。  
  
|**控制字符**|**编码后的输出**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>示例  
 下面是同时包含特殊字符和控制字符的源数据的 **FOR JSON** 输出的示例。  
  
 查询：  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 结果：  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解 SQL Server 中内置 JSON 支持的详细信息  
若要获取大量特定解决方案、用例和建议，请参阅 Microsoft 项目经理 Jovan Popovic 发表的 SQL Server 和 Azure SQL 数据库中的[内置 JSON 支持相关博客文章](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)。
  
## <a name="see-also"></a>另请参阅  
 [使用 FOR JSON 将查询结果格式化为 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR 子句](../../t-sql/queries/select-for-clause-transact-sql.md)

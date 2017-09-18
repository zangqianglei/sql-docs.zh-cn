---
title: "集 ANSI_WARNINGS (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET ANSI_WARNINGS
- ANSI_WARNINGS_TSQL
- ANSI_WARNINGS
- SET_ANSI_WARNINGS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], ISO standard behavior
- warnings [SQL Server]
- SET ANSI_WARNINGS statement
- ANSI_WARNINGS option
ms.assetid: f82aaab0-334f-427b-89b0-de4af596b4fa
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: feee804808cb9ba8d6e3dd97fb512a3a73301e17
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansiwarnings-transact-sql"></a>SET ANSI_WARNINGS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  对几种错误情况指定 ISO 标准行为。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET ANSI_WARNINGS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_WARNINGS ON;  
```  
  
## <a name="remarks"></a>注释  
 SET ANSI_WARNINGS 可以影响下列情况：  
  
-   设置为 ON 时，如果聚合函数（如 SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP 或 COUNT）中出现空值，将生成警告消息。 设置为 OFF 时，不发出警告。  
  
-   设置为 ON 时，被零除错误和算术溢出错误将导致回滚语句，并生成错误消息。 设置为 OFF 时，被零除错误和算术溢出错误将导致返回空值。 如果插入或更新尝试对，则会发生在其中通过零除或算术溢出错误导致返回空值的行为**字符**，Unicode，或**二进制**在其中的列长度新值超过了列的最大大小。 如果 SET ANSI_WARNINGS 为 ON 时，将取消 INSERT 或 UPDATE 所指定的 ISO 标准。 字符列的尾随空格和二进制列的尾随零都将被忽略。 设置为 OFF 时，数据将剪裁为列的大小，并且语句执行成功。  
  
    > [!NOTE]  
    >  当截断发生在任何转换或从**二进制**或**varbinary**发出任何警告或错误的数据，而不考虑 SET 选项。  
  
    > [!NOTE]  
    >  在存储过程和用户定义函数中传递参数，或者在批处理语句中声明和设置变量时，不执行 ANSI_WARNINGS。 例如，如果变量指**char （3)**，然后设置为值大于三个字符，数据将剪裁为定义的大小和插入或更新语句会成功。  
  
 可以使用 sp_configure 的 user options 选项，为服务器的所有连接设置 ANSI_WARNINGS 的默认设置。 有关详细信息，请参阅本主题后面的 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)不熟悉的读者。  
  
 创建或操作对索引视图或计算列的索引时，SET ANSI_WARNINGS 必须为 ON。 如果 SET ANSI_WARNINGS 为 OFF，对计算列或索引视图的索引所在的表执行 CREATE、UPDATE、INSERT 和 DELETE 语句将失败。 对计算列所需的 SET 选项设置的索引的视图和索引的详细信息，请参阅"当你使用 SET 语句的注意事项"中[SET 语句 &#40;Transact SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含 ANSI_WARNINGS 数据库选项。 此选项与 SET ANSI_WARNINGS 等效。 如果 SET ANSI_WARNINGS 为 ON，则发生被零除、字符串超出数据库列及其他类似错误时，将引发错误或警告。 如果 SET ANSI_WARNINGS 为 OFF，则不会引发这些错误和警告。 model 数据库中的 SET ANSI_WARNINGS 默认值为 OFF。 如果未指定，则应用 ANSI_WARNINGS 设置。 如果 SET ANSI_WARNINGS 为 OFF，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用中的 is_ansi_warnings_on 列的值[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图。  
  
 执行分布式查询时，应将 ANSI_WARNINGS 设置为 ON。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接时自动将 ANSI_WARNINGS 设置为 ON。 这可以在 ODBC 数据源、ODBC 连接属性（它们在连接前在应用程序中设置）中进行配置。 从 DB-Library 应用程序连接时，SET ANSI_WARNINGS 的默认值为 OFF。  
  
 SET ANSI_DEFAULTS 为 ON 时，将启用 SET ANSI_WARNINGS。  
  
 SET ANSI_WARNINGS 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
 如果 SET ARITHABORT 或 SET ARITHIGNORE 为 OFF，而 SET ANSI_WARNINGS 为 ON，则遇到被零除或溢出错误时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仍会返回错误消息。  
  
 要查看此设置的当前设置，请运行以下查询。  
  
```  
DECLARE @ANSI_WARN VARCHAR(3) = 'OFF';  
IF ( (8 & @@OPTIONS) = 8 ) SET @ANSI_WARN = 'ON';  
SELECT @ANSI_WARN AS ANSI_WARNINGS;  
```  
  
## <a name="permissions"></a>Permissions  
 要求具有 public 角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例阐释了 SET ANSI_WARNINGS 为 ON 和 OFF 时的上述三种情况。  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE T1   
(  
   a int,   
   b int NULL,   
   c varchar(20)  
);  
GO  
  
SET NOCOUNT ON;  
  
INSERT INTO T1   
VALUES (1, NULL, '')   
      ,(1, 0, '')  
      ,(2, 1, '')  
      ,(2, 2, '');  
  
SET NOCOUNT OFF;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS ON';  
GO  
  
SET ANSI_WARNINGS ON;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (3, 3, 'Text string longer than 20 characters');  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
PRINT '**** Setting ANSI_WARNINGS OFF';  
GO  
SET ANSI_WARNINGS OFF;  
GO  
  
PRINT 'Testing NULL in aggregate';  
GO  
SELECT a, SUM(b)   
FROM T1   
GROUP BY a;  
GO  
  
PRINT 'Testing String Overflow in INSERT';  
GO  
INSERT INTO T1   
VALUES (4, 4, 'Text string longer than 20 characters');  
GO  
SELECT a, b, c   
FROM T1  
WHERE a = 4;  
GO  
  
PRINT 'Testing Divide by zero';  
GO  
SELECT a / b AS ab   
FROM T1;  
GO  
  
DROP TABLE T1  
```  
  
## <a name="see-also"></a>另请参阅  
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;Transact SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  

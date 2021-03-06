---
title: 常量 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e38cf3dd4e18019a3656be584e799d5a1ee40ff3
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698736"
---
# <a name="constants-transact-sql"></a>常量 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

常量，也称为文字值或标量值，是表示一个特定数据值的符号。 常量的格式取决于它所表示的值的数据类型。
  
## <a name="character-string-constants"></a>字符串常量
字符串常量括在单引号内并包含字母数字字符（a-z、A-Z 和 0-9）以及特殊字符，如感叹号 (!)、at 符 (@) 和数字号 (#)。 将为字符串常量分配当前数据库的默认排序规则，除非使用 COLLATE 子句为其指定了排序规则。 用户键入的字符串通过计算机的代码页计算，如有必要，将被转换为数据库的默认代码页。
  
如果已为某个连接将 QUOTED_IDENTIFIER 选项设置成 OFF，则字符串也可以使用双引号括起来，但 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口和 ODBC 驱动程序将自动使用 SET QUOTED_IDENTIFIER ON。 我们建议使用单引号。
  
如果单引号中的字符串包含一个嵌入的引号，可以使用两个单引号表示嵌入的单引号。 对于嵌入在双引号中的字符串则没有必要这样做。
  
以下是字符串的示例：
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
空字符串用中间没有任何字符的两个单引号表示。 在 6.x 兼容模式中，空字符串被看作是一个空格。
  
字符串常量支持增强的排序规则。
  
> [!NOTE]  
>  大于 8000 字节的字符常量为 varchar(max) 类型的数据。  
  
## <a name="unicode-strings"></a>Unicode 字符串
Unicode 字符串的格式与普通字符串相似，但它前面有一个 N 标识符（N 代表 SQL-92 标准中的区域语言）。 N 前缀必须是大写字母。 例如，'Michél' 是字符常量，而 N'Michél' 是 Unicode 常量。 Unicode 常量被解释为 Unicode 数据，并且不使用代码页进行计算。 Unicode 常量有排序规则。 该排序规则主要用于控制比较和如何区分大小写。 为 Unicode 常量分配当前数据库的默认排序规则，除非使用 COLLATE 子句为其指定了排序规则。 对于字符数据，存储 Unicode 数据时每个字符使用 2 个字节，而不是每个字符 1 个字节。 有关详细信息，请参阅 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。
  
Unicode 字符串常量支持增强的排序规则。
  
> [!NOTE]  
>  大于 8000 字节的 Unicode 常量为 nvarchar(max) 类型的数据。  
  
## <a name="binary-constants"></a>二进制常量
二进制常量具有前辍 `0x` 并且是十六进制数字字符串。 这些常量不使用引号括起。
  
下面是二进制字符串的示例：
  
```sql
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  大于 8000 字节的二进制常量为 varbinary(max) 类型的数据。  
  
## <a name="bit-constants"></a>bit 常量
bit 常量使用数字 0 或 1 表示，并且不括在引号中。 如果使用一个大于 1 的数字，则该数字将转换为 1。
  
## <a name="datetime-constants"></a>datetime 常量
datetime 常量使用特定格式的字符日期值来表示，并被单引号括起来。
  
下面是 datetime 常量的示例：
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
下面是 datetime 常量的示例：
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>integer 常量
integer 常量以数字字符串表示，其中数字未用引号括起来并且不包含小数点。 integer 常量必须为整数；它们不能包含小数。
  
下面是 integer 常量的示例：
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>decimal 常量
decimal 常量以数字字符串表示，其中数字未用引号括起来并且包含小数点。
  
下面是 decimal 常量的示例：
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>float 和 real 常量
float 和 real 常量使用科学记数法来表示。
  
下面是 float 或 real 常量值的示例：
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>money 常量
money 常量以数字字符串表示，其中前缀为可选的小数点和可选的货币符号。 money 常量不使用引号括起。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不强制采用任何种类的分组规则，例如在代表货币的字符串中每隔三个数字插入一个逗号 (,)。
  
> [!NOTE]  
>  在指定的 money 文本中，将忽略任何位置的逗号。  
  
下面是 money 常量的示例：
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>uniqueidentifier 常量
uniqueidentifier 常量是表示 GUID 的字符串。 可以使用字符或二进制字符串格式指定。
  
以下示例都指定相同的 GUID：
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>指定负数和正数  
若要指示一个数是正数还是负数，请对数值常量应用 + 或 - 一元运算符。 这将创建一个表示有符号数字值的表达式。 如果没有应用 + 或 - 一元运算符，数值常量将使用正数。
  
有符号 integer 表达式：  
  
```sql
+145345234
-2147483648
```
有符号 decimal 表达式：  
  
```sql
+145345234.2234
-2147483648.10
```
  
有符号 float 表达式：  
  
```sql
+123E-3
-12E5
```
  
有符号 money 表达式：  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>增强的排序规则  
SQL Server 所支持的字符和 Unicode 字符串常量也支持增强的排序规则。 有关详细信息，请参阅 [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) 子句。
  
## <a name="see-also"></a>另请参阅
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[运算符 (Transact-SQL)](../../t-sql/language-elements/operators-transact-sql.md)
  
  

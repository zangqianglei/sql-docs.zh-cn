---
title: "更改程序集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], modifying
- permissions [CLR integration]
- altering assemblies
- ALTER ASSEMBLY statement
ms.assetid: 9e765fbd-f339-473c-8537-22f478e79696
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f279c3f1e1315ea44cdb75918b471c8fdd22ee01
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="altering-an-assembly"></a>更改程序集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]已在中注册的程序集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可以从较新版本使用 ALTER ASSEMBLY 语句更新。 若要更新程序集，可按照如下语法使用 ALTER ASSEMBLY 语句：  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 ALTER ASSEMBLY 不中断当前正在运行且正在使用此程序集的进程；这些进程使用未经更改的程序集继续执行。 ALTER ASSEMBLY 不能用于更改公共语言运行时 (CLR) 函数、聚合函数、存储过程和触发器的签名。 只要未更改签名或属性，就可以向程序集添加新的公共方法，以任何方式修改专用方法以及修改公共方法。 不能使用 ALTER ASSEMBLY 更改本机序列化用户定义类型（包含数据成员或基类）内包含的字段。 不支持所有其他更改。 有关详细信息，请参阅[ALTER ASSEMBLY &#40;Transact SQL &#41;](../../../t-sql/statements/alter-assembly-transact-sql.md).  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>更改程序集的权限集  
 还可以使用 ALTER ASSEMBLY 语句更改程序集的权限集。 下面的语句更改为 SQLCLRTest 程序集的权限集**EXTERNAL_ACCESS**。  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 如果正在从更改程序集的权限集**安全**到**EXTERNAL_ACCESS**或**UNSAFE**，将非对称密钥和相应的登录名与**EXTERNAL ACCESS ASSEMBLY**权限或**UNSAFE ASSEMBLY**必须首先创建程序集的权限。 有关详细信息，请参阅 [Creating an Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)。  
  
## <a name="adding-the-source-code-of-an-assembly"></a>添加程序集的源代码  
 CREATE ASSEMBLY 中不存在 ALTER ASSEMBLY 语法中的 ADD FILE 子句。 您可以使用该子句来添加源代码或与程序集关联的任何其他文件。 这些文件将从其原始位置复制并存储到数据库的系统表中。 如果您需要重新创建或记录 UDT 的当前版本，这样可确保源代码或其他文件随时备用。  
  
 以下语句添加 Point UDT 的 Point.cs 类源代码。 这会复制 Point.cs 文件中包含的文本并用名称“PointSource”将其存储在数据库中。  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>另请参阅  
 [管理 CLR 集成程序集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [创建程序集](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [删除程序集](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [ALTER ASSEMBLY (Transact-SQL)](../../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
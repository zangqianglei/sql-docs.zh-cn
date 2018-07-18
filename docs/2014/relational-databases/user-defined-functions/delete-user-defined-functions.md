---
title: 删除用户定义函数 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: db1d668a-23b7-4757-a9c5-1bd848ba7f6d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9fa7957927c04f883e7aedf5f19571c41fd21e30
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417916"
---
# <a name="delete-user-defined-functions"></a>删除用户定义函数
  你可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 删除 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的用户定义函数 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要删除用户定义函数，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   如果数据库中存在引用此函数的 Transact-SQL 函数或视图并且这些函数或视图通过使用 SCHEMABINDING 创建，或者存在引用该函数的计算列、CHECK 约束或 DEFAULT 约束，则您将无法删除该函数。  
  
-   如果存在引用此函数并且已生成索引的计算列，则您将无法删除该函数。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要具有对该函数所属架构的 ALTER 权限，或对该函数的 CONTROL 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-user-defined-function"></a>删除用户定义函数  
  
1.  单击包含要修改的函数的数据库旁边的加号。  
  
2.  单击 **“可编程性”** 文件夹旁的加号。  
  
3.  单击包含要修改的函数的文件夹旁边的加号：  
  
    -   Table-valued Function  
  
    -   标量值函数  
  
    -   Aggregate 函数  
  
4.  右键单击要删除的函数，然后选择“删除”。  
  
5.  在 **“删除对象”** 对话框中，单击 **“确定”**。  
  
    > [!IMPORTANT]  
    >  单击“删除对象”对话框中的“显示依赖关系”，打开“function_name 依赖关系”对话框。 这将显示依赖于该函数的所有对象和该函数依赖的所有对象。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-user-defined-function"></a>删除用户定义函数  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- creates function called “Sales.ufn_SalesByStore”  
    USE AdventureWorks2012;  
    GO  
    CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
    RETURNS TABLE  
    AS  
    RETURN   
    (  
        SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
        FROM Production.Product AS P   
        JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
        JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
        JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
        WHERE C.StoreID = @storeid  
        GROUP BY P.ProductID, P.Name  
    );  
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- determines if function exists in database  
    IF OBJECT_ID (N'Sales.fn_SalesByStore', N'IF') IS NOT NULL  
    -- deletes function  
        DROP FUNCTION Sales.fn_SalesByStore;  
    GO  
    ```  
  
 有关详细信息，请参阅 [DROP FUNCTION (Transact-SQL)](/sql/t-sql/statements/drop-function-transact-sql)。  
  
  
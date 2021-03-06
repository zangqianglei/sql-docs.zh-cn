---
title: 更改数据库的目标恢复时间 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: e466419a-d8a4-48f7-8d97-13a903ad6b15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8fbf203ad7928de8b9d6e4919f9b1d44b5f5cd45
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141099"
---
# <a name="change-the-target-recovery-time-of-a-database-sql-server"></a>更改数据库的目标恢复时间 (SQL Server)
  本主题介绍如何通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中设置和更改 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据库的目标恢复时间。 默认情况下，目标恢复时间为 0，数据库使用“自动检查点”  （由 **recovery interval** 服务器选项控制）。 如果将目标恢复时间设置为大于 0，数据库将使用“间接检查点”  并为此数据库建立恢复时间上限。  
  
> [!NOTE]  
>  如果长时间运行的事务导致过多 UNDO 时间，则可能超过给定数据库的目标恢复时间设置为该数据库指定的上限。  
  
-   **准备工作：**[限制和局限](#Restrictions)、[安全性](#Security)  
  
-   **若要更改目标恢复时间，请使用：**[SQL Server Management Studio](#SSMSProcedure) 或 [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a>  
  
> [!CAUTION]  
>  为间接检查点配置的数据库上的联机事务工作负荷可能导致性能下降。 间接检查点确保损坏页的数量低于特定阙值，以便在目标恢复时间内完成数据库恢复。 与利用损坏页数量的间接检查点相反，恢复间隔配置选项使用事务数量来确定恢复时间。 当在接收大量 DML 操作的数据库上启用了间接检查点时，后台写入线程可以开始积极刷新磁盘的脏缓冲区，以确保执行恢复所需的时间在数据库所设目标恢复时间范围内。 这可能造成某些系统上出现额外的 I/O 活动，如果磁盘子系统在 I/O 阙值之上或附近运行，则这会导致性能瓶颈。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要对数据库拥有 ALTER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **更改目标恢复时间**  
  
1.  在 **“对象资源管理器”** 中，连接到某个 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例，再展开该实例。  
  
2.  右键单击要更改的数据库，然后单击 **“属性”** 命令。  
  
3.  在 **“数据库属性”** 对话框中，单击 **“选项”** 页。  
  
4.  在 **“恢复”** 面板的 **“目标恢复时间(秒)”** 字段中，指定要作为此数据库恢复时间上限的秒数。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **更改目标恢复时间**  
  
1.  连接到数据库所在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
2.  按如下所示使用以下 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options)语句：  
  
     TARGET_RECOVERY_TIME =target_recovery_time { SECONDS | MINUTES }  
  
     *target_recovery_time*  
     大于 0（默认值）时，指定在发生崩溃的情况下指定数据库的恢复时间上限。  
  
     SECONDS  
     指示 *target_recovery_time* 表示为秒数。  
  
     MINUTES  
     指示 *target_recovery_time* 表示为分钟数。  
  
     以下示例将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的目标恢复时间设置为 `60` 秒。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET TARGET_RECOVERY_TIME = 60 SECONDS;  
    ```  
  
## <a name="see-also"></a>请参阅  
 [数据库检查点 (SQL Server)](database-checkpoints-sql-server.md)   
 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
  

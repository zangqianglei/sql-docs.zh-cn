---
title: "“线程”窗口 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.threads
helpviewer_keywords:
- Threads Window [Transact-SQL]
ms.assetid: e153f619-0049-4162-9076-c24a454f3278
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c5b7d3f057bddab388a75ad48f447ede194c8aa0
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-debugger---threads-window"></a>Transact-SQL 调试器 -“线程”窗口
  “线程” **** 窗口显示有关正在调试的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器会话使用的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 线程的信息。 只有在调试模式下才可以显示此线程信息。  
  
## <a name="task-list"></a>任务列表  
 **访问“线程”窗口**  
  
-   在 **“调试”** 菜单上单击 **“窗口”**，然后单击 **“线程”**。  
  
## <a name="columns"></a>列  
 **ID**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器分配给该线程的唯一标识号。 从 sys.dm_os_threads 动态管理视图中选择某一行，即可找到有关此线程的详细信息。  
  
 如果当前未在轻型池模式下运行，则请选择满足以下条件的行：此行中 os_thread_id 列的值与 **ID** 列的值相匹配。 如果当前在轻型池模式下运行，则请选择满足以下条件的行：此行中 fiber_context_address 列的值与 **ID** 列的值相匹配。  
  
 **名称**  
 以 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 计算机名/实例名 [SPID] **格式显示有关**会话的信息。  
  
 **计算机名**  
 运行查询编辑器会话连接到的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的计算机的名称。  
  
 **InstanceName**  
 查询编辑器会话连接到的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的名称。  
  
 **[SPID]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会话进程 ID，用于唯一标识此会话。 通过在 sys.sysprocesses 视图中选择 spid 列中此 ID 值所在的行，可以获取有关此会话的更多信息。  
  
 **位置**  
 显示正在调试的查询编辑器会话使用的脚本文件的名称。  
  
 **Priority**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器不支持此功能。  
  
 **挂起**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调试器不支持此功能。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-SQL 调试器](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 调试器信息](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [sys.dm_os_threads (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)   
 [sys.sysprocesses (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)  
  
  
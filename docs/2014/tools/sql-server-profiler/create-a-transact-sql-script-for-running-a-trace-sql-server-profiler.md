---
title: 创建 Transact-SQL 脚本来运行跟踪 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], running
- scripts [SQL Server], traces
ms.assetid: 6b0e2519-998d-40d5-b8ba-5e6a773f91a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13bc8fb9497ce9d0cbb4e5adad21cc402217d3d2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138137"
---
# <a name="create-a-transact-sql-script-for-running-a-trace-sql-server-profiler"></a>创建 Transact-SQL 脚本来运行跟踪 (SQL Server Profiler)
  本主题说明了如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]从现有的跟踪文件或表中创建 Transact-SQL 脚本。  
  
### <a name="to-create-a-transact-sql-script-to-run-a-trace"></a>创建 Transact-SQL 脚本来运行跟踪  
  
1.  打开跟踪文件或表。 有关详细信息，请参阅[打开跟踪文件 (SQL Server Profiler)](open-a-trace-file-sql-server-profiler.md) 或[打开跟踪表 (SQL Server Profiler)](open-a-trace-table-sql-server-profiler.md)。  
  
2.  在“文件”菜单上，依次指向“导出”和“脚本跟踪定义”，然后单击与你要跟踪的服务器对应的版本。  
  
3.  在 **“另存为”** 对话框中，输入脚本文件名称，然后单击 **“保存”**。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Profiler 模板和权限](sql-server-profiler-templates-and-permissions.md)   
 [SQL Server 事件探查器](sql-server-profiler.md)  
  
  

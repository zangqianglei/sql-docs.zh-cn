---
title: "更改已注册的服务器或已注册的服务器组的名称 | Microsoft Docs"
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying registered server or server group names
- server groups [SQL Server]
- Registered Servers [SQL Server], names
- renaming registered server or server group
- names [SQL Server], registered server or server group
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: b99eea0ee5988ce791948c2fa7340271b74e7ec4
ms.contentlocale: zh-cn
ms.lasthandoff: 07/31/2017

---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>更改已注册的服务器或已注册的服务器组的名称
  本主题说明如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中更改已注册服务器或服务器组的名称。 该名称可以随时更改。 在已注册的服务器中更改某个服务器的名称只会更改该名称的显示方式。 若要连接到其他服务器，必须编辑已注册的服务器的连接属性。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
从菜单导航到“视图”\\“已注册的服务器”，以打开“已注册的服务器”窗格。  
#### <a name="to-change-the-name-of-a-server"></a>更改服务器的名称  
  
1.  在“已注册的服务器”中，展开“数据库引擎”后，展开“本地服务器组”。  

2.  右键单击某服务器，选择“属性”以打开“编辑服务器注册属性”对话框窗口。
  
3.  在“已注册的服务器名称”文本框中键入用于该服务器注册的新名称，单击“保存”。  
  
#### <a name="to-change-the-name-of-a-server-group"></a>更改服务器组的名称  
  
1.  在“已注册的服务器”中，展开“数据库引擎”后，展开“本地服务器组”。  

2.  右键单击某服务器组，选择“属性”以打开“编辑服务器组属性”对话框窗口。 
  
3.  在“组名称”文本框中键入该服务器组的新名称，单击“保存”。  
  
## <a name="see-also"></a>另请参阅  
 [更改服务器的注册信息 (SQL Server Management Studio)](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)  
  
  

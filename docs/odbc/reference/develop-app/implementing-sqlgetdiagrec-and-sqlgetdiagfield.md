---
title: "实现 SQLGetDiagRec 和 SQLGetDiagField |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 11ba1857-b533-4517-8131-a2a8a0154a0a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 463ddfe552c94a9e90ceb2a24f8061674955979d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="implementing-sqlgetdiagrec-and-sqlgetdiagfield"></a>实现 SQLGetDiagRec 和 SQLGetDiagField
**SQLGetDiagRec**和**SQLGetDiagField**由驱动程序管理器和每个驱动程序实现。 驱动程序管理器和每个驱动程序维护的每个环境、 连接、 语句和的描述符句柄的诊断记录，仅当另一个函数调用与将释放句柄或句柄释放这些记录。  
  
 尽管驱动程序管理器和每个驱动程序必须决定根据中排名第一条状态记录[状态记录序列](../../../odbc/reference/develop-app/sequence-of-status-records.md)，驱动程序管理器确定最终的记录序列。  
  
 **SQLGetDiagRec**和**SQLGetDiagField**不能开机自检有关自身的诊断记录。  
  
 本部分包含以下主题。  
  
-   [诊断处理规则](../../../odbc/reference/develop-app/diagnostic-handling-rules.md)  
  
-   [角色的驱动程序管理器](../../../odbc/reference/develop-app/role-of-the-driver-manager.md)  
  
-   [该驱动程序的角色](../../../odbc/reference/develop-app/role-of-the-driver.md)
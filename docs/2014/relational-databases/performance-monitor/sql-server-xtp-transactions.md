---
title: XTP 事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4dc00c5b6fe238336c626a06057c4fcc304386b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072317"
---
# <a name="xtp-transactions"></a>XTP 事务
  XTP 事务性能对象包含与中的 XTP 引擎事务相关的计数器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 下表介绍**XTP 事务**计数器。  
  
|计数器|Description|  
|-------------|-----------------|  
|**级联中止数/秒**|由于提交依赖关系回滚而每秒回滚的事务数（平均值）。|  
|**采用的提交依赖关系数/秒**|事务每秒采用的提交依赖关系数（平均值）。|  
|**准备好的只读事务数/秒**|准备好进行提交处理的每秒只读事务数。|  
|**保存点刷新次数/秒**|保存点每秒“刷新”的次数（平均值）。 保存点刷新指现有保存点重置为事务生存期中的当前点。|  
|**保存点回滚次数/秒**|事务每秒回滚到保存点的次数（平均值）。|  
|**创建的保存点数/秒**|每秒创建的保存点数（平均值）。|  
|**事务验证失败数/秒**|每秒验证失败的事务数（平均值）。|  
|**用户中止的事务数/秒**|用户每秒中止的事务数（平均值）。|  
|**中止的事务数/秒**|（用户和系统）每秒中止的事务数（平均值）。|  
|**创建的事务数/秒**|系统中每秒创建的事务数（平均值）。<br /><br /> 对 XTP 事务的计数方式不同于基于磁盘的事务（反映在“数据库:事务数/秒”中）。 例如，“创建的事务数/秒”对只读事务进行计数，而“数据库:事务数/秒”则不然。|  
  
## <a name="see-also"></a>请参阅  
 [XTP&#40;内存中 OLTP&#41;性能计数器](../../integration-services/performance/performance-counters.md)  
  
  

---
title: sysssislog (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
author: douglasl
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fe5d4d2b6475c8f46a7d47f3b8106772def6dfb7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689846"
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包或其任务和容器在运行时生成的每个日志记录条目各占一行。 在安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 时，将在 msdb 数据库中创建该表。 如果将日志记录配置为记录到不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，则会在指定的数据库中创建采用此格式的 sysssislog 表。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 此表中写入日志记录条目**仅**包时使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日志提供程序。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|日志记录项的唯一标识符。|  
|事件|**sysname**|生成日志记录项的事件的名称。|  
|computer|**nvarchar**|生成日志记录条目时运行包的计算机。|  
|运算符后的表达式|**nvarchar**|运行生成日志记录条目的包的用户的名称。|  
|源 (source)|**nvarchar**|包中生成日志记录条目的可执行文件的名称。|  
|sourceid|**uniqueidentifier**|包中生成日志记录条目的可执行文件的 GUID。|  
|executionid|**uniqueidentifier**|生成日志记录条目的可执行文件的执行实例的 GUID。|  
|starttime|**datetime**|包开始运行的时间。|  
|endtime|**datetime**|包的完成时间。<br /><br /> 此功能尚未实现。 endtime 列中的值始终与 starttime 列中的值相同。|  
|datacode|**int**|一个可选的整数值，它通常表示运行容器或任务的结果。|  
|databytes|**image**|包含附加信息的可选字节数组。|  
|message|**nvarchar**|事件以及与事件关联的信息的说明。|  
  
## <a name="see-also"></a>请参阅  
 [Integration Services (SSIS) 日志记录](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  

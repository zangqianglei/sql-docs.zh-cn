---
title: srv_setutype（扩展存储过程 API）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_setutype
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b5f1b038d574da6e04fa934d4f4c599966341a7c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217385"
---
# <a name="srvsetutype-extended-stored-procedure-api"></a>srv_setutype（扩展存储过程 API）
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]请改用 CLR 集成。  
  
 为行中的列设置用户定义数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
  
```  
  
## <a name="arguments"></a>参数  
 srvproc  
 指向作为特定客户端连接句柄的 SRV_PROC 结构的指针。 该结构包含扩展存储过程 API 库用于管理应用程序和客户端之间的通信和数据的信息。  
  
 *column*  
 指示要设置的列。 列的编号从 1 开始。  
  
 user_type  
 指定用户定义数据类型的代码。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。 如果相应列不存在，则返回 FAIL。  
  
## <a name="remarks"></a>备注  
 列具有两种数据类型：其实际数据类型及其用户定义数据类型。 用户定义数据类型由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于存储实际的用户定义数据类型的列和（如果有的话）列说明信息，例如，列的为 Null 性和可更新性。  
  
 在使用 srv_describe 定义列后，并且在发送最后一行前，随时都可以调用 srv_setutype 函数。  
  
> [!IMPORTANT]  
>  应全面检查扩展存储过程的源代码，并在生产服务器中安装编译的 DLL 之前，对这些 DLL 进行测试。 有关安全检查和测试的信息，请访问此 [Microsoft 网站](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>请参阅  
 [srv_describe（扩展存储过程 API）](srv-describe-extended-stored-procedure-api.md)  
  
  

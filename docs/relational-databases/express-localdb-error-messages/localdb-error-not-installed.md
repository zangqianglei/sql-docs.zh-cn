---
title: LOCALDB_ERROR_NOT_INSTALLED |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: e7912885-1c14-409b-9022-83ad4c36f3bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b88f152c1c8d7e586f3da3fc5bc0bd2eac8305c2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815845"
---
# <a name="localdberrornotinstalled"></a>LOCALDB_ERROR_NOT_INSTALLED
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|278|  
|事件源|SQL Server 本地数据库运行时 12.0|  
|组件|本地数据库运行时 API|  
|消息正文|注意： 消息文本为空，因为此消息表示整个 LocalDB API （包括将 HRESULTS 映射到消息文本的 FormatMessage 函数） 不可用。|  
  
## <a name="explanation"></a>解释  
 计算机上没有安装本地数据库运行时。  
  
## <a name="user-action"></a>用户操作  
 安装本地数据库运行时，然后重试操作。  
  
  

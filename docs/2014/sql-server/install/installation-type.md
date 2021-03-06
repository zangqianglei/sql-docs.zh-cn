---
title: 安装类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 0420c555-7a3b-42b9-8651-0b4f5bcb0008
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6c91331f93347a860946741229f9b6a287796e03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105607"
---
# <a name="installation-type"></a>安装类型
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导的“安装类型”页可以指定是安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的新实例还是向现有实例中添加功能。  
  
## <a name="options"></a>选项  
 选择指示您所做选择的单选按钮：  
  
-   执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的全新安装  
  
-   向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的现有实例中添加功能  
  
     如果选择与向现有实例中添加功能相对应的选项，则使用下拉列表选择要更新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 您只能向[!INCLUDE[ssDE](../../includes/ssde-md.md)] 的已准备映像添加 SysPrep 支持的功能（ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）。 只有在已准备实例完成后，才能添加 SysPrep 不支持的其他功能。  
  
 **注意** 安装故障转移群集实例之后，不能再向其中添加功能。 若要向现有故障转移群集中添加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，则必须执行全新安装才能安装单独的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
  

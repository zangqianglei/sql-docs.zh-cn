---
title: "了解 Analysis Services 部署脚本 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], scripts
- Analysis Services deployments, scripts
- scripts [Analysis Services], deployment
ms.assetid: a63ebee9-9848-48f1-82ad-64ecf2e47019
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ccc1b2b2861a20de2f02bf118a5abcf14e8ea6b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="understanding-the-analysis-services-deployment-script"></a>了解 Analysis Services 部署脚本
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导生成的 XMLA 部署脚本由两部分组成：  
  
-   部署脚本的第一部分包含创建、更改或删除目标数据库中的相应 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象所需的命令。 默认情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目生成的输入文件基于增量部署。 因此，XMLA 部署脚本将只对那些已更改或删除的对象产生影响。  
  
-   部署脚本的第二部分包含仅处理在目标服务器上创建或更改的对象（“处理默认值”选项）或完全处理目标数据库所需的命令。 还可以选择使部署脚本不包含任何处理命令。  
  
 整个部署脚本可以在单个事务或多个事务内执行。 如果脚本在多个事务内执行，则脚本的第一部分作为单个事务执行，并且每个对象都在其自己的事务内进行处理。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导仅将对象部署到单个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中。 该向导不会部署任何服务器级别对象或数据。  
  
## <a name="see-also"></a>另请参阅  
 [运行 Analysis Services 部署向导](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [了解用于创建部署脚本的输入文件](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
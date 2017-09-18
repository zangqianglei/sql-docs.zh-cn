---
title: "将包复制 SQL Server Data Tools 中 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 59a001e0aa360183e5e393faedc613cfabda0f02
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="copy-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中复制包
  此主题介绍如何通过复制现有包来创建新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包，以及如何更新新包的 **Name** 和 **GUID** 属性。  
  
### <a name="to-copy-a-package"></a>复制包  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开含有要复制的包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击包。  
  
3.  验证已在解决方案资源管理器中选择要复制的包，或者包含该包的 SSIS 设计器的选项卡是活动的选项卡。  
  
4.  上**文件**菜单上，单击**保存\<包名称 > 作为**。  
  
    > [!NOTE]  
    >  必须在 SSIS 设计器中打开包，然后“另存为”选项才会出现在“文件”菜单中。  
  
5.  （可选）浏览到其他文件夹。  
  
6.  更新包文件的名称。 确保保留 .dtsx 文件扩展名。  
  
7.  单击 **“保存”**。  
  
8.  在出现提示时，选择是否更新包对象的名称，使其与文件名匹配。 如果单击 **“是”**，将更新包的 **Name** 属性。 新的包将添加到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，并在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开。  
  
9. （可选）单击 **“控制流”** 选项卡的背景，并单击 **“属性”**。  
  
10. 在属性窗口中，单击值 ID 属性，然后在下拉列表中，单击**\<生成新的 ID >**。  
  
11. 在 **“文件”** 菜单上，单击 **“保存选定项”** ，以保存新建的包。  
  
## <a name="see-also"></a>另请参阅  
 [保存包的副本](http://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [在 SQL Server Data Tools 中创建包](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS &#41;包](../integration-services/integration-services-ssis-packages.md)  
  
  
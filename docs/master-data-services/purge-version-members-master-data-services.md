---
title: "清除版本成员 (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 56cccc3f368f17118dece215275fbe23822e9040
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="purge-version-members-master-data-services"></a>清除版本成员 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，删除成员仅将其停用或软删除。 数据仍驻留在数据库中。 本主题介绍如何在模型版本中清除（永久删除）所有软删除的成员。  
  
## <a name="prerequisites"></a>先决条件  
 执行此过程。  
  
-   你必须有权访问“版本管理”功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
## <a name="to-purge-soft-deleted-members"></a>清除软删除的成员  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“版本管理”**。  
  
2.  在“管理版本”  页上，选择与要清除的版本对应的模型。 随后显示模型版本的列表。  
  
3.  选择与要清除的版本对应的行。  
  
4.  单击“清除成员” 。  
  
5.  在确认提示中单击“确定”。  
  
## <a name="additional-methods-to-purge-members"></a>清除成员的其他方法  
 清除版本成员会永久删除与所选版本相关的所有实体中的软删除成员。 更精细的替代方法是使用实体基本暂存，仅永久删除实体的特定成员。 此外，具有资源管理器功能权限的实体管理员可能会清除实体资源管理器页中的实体版本。  
  
 有关详细信息，请参阅[叶成员临时表 (Master Data Services)](../master-data-services/leaf-member-staging-table-master-data-services.md)。  
  
  
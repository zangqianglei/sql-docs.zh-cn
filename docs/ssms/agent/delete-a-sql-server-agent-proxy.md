---
title: "删除 SQL Server 代理程序代理 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8371f1b086c15881e6cfd125194038d5c8245b72
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-sql-server-agent-proxy"></a>删除 SQL Server 代理程序代理
本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 中删除 [!INCLUDE[tsql](../../includes/tsql_md.md)]代理的代理帐户。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要删除 SQL Server 代理的代理帐户，可使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理帐户时，请确保该代理未引用任何活动的作业步骤。 若要检查是否有引用该代理的作业步骤，请右键单击该代理，选择“属性”，然后在“proxy_name 代理帐户属性”对话框中选择“引用”页。 如果删除某个代理，在 **“删除对象”** 对话框中会出现一个用于重新分配使用该代理的所有作业步骤的选项。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的代理帐户使用凭据存储 Windows 用户帐户的相关信息。 凭据中指定的用户必须对正在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的计算机具有“以批处理作业登录”权限。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理检查代理帐户的子系统访问权限，并在每次运行作业步骤时向代理帐户授予访问权限。 如果代理对子系统不再具有访问权限，则作业步骤将失败。 否则， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理将模拟代理帐户中指定的用户并运行作业步骤。  
  
-   如果用户的登录帐户具有访问代理帐户的权限，或者用户属于具有访问代理帐户的权限的任何角色，则用户可以在作业步骤中使用代理帐户。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
只有 **sysadmin** 固定服务器角色的成员才能创建、修改或删除代理帐户。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>删除 SQL Server 代理的代理帐户  
  
1.  在 **“对象资源管理器”**中，单击加号以展开包含要删除的代理帐户的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以便展开 **“代理”** 文件夹。  
  
4.  单击加号以展开包含要删除的代理帐户的子系统（例如，“ActiveX 脚本”）。  
  
5.  右键单击要删除的代理帐户，然后选择“删除”。  
  
6.  在 **“删除对象”** 对话框中，确认选择了正确的代理帐户。 选中 **“重新分配给”** 复选框以向其他帐户重新分配引用此代理帐户的作业步骤。  
  
7.  单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>删除 SQL Server 代理的代理帐户  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_delete_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/44a1db13-b7f2-4dab-a1b5-b8dafb41737c)。  
  

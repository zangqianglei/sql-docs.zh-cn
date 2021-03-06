---
title: sp_scriptdynamicupdproc (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_scriptdynamicupdproc_TSQL
- sp_scriptdynamicupdproc
helpviewer_keywords:
- sp_scriptdynamicupdproc
ms.assetid: b4c18863-ed92-4aa2-a04f-7ed832fc9e07
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8675cc6e79bbfd78b82abb756a6de80cd33d54d6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47627915"
---
# <a name="spscriptdynamicupdproc-transact-sql"></a>sp_scriptdynamicupdproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  生成创建动态更新存储过程的 CREATE PROCEDURE 语句。 自定义存储过程中的 UPDATE 语句是基于 MCALL 语法动态生成的，它指示要更改的列。 如果订阅表中的索引数不断增加，并且被更改列的数目很小，请使用此存储过程。 此存储过程在发布服务器的发布数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_scriptdynamicupdproc [ @artid =] artid  
```  
  
## <a name="arguments"></a>参数  
 [  **@artid=**] *artid*  
 文章 id。 *artid*是**int**，无默认值。  
  
## <a name="result-sets"></a>结果集  
 返回一个结果集包含单个**nvarchar(4000)** 列。 该结果集构成了用于创建自定义存储过程的完整 CREATE PROCEDURE 语句。  
  
## <a name="remarks"></a>备注  
 **sp_scriptdynamicupdproc**事务复制中使用。 默认的 MCALL 脚本编写逻辑包括 UPDATE 语句中的所有列，并使用一个位图来确定已更改的列。 如果某列未更改，则将其恢复回自身，这种做法通常不会导致任何问题。 如果该列被索引，则需要进行额外的处理。 动态方法仅包括已更改的列，这样可提供一个最优的 UPDATE 字符串。 然而，生成动态 UPDATE 语句时会在运行时发生额外处理。 建议您先测试动态方法和静态方法，然后选择最佳解决方案。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_scriptdynamicupdproc**。  
  
## <a name="examples"></a>示例  
 此示例将创建一个项目 (与*artid*设置为**1**) 上**作者**表中**pubs**数据库，并指定更新语句是要执行的自定义过程：  
  
```  
'MCALL sp_mupd_authors'  
```  
  
 通过在发布服务器运行下列存储过程，生成将由订阅服务器中的分发代理执行的自定义存储过程：  
  
```  
EXEC sp_scriptdynamicupdproc @artid = '1'  
  
The statement returns:  
  
CREATE PROCEDURE [sp_mupd_authors]   
  @c1 varchar(11),@c2 varchar(40),@c3 varchar(20),@c4 char(12),@c5 varchar(40),@c6 varchar(20),  
  @c7 char(2),@c8 char(5),@c9 bit,@pkc1 varchar(11),@bitmap binary(2)  
as  
  
declare @stmt nvarchar(4000), @spacer nvarchar(1)  
SELECT @spacer =N''  
SELECT @stmt = N'UPDATE [authors] SET '  
  
if substring(@bitmap,1,1) & 2 = 2  
begin  
  select @stmt = @stmt + @spacer + N'[au_lname]' + N'=@2'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 4 = 4  
begin  
  select @stmt = @stmt + @spacer + N'[au_fname]' + N'=@3'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 8 = 8  
begin  
  select @stmt = @stmt + @spacer + N'[phone]' + N'=@4'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 16 = 16  
begin  
  select @stmt = @stmt + @spacer + N'[address]' + N'=@5'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 32 = 32  
begin  
  select @stmt = @stmt + @spacer + N'[city]' + N'=@6'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 64 = 64  
begin  
  select @stmt = @stmt + @spacer + N'[state]' + N'=@7'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 128 = 128  
begin  
  select @stmt = @stmt + @spacer + N'[zip]' + N'=@8'  
  select @spacer = N','  
end  
if substring(@bitmap,2,1) & 1 = 1  
begin  
  select @stmt = @stmt + @spacer + N'[contract]' + N'=@9'  
  select @spacer = N','  
end  
select @stmt = @stmt + N' where [au_id] = @1'  
exec sp_executesql @stmt, N' @1 varchar(11),@2 varchar(40),@3 varchar(20),@4 char(12),@5 varchar(40),  
                             @6 varchar(20),@7 char(2),@8 char(5),@9 bit',@pkc1,@c2,@c3,@c4,@c5,@c6,@c7,@c8,@c9  
  
if @@rowcount = 0  
   if @@microsoftversion>0x07320000  
      exec sp_MSreplraiserror 20598  
```  
  
 运行此存储过程后，可以使用生成的脚本在订阅服务器手动创建存储过程。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

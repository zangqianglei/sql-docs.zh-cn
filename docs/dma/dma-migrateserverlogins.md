---
title: 迁移 SQL Server 登录名使用数据迁移助手 |Microsoft Docs
description: 了解如何迁移 SQL Server 登录名使用数据迁移助手
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 3e9e6dad97bbfb2010f71e9e056da8a0912a4506
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2018
ms.locfileid: "49643805"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>迁移 SQL Server 登录名使用数据迁移助手

本文概述了使用数据迁移助手迁移 SQL Server 登录名。 

## <a name="which-logins-are-migrated"></a>哪些登录名迁移

- 你可以迁移基于 Windows 主体 （例如域用户或 Windows 域组） 的登录名。 您也可以迁移基于 SQL 身份验证，也称为 SQL Server 登录名创建登录名。

- 数据迁移助手当前不支持与独立的安全证书 （登录名映射到证书）、 独立的非对称密钥 （登录名映射到非对称密钥） 和登录名映射到凭据的登录名。

- 并不移动数据迁移助手**sa**名称括在双引号哈希将与登录名和服务器原则 (\#\#)，这是仅供内部使用。

- 默认情况下，数据迁移助手选择所有限定登录名迁移。 或者，您可以选择要迁移的特定登录名。 当数据迁移助手迁移限定的所有登录名时，登录用户映射中保持不变将迁移的数据库。 

  如果你打算迁移特定的登录名，请务必选择映射到选择用于迁移的数据库中的一个或多个用户的登录名。

- 作为登录名迁移的一部分，数据迁移助手还将移动用户定义的服务器角色并将服务器级权限添加到用户定义的服务器角色。 该角色的所有者将设置为**sa**主体。

## <a name="during-and-after-migration"></a>迁移期间和之后

- 作为登录名迁移的一部分，数据迁移助手将权限分配给目标 SQL Server 上的安全对象存在于源 SQL Server 上。 

  如果在目标 SQL Server 上已存在登录名，数据迁移助手会迁移仅分配给安全对象的权限并不会重新创建整个登录名。

- 数据迁移助手可最大程度地将登录名映射到数据库用户，如果目标服务器上已存在登录名。

- 建议您查看迁移结果以了解的登录名迁移和任何建议的迁移后操作的总体状态。

## <a name="resources"></a>Resources

[数据迁移助手 (DMA)](../dma/dma-overview.md)

[数据迁移助手： 配置设置](../dma/dma-configurationsettings.md)

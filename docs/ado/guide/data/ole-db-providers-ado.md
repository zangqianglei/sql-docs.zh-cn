---
title: OLE DB 访问接口 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3f4f1d4efed51a8f9e3b5eaf3bd4a2c7f385e75
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613805"
---
# <a name="ole-db-providers-ado"></a>OLE DB 提供程序 (ADO)
OLE DB 定义一组 COM 接口，从而提供对存储在各种信息源中的数据进行统一访问的应用程序。 这种方法可以将数据源以共享其数据通过支持的 DBMS 功能适用于数据源的接口。 根据设计，OLE DB 的高性能体系结构基于其使用的灵活的、 基于组件的服务模型。 而不是让规定的数量的应用程序和数据之间的中间层，OLE DB 要求仅在所需的组件完成特定任务。  
  
 例如，假设用户想要运行查询。 请考虑下列情形：  
  
-   数据驻留在关系数据库中当前存在的 ODBC 驱动程序，但没有本机 OLE DB 访问接口： 应用程序使用 ADO 与 OLE DB 访问接口对于 ODBC，然后将加载相应的 ODBC 驱动程序。 该驱动程序将 SQL 语句传递给 DBMS，检索数据。  
  
-   数据驻留在 Microsoft SQL Server 没有本机 OLE DB 访问接口： 应用程序使用 ADO 来直接与 OLE DB 访问接口的 Microsoft SQL Server 进行通信。 没有中间方是必需的。  
  
-   数据驻留在 Microsoft Exchange Server 的 OLE DB 提供程序，但不公开到过程的 SQL 查询引擎： 应用程序使用 ADO 与 OLE DB 访问接口的 Microsoft Exchange 和 OLE DB 查询处理器将调用若要处理查询的组件。  
  
-   数据驻留在 Microsoft NTFS 文件系统中的文档的形式： 使用本机 OLE DB 访问接口通过 Microsoft 索引服务，该文件系统，从而启用有效的内容中的索引的内容和文档的属性访问数据搜索。  
  
 在所有上述示例中，应用程序可查询的数据。 用户的需求符合最小组件数。 每种情况下，仅在需要时，使用其他组件和调用所需的组件。 使用 OLE DB，可重用和共享组件的此按需加载极大地影响到高性能。  
  
 提供程序分为两类： 提供数据和提供服务。 数据提供程序拥有其自己的数据，并公开以表格形式向你的应用程序。 服务提供商对服务进行封装生成和使用数据，并增加 ADO 应用程序中的功能。 此外可以将服务提供商进一步定义为服务组件，必须在与其他服务提供程序或组件一起工作。  
  
 ADO 提供一致的与各种 OLE DB 访问接口的较高级别接口。  
  
 本部分包含以下主题。  
  
-   [数据提供程序](../../../ado/guide/data/data-providers.md)  
  
-   [服务提供商和组件](../../../ado/guide/data/service-providers-and-components.md)

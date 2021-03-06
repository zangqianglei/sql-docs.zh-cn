---
title: 动态游标 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0d7a19476a00fb88e0b2195c761993f91b7a5d4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838325"
---
# <a name="dynamic-cursors"></a>动态游标
动态游标检测结果集中，而不考虑是否发生的更改从内部游标或游标以外的其他用户的行所做的所有更改。 所有的 insert、 update 和 delete 语句所做的所有用户都通过游标可见。 动态游标可以检测到的行、 顺序和中的结果集打开游标后的值所做的任何更改。 游标外部所做的更新不可见，直到提交 （除非游标事务隔离级别设置为"未提交"）。  
  
 例如，假设动态游标提取两个行和另一个应用程序，然后更新这些行之一和删除其他。 如果动态游标然后提取这些行，它将找不到已删除的行，但它将显示已更新的行的新值。  
  
 动态游标是一个不错的选择，如果你的应用程序必须检测到其他用户所做的所有并发更新。 使用**adOpenDynamic CursorTypeEnum**以指示你想要使用动态游标在 ADO 中。  
  
## <a name="see-also"></a>请参阅  
 [只进游标](../../../ado/guide/data/forward-only-cursors.md)   
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [键集游标](../../../ado/guide/data/keyset-cursors.md)

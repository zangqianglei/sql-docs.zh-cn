---
title: 优先约束中使用表达式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence constraints [Integration Services], adding expressions
- expressions [Integration Services], adding
ms.assetid: 601038bb-3b17-42ac-b09d-5b3a82fb6564
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5dd09ba81c6bdf79abdb5d668821442fad7acab0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114603"
---
# <a name="use-an-expression-in-a-precedence-constraint"></a>在优先约束中使用表达式
  此过程介绍如何使用 **“优先约束编辑器”** 对话框将表达式添加到优先约束中。 包中必须包含至少两个可执行文件（可以是任务或容器），并且它们必须由优先约束连接起来，才能将表达式添加到优先约束。  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>将表达式添加到优先约束  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  在“控制流”选项卡的设计图面上双击优先约束。 **“优先约束编辑器”** 将打开。  
  
5.  在 **“求值运算”** 列表中选择 **“表达式”**、 **“表达式和约束”** 或者 **“表达式或约束”** 。  
  
6.  在 **“表达式”** 文本框中键入表达式，或启动表达式生成器来创建表达式。  
  
7.  若要验证表达式语法，请单击 **“测试”**。  
  
8.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [优先约束](control-flow/precedence-constraints.md)   
 [使用默认优先约束来连接任务和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [使用快捷菜单设置优先约束的值](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [设置优先约束的属性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)  
  
  

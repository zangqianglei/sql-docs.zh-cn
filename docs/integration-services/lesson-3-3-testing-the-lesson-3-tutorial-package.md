---
title: 步骤 3：测试第 3 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca00f40146d5019f770e3141d3961e40ed526ccc
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559155"
---
# <a name="lesson-3-3---testing-the-lesson-3-tutorial-package"></a>第 3-3 课 - 测试第 3 课教程包
在该任务中，将运行 Lesson 3.dtsx 包。 在包运行时，“日志事件”窗口将列出写入日志文件中的日志条目。 执行完包之后，将验证日志提供程序所生成的日志文件的内容。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
测试包之前，应当确保 Lesson 3 包中的控制流和数据流包含下列关系图中显示的对象。 控制流应与第 2 课中的控制流相同。 数据流应与第 1 课和第 2 课中的数据流相同。  
  
**控制流**  
  
![包中的控制流](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### <a name="to-run-the-lesson-3-tutorial-package"></a>运行第 3 课教程包  
  
1.  在 SSIS 菜单中，单击“日志事件”。  
  
2.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
3.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
### <a name="to-examine-the-generated-log-file"></a>检查生成的日志文件  
  
-   使用记事本或其他任何文本编辑器，打开 TutorialLog.log 文件。  
  
-   尽管为 **PipelineExecutionPlan** 和 **PipelineExecutionTrees** 事件所生成的信息的语义超出了本教程的讨论范围，但是，可以看到第一行列出了在 **“配置 SSIS 日志”** 对话框的 **“详细信息”** 选项卡中所指定的信息字段。 此外，可以验证已为 Foreach 循环的每个迭代记录了所选择的两个事件：PipelineExecutionPlan 和 PipelineExecutionTrees。  
  
## <a name="next-lesson"></a>下一课  
[第 4 课：使用 SSIS 添加错误流重定向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  

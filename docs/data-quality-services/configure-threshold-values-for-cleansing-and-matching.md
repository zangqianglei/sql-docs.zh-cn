---
title: "配置清理和匹配活动的阈值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.admin.config.general.f1"
helpviewer_keywords: 
  - "清理, 阈值"
  - "清理阈值"
  - "匹配, 阈值"
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 配置清理和匹配活动的阈值
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中配置在计算机辅助清理和匹配活动中使用的阈值。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_administrator 角色才能配置这些阈值。  
  
##  <a name="Configure"></a> 配置阈值  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [运行数据质量客户端应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“配置”**。  
  
3.  接下来，单击 **“常规设置”** 选项卡。 通过此选项卡可以为清理活动以及匹配活动指定阈值。  
  
4.  若要为清理活动指定阈值，请在 **“交互式清理”** 区域下的以下各框中指定适当的值：  
  
    -   **用于建议的最低分数**︰ 最低分数或置信度，将由 DQS 在计算机辅助的清理过程建议替换值。 以相应百分比值的小数表示形式输入一个值。 例如，对于 75% 键入 0.75。 该值应小于或等于在 **“用于自动更正的最低分数”** 框中指定的值。 默认值为 0.7。  
  
    -   **用于自动更正的最低分数**︰ 最低分数或置信度，将由 DQS 用于自动更正值在计算机辅助的清理过程。 以相应百分比值的小数表示形式输入一个值。 例如，对于 90% 输入 0.9。 默认值为 0.8。  
  
5.  若要为匹配活动指定阈值，请在 **“匹配”** 区域下的 **“最低记录分数”** 框中指定一个值。 此值表示一条记录要被视为另一条记录的匹配项的最低分数。 默认值为 80%。  
  
6.  单击 **“关闭”**。  
  
  
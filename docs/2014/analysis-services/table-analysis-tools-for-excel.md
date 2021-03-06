---
title: Excel 表分析工具 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- getting started
ms.assetid: 6d9d1481-18e4-4108-9efa-68152b0940c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da1d5ceae73ae17f9e3689a13c21619dac5fbc93
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049067"
---
# <a name="table-analysis-tools-for-excel"></a>Excel 表分析工具
  中的数据挖掘工具**分析**工具栏是开始使用数据挖掘的最简单方法。 每个工具都会对您的数据的分布和类型自动进行分析，并且设置参数以确保结果有效。 您就无需选择某一算法或配置复杂的参数。  
  
 ![DM](media/dm-tabletoolsanalyze.gif "DM")  
  
 **分析**功能区包含以下工具：  
  
 [分析关键影响因素&#40;Excel 表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 您选择感兴趣的列或输出值，然后算法将分析所有输入数据，以便标识对目标影响最大的因素。 或者，您可以创建比较任何两个值的报告，以便可以看到影响因素是如何变化的。  
  
 **分析关键影响因素**工具使用 Microsoft 朴素贝叶斯算法。  
  
 [检测类别&#40;Excel 表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)  
 通过该工具，可以添加任何数据集和应用聚类分析来找到数据分组。 它用于找到相似之处和创建组以便进一步分析。  
  
 **检测类别**工具使用 Microsoft 聚类分析算法。  
  
 [从示例填充&#40;Excel 表分析工具&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
 这种工具可帮助您归结缺失值的原因。 您提供缺失值应该是什么的一些示例，该工具将基于表中的所有数据生成模式，然后基于数据中的模式建议新值。  
  
 **从示例填充**工具使用 Microsoft 逻辑回归算法。  
  
 [预测&#40;Excel 表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)  
 该工具使用随时间变化的数据，并预测将来值。  
  
 **预测**工具使用 Microsoft 时序算法。  
  
 [突出显示异常值&#40;Excel 表分析工具&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
 该工具对数据表中的模式进行分析，查找不适合该模式的行和值。 然后，您可以查看和更正它们并重新运行模型，或者对值进行标记以便以后执行操作。  
  
 **突出显示异常**工具使用 Microsoft 聚类分析算法。  
  
 [目标查找应用场景&#40;Excel 表分析工具&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
 在中**目标查找**工具，您指定一个目标值，并且该工具标识必须更改才能满足该目标的潜在因素。 例如，如果您知道必须将电话满意度增加 20%，则可以要求模型预测应进行变化以便实现该目标的因素。  
  
 **目标查找**工具使用 Microsoft 逻辑回归算法。  
  
 [假设方案&#40;Excel 表分析工具&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
 **模拟分析**工具补充**目标查找**工具。 使用此工具，您输入要更改的值，并且模型将预测该更改是否足以实现预期结果。 例如，您可以要求该模型推断再增加一名电话接线员是否可以将客户满意度增加一个百分点。  
  
 **假设**工具使用 Microsoft 逻辑回归算法。  
  
 [预测计算器&#40;Excel 表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 此工具创建一个模型，该模型分析导致目标结果的因素，然后根据从数据得出的评分规则，预测任何新输入的结果。 此工具还生成一个交互式决策工作表，通过它，可轻松地为新输入评分。 您还可以创建评分工作表的打印版本，以供脱机使用。  
  
 **预测计算器**工具使用 Microsoft 逻辑回归算法。  
  
 [购物篮分析&#40;Excel 表分析工具&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
 此工具可找出可用于交叉销售或增售中的模式。 它可找出经常一起购买的几组产品，还可根据相关成组产品的价格和成本生成报告以帮助作出决策。  
  
 此工具不仅限于购物篮分析；还可将其应用于任何自身参与关联分析的问题。 例如，可查找经常一起发生的事件、导致诊断的因素或任何其他各组原因和结果。  
  
 **购物篮分析**工具使用 Microsoft 关联算法。  
  
## <a name="requirements-for-the-table-analysis-tools-for-excel"></a>Excel 表分析工具的要求  
 若要使用 Excel 表分析工具，必须首先与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。 通过此连接可以访问用于分析数据的 Microsoft 数据挖掘算法。 如果您无权访问实例，则建议您让管理员设置一个您可用于试验数据挖掘的实例。 有关详细信息，请参阅[连接到源数据&#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 若要使用表分析工具来处理数据，必须将想要使用的数据范围转换为 Excel 表。  
  
 如果无法看到**分析**功能区中，请尝试在某个数据表中第一次单击。 在选择某一数据表之前将不会激活该菜单。  
  
## <a name="see-also"></a>请参阅  
 [Excel 数据挖掘客户端&#40;SQL Server 数据挖掘外接程序&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)   
 [解决 Visio 数据挖掘关系图问题&#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)   
 [Office 数据挖掘外接程序中包含的功能](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  

---
title: "表格模型 (SSAS 表格) 中的 DAX |Microsoft 文档"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2693985-1bea-4861-a100-cea4761ba809
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 653c715b8a3b990cc6073b2455887232c71c32b4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dax-in-tabular-models-ssas-tabular"></a>表格模型 (SSAS 表格) 中的 DAX
  数据分析表达式 (DAX) 是用于分析服务、 Power BI Desktop 中，和在 Excel 中的 Power Pivot 中创建自定义计算的公式语言。 DAX 公式包括一些函数、运算符和值，用于对表和列中的数据执行高级计算。  
  
 尽管 DAX Analysis Services、 Power BI Desktop 和 Excel 中的 Power Pivot 中使用的则本主题更适用于 Analysis Services 表格模型项目创作 SQL Server Data Tools (SSDT) 中。  
  
##  <a name="bkmk_DAX"></a> DAX formulas in calculated columns, measures, and row filters  
 对于在 SSDT 中创作的表格模型，DAX 公式用于计算的列、 度量值和行筛选器。  
  
### <a name="calculated-columns"></a>计算列  
 计算的列是您将添加到现有表 （在模型设计器），然后创建 DAX 公式来定义列的值的列。 
  
> [!NOTE]  
>  使用 DirectQuery 模式从关系数据源检索数据的模型不支持计算列。  
  
 当计算列包含有效的 DAX 公式时，一输入公式就会为每行计算值。 值随后存储在数据库中。 例如，在 Date 表中，在公式栏中输入公式 `=[Calendar Year] & " Q" & [Calendar Quarter]` 时，将通过从 Calendar Year 列（在同一 Date 表中）中取值，添加一个空格和大写字母 Q，然后添加 Calendar Quarter 列（在同一 Date 表中）中的值，为该表中的每行计算值。 系统将立即计算并显示计算列中每行的结果，例如，显示为 **2010 Q1**。 仅当重新处理数据时才会重新计算列值。  
  
 有关详细信息，请参阅 [计算列](../../analysis-services/tabular-models/ssas-calculated-columns.md)中创建的表格模型项目。  
  
### <a name="measures"></a>度量值组  
 度量值是结果随上下文而变化的动态公式。 度量值用于在报表格式中，支持组合，并通过使用多个属性，如 Power BI 报表或 Excel 数据透视表或数据透视图筛选模型数据。 通过使用模型设计器在 SSDT 中的度量值网格 （和公式栏），由模型作者定义度量值。  
  
 度量值中的公式可以使用标准聚合函数（通过使用 COUNT 或 SUM 之类的自动求和功能自动创建），您也可以通过使用 DAX 定义自己的公式。 在公式栏中为某一度量值定义公式时，工具提示功能会显示当前上下文中的总结果预览，但除此之外，在任何位置都不会立即输出结果。 其他度量值详细信息也会显示在 **“属性”** 窗格中。  
  
 您不能立即看到计算的（筛选）结果的原因是，在没有上下文的情况下无法确定度量值的结果。 若要计算度量值，需要一个可以提供上下文的报表客户端应用程序，在检索与每个单元相关的数据然后针对每个单元计算表达式时需要该应用程序提供的上下文。 该客户端可能是 Excel 数据透视表或数据透视图、 Power BI 报表或 MDX 查询。 无论报表客户端是什么，都会对结果中的每个单元运行单独的查询。 也就是说，每个行和列数据透视表中的标头组合或切片器和筛选器在 Power BI 报表中，每个所选生成不同的计算度量值的数据子集。 例如，在具有该公式的度量值`Total Sales:=SUM([Sales Amount])`，当用户将总销售额度量值放置在数据透视表，值窗口中，然后位置从 DimProduct 表到筛选器窗口中，Sales Amount 的总和 DimProductCategory 列计算并显示每个产品类别。  
  
 与计算列和行筛选器不同，度量值的语法中在公式之前包括该度量值的名称。 在刚才提供的示例中，名称 **Total Sales:** 显示在公式之前。 创建一个度量值后，其名称和定义将显示在报表客户端应用程序的“字段”列表中，可供模型的所有用户使用（具体取决于透视和角色）。  
  
 有关详细信息，请参阅 [度量值组](../../analysis-services/tabular-models/measures-ssas-tabular.md)中创建的表格模型项目。  
  
### <a name="row-filters"></a>行筛选器  
 行筛选器定义表中对特定角色的成员可见的行。 通过使用 DAX 公式可为模型中的每个表创建行筛选器。 在 SSDT 中使用角色管理器，对特定角色创建行筛选器。 行筛选器还可以为已部署的模型通过使用 SQL Server Management Studio (SSMS) 中的角色属性定义。  
  
 在行筛选器中，DAX 公式（求值结果必须为 TRUE/FALSE 布尔值条件）定义该特定角色的成员执行查询的结果可返回的行。 不能返回未包含在 DAX 公式中的行。 例如，对于具有以下 DAX 公式 `=Customers[Country] = “USA”`的 Customers 表，Sales 角色的成员将只能查看美国境内客户的数据和聚合值，例如仅为美国客户返回 SUM。  
  
 使用 DAX 公式定义行筛选器时，您将创建一个允许的行集。 这并不影响访问其他行；其他行只是不会作为允许的行集的一部分返回。 其他角色可允许访问 DAX 公式所排除的行。 如果某用户是其他角色的成员，并且该角色的行筛选器允许访问该特定行集，则该用户可以查看该行的数据。  
  
 行筛选器应用于指定的行以及相关行。 如果表具有多个关系，则筛选器将安全性应用于处于活动状态的关系。 行筛选器将与为相关表定义的其他行筛选器相交。  
  
 有关详细信息，请参阅[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)。  
  
##  <a name="bkmk_DAX_datatypes"></a> DAX 数据类型  
 您可以将数据从可能支持不同数据类型的众多不同数据源导入到模型中。 将数据导入模型时，数据将转换为表格模型数据类型之一。 当在计算中使用模型数据时，数据则会因计算的持续时间和输出而转换为 DAX 数据类型。 当您创建一个 DAX 公式时，该公式中使用的项将自动确定返回的值数据类型。  
  
 表格模型和 DAX 支持下列数据类型：  
  
|模型中的数据类型|DAX 中的数据类型|Description|  
|------------------------|----------------------|-----------------|  
|整数|一个 64 位（八字节）整数值 <sup>1、2</sup>|没有小数位的数字。 整数可以是正数或负数，但必须是介于 -9,223,372,036,854,775,808 (-2^63) 和 9,223,372,036,854,775,807 (2^63-1) 之间的整数。|  
|小数|一个 64 位（八字节）实数 <sup>1、2</sup>|实数是可具有小数位的数字。 实数涵盖很广范围的值：<br /><br /> 从 -1.79E +308 到 -2.23E -308 的负值<br /><br /> 零<br /><br /> 从 2.23E -308 到 1.79E + 308 的正值<br /><br /> 但是，有效位数限制为 17 个小数位。|  
|Boolean|Boolean|True 或 False 值。|  
|Text|字符串|一个 Unicode 字符数据字符串。 可以是字符串，或以文本格式表示的数字或日期。|  
|日期|日期/时间|采用接受的日期-时间表示形式的日期和时间。<br /><br /> 有效值是 1900 年 3 月 1 日后的所有日期。|  
|货币|货币|货币数据类型允许值介于 -922,337,203,685,477.5808 到 922,337,203,685,477.5807 之间，并且具有四个小数位的固定精度。|  
|N/A|空白|空白是 DAX 中的一种数据类型，表示并替代 SQL 中的 Null。 您可以通过使用 BLANK 函数创建空白，并通过使用逻辑函数 ISBLANK 测试是否存在空白。|  
  
 表格模型还包括 Table 数据类型，作为许多 DAX 函数的输入或输出。 例如，FILTER 函数采用表作为输入，并输出仅包含满足筛选条件的行的另一个表。 通过组合表函数与聚合函数，您可以对动态定义的数据集执行复杂计算。  
  
 尽管数据类型通常都是自动设置的，但还是需要了解数据类型，尤其是它们如何应用到 DAX 公式，这一点非常重要。 举例来说，公式中的错误或是意外结果通常都是因为对参数中指定的数据类型使用了不该使用的特定运算符而导致的。 例如，公式 `= 1 & 2`返回结果为 12 的字符串。 但是公式 `= “1” + “2”`返回的结果为整数 3。  
  
 有关中表格模型和 DAX 中的数据类型的显式和隐式转换的数据类型的详细信息，请参阅[数据类型支持](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)。  
  
##  <a name="bkmk_DAX_opertors"></a> DAX 运算符  
 DAX 语言在公式中使用四种不同类型的运算符：  
  
-   对值进行比较，并返回一个逻辑 TRUE\FALSE 值的比较运算符。  
  
-   执行返回数值的算术运算的算术运算符。  
  
-   联接两个或更多文本字符串的文本连接运算符。  
  
-   将两个或更多表达式组合起来以返回单个结果的逻辑运算符。  
  
 有关在 DAX 公式中使用的运算符的详细信息，请参阅 [DAX 运算符参考](http://msdn.microsoft.com/en-us/1befbddc-6178-472c-8bc4-05dafd62207e)。  
  
##  <a name="bkmk_DAX_Formulas"></a> DAX formulas  
 DAX 公式对于在计算列和度量值中创建计算以及使用行级别筛选器保护数据方面非常重要。 若要创建用于计算的列和度量值公式，你将使用的模型设计器窗口或 DAX 编辑器顶部的公式栏。 若要创建用于行筛选器的公式，您需要使用“角色管理器”对话框。 本节中的信息旨在帮助您开始了解 DAX 公式的基础知识。  
  
###  <a name="basics"></a> Formula basics  
 利用 DAX，表格模型作者既可以将自定义计算定义为模型表中的计算列的一部分，也可以将其定义为与表关联但不直接显示在表中的度量值。 DAX 还支持模型作者保护数据，因为 DAX 支持创建返回布尔值的计算，由布尔值定义可供关联角色的成员用户查询的特定或相关表中的行。  
  
 DAX 公式可以很简单，也可以很复杂。 下表显示了可以在计算列中使用的简单公式的一些示例。  
  
|||  
|-|-|  
|公式|Description|  
|`=TODAY()`|将今天的日期插入列中的每一行。|  
|`=3`|将值 3 插入列中的每一行。|  
|`=[Column1] + [Column2]`|将 [Column1] 和 [Column2] 的同一行中的值相加，并且将结果放置于同一行的计算列中。|  
  
 无论您创建的公式是繁是简，您都可以在构建公式时使用以下步骤：  
  
1.  每个公式必须以等号开头。  
  
2.  可以键入或选择一个函数名称，也可以键入一个表达式。  
  
3.  开始键入所需函数或名称的前几个字母，记忆式键入功能将显示可用函数、表和列的列表。 按 Tab 从记忆式键入列表向公式中添加项。  
  
     还可以单击 **Fx** 按钮显示可用函数的列表。 若要从下拉列表中选择某一函数，请使用箭头键突出显示该项，然后单击 **“确定”** 将该函数添加到公式中。  
  
4.  通过从可能的表和列的下拉列表中选择参数，或者通过键入值，向函数提供参数。  
  
5.  检查是否有语法错误：确保所有括号都成对出现且正确引用列、表和值。  
  
6.  按 Enter 以接受该公式。  
  
> [!NOTE]  
>  在计算列中，只要您输入的公式，该公式将进行验证，则使用值填充列。 在度量值中，按 Enter 可在表的度量值网格中保存度量值定义。 如果公式无效，将会显示错误。  
  
 在此示例中，我们将查看名为 Days in Current Quarter 的度量值中一个更为复杂的公式：  
  
```  
Days in Current Quarter:=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))  
```  
  
 此度量值用于创建一个不完整期间与前一个期间之间的比率。 该公式必须考虑期间中已消逝的比例，并将其与前一期间中的同一比例进行比较。 在此情况下，[Days Current Quarter to Date]/[Days in Current Quarter] 给出当前期间中已消逝的比例。  
  
 此公式包含以下元素：  
  
|公式元素|Description|  
|---------------------|-----------------|  
|`Days in Current Quarter:=`|度量值的名称。|  
|`=`|公式以等号 (=) 开头。|  
|`COUNTROWS`|[COUNTROWS 函数 (DAX)](http://msdn.microsoft.com/en-us/830dd659-5405-4e0a-8d26-01ae9d5e5e9a) 计算 Date 表中的行数。|  
|`()`|左括号和右括号指定参数。|  
|`DATESBETWEEN`|DATESBETWEEN 函数返回 Date 表的 Date 列中每个值的最后日期之间的天数。|  
|`'Date'`|指定 Date 表。 表引在单引号中。|  
|`[Date]`|指定 Date 表中的 Date 列。 列括在方括号中。|  
|`,`||  
|`STARTOFQUARTER`|STARTOFQUARTER 函数返回季度的开始日期。|  
|`LASTDATE`|LASTDATE 函数返回季度的结束日期。|  
|`'Date'`|指定 Date 表。|  
|`[Date]`|指定 Date 表中的 Date 列。|  
|`,`||  
|`ENDOFQUARTER`|ENDOFQUARTER 函数|  
|`'Date'`|指定 Date 表。|  
|`[Date]`|指定 Date 表中的 Date 列。|  
  
#### <a name="using-formula-autocomplete"></a>使用公式记忆式键入功能  
 模型设计器中的公式栏和“角色管理器”对话框中的公式“行筛选器”窗口都提供记忆式键入功能。 记忆式键入功能通过为您提供公式中每个元素的选项，可帮助您输入有效的公式语法。  
  
-   可以在具有嵌套函数的现有公式中使用公式记忆式键入功能。 刚好在插入点之前的文本将用于显示下拉列表中的值，并且插入点之后的所有文本都保持不变。  
  
-   记忆式键入功能不添加函数的右括号或自动匹配括号。 您必须确保每个函数在语法上都是正确的，否则不能保存或使用公式。  
  
#### <a name="using-multiple-functions-in-a-formula"></a>在公式中使用多个函数  
 您可以嵌套函数，这意味着您可以使用一个函数的结果作为另一个函数的参数。 在计算列中，最多可以嵌套 64 个级别的函数。 但是，嵌套可能会导致很难创建公式或者排除公式问题。  
  
 许多函数设计为仅用作嵌套函数。 这些函数返回一个表，该表不能直接保存为结果，而必须作为表函数的输入提供。 例如，函数 SUMX、AVERAGEX 和 MINX 全都要求将表作为第一个参数。  
  
> [!NOTE]  
>  在度量值内嵌套函数时会应用一些限制，以确保不会由于列之间的依赖关系所要求的许多计算而影响性能。  
  
##  <a name="bkmk_DAX_functions"></a> DAX functions  
 本节概述 DAX 中支持的函数“类型”。  有关详细信息，请参阅 [DAX 函数参考](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b)。  
  
 DAX 提供多种函数，可用于使用日期和时间执行计算、创建条件值、处理字符串、基于关系执行查找，以及循环访问某个表以执行递归计算。 如果您熟悉 Excel 公式，会发现 Excel 公式与 DAX 公式中的多数函数都极为相似；但是，DAX 公式在以下方面显著不同：  
  
-   DAX 函数始终引用完整的列或表。 如果您想要仅使用表或列中的特定值，则可以向公式中添加筛选器。  
  
-   如果需要逐行自定义计算，DAX 可提供允许您使用当前行值或相关值作为一种参数来执行计算（因上下文而异）的函数。 若要了解这些函数的工作方式，请参阅本主题下文中的 [Context in DAX Formulas](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md#bkmk_context) 。  
  
-   DAX 包含的许多函数都将返回表，而不是返回值。 表不会显示在报告客户端中，而是用于向其他函数提供输入。 例如，您可以检索一个表，然后对该表中的非重复值进行计数，或者计算多个已筛选表或列的动态总和。  
  
-   DAX 函数包括各种*时间智能*函数。 利用这些函数，您可以定义或选择日期范围，并基于这些日期或范围执行动态计算。 例如，您可以比较并行时段内的总和。  
  
### <a name="date-and-time-functions"></a>日期和时间函数  
 DAX 中的日期和时间函数类似于 Microsoft Excel 中的日期和时间函数。 但是，DAX 函数基于 Microsoft SQL Server 使用的 **datetime** 数据类型。 有关详细信息，请参阅 [日期和时间函数 (DAX)](http://msdn.microsoft.com/en-us/9fc9214a-fcd6-40c0-bf51-0c95637c6ffb)。  
  
### <a name="filter-functions"></a>筛选器函数  
 DAX 中的筛选器函数可以返回特定数据类型、在相关表中查找值以及按相关值进行筛选。 查找函数通过使用表和关系进行工作，与数据库类似。 筛选函数可用于操作数据上下文来创建动态计算。 有关详细信息，请参阅 [筛选器函数 (DAX)](http://msdn.microsoft.com/en-us/b036fd40-4d3b-426d-a0d2-80258b53d8e5)。  
  
### <a name="information-functions"></a>信息函数  
 信息函数查找作为参数提供的单元格或行，并且指示值是否与预期的类型匹配。 例如，如果您引用的值包含错误，则 ISERROR 函数将返回 TRUE。 有关详细信息，请参阅 [信息函数 (DAX)](http://msdn.microsoft.com/en-us/6d2bee09-0456-4444-b4d2-c231fd788a2e)。  
  
### <a name="logical-functions"></a>逻辑函数  
 逻辑函数对表达式执行操作，以返回表达式中有关值的信息。 例如，通过 TRUE 函数您可以了解您正在计算的表达式是否返回 TRUE 值。 有关详细信息，请参阅 [逻辑函数 (DAX)](http://msdn.microsoft.com/en-us/2eb33add-60b2-44ab-b761-012a473116a2)。  
  
### <a name="mathematical-and-trigonometric-functions"></a>数学和三角函数  
 DAX 中的数学函数与 Excel 中的数学和三角函数非常相似。 DAX 函数使用的数值数据类型存在一些细微的差别。 有关详细信息，请参阅 [数学和三角函数 (DAX)](http://msdn.microsoft.com/en-us/1f408ec1-e769-43d6-a68c-567bc30d893f)。  
  
### <a name="statistical-functions"></a>统计函数  
 DAX 提供执行聚合的统计函数。 除了求和与平均值或者查找最小值和最大值外，您还可以通过 DAX 在聚合之前筛选列或基于相关表创建聚合。 有关详细信息，请参阅 [统计函数 (DAX)](http://msdn.microsoft.com/en-us/ba4c1298-57a0-40fc-b6f6-00e187ace559)。  
  
### <a name="text-functions"></a>文本函数  
 DAX 中的文本函数与 Excel 中的同等函数非常相似。 可以返回部分字符串、搜索字符串中的文本或连接字符串。 DAX 还提供了用于控制日期、时间和数字格式的函数。 有关详细信息，请参阅 [文本函数 (DAX)](http://msdn.microsoft.com/en-us/e4821571-ae55-4df7-ae98-c578200bba5f)。  
  
### <a name="time-intelligence-functions"></a>时间智能函数  
 DAX 中提供的时间智能函数允许你创建使用有关日历和日期的内置知识的计算。 通过将时间和日期范围与聚合或计算结合使用，您可以为销售、库存等生成可比较时间段内的有意义比较。 有关详细信息，请参阅[时间智能函数 (DAX)](http://msdn.microsoft.com/en-us/91df278d-4b28-40c1-a572-cdb91f081517)。  
  
###  <a name="bkmk_TableFunc"></a> Table-valued functions  
 有许多 DAX 函数可输出表并且/或者将表作为输入。 因为表可以包含单个列，所以表值函数还可以将单个列作为输入。 了解如何使用这些表值函数对于充分利用 DAX 公式很重要。 DAX 包括以下类型的表值函数：  
  
  **筛选器函数**-返回某一列、 表或相关的当前行的值。  
    
  **聚合函数**-聚合表的行上的任何表达式。  
    
  **时间智能函数**-返回表的日期，或使用日期表计算聚合。  
  
##  <a name="bkmk_context"></a> Context in DAX formulas  
  “上下文”是在使用 DAX 创建公式时需要了解的一个重要概念。 您可以通过上下文执行动态分析，因为公式的结果会发生更改以反映当前行或单元选择以及任何相关数据。 了解上下文并有效使用上下文对构建高性能的动态分析和解决公式中的问题至关重要。  
  
 可以在不同的上下文中计算表格模型中的公式，这取决于其他设计元素：  
  
-   数据透视表或报表中应用的筛选器  
  
-   公式中定义的筛选器  
  
-   使用公式中的特殊函数指定的关系  
  
 有许多类型的上下文：“行上下文” 、“查询上下文” 和“筛选上下文”。  
  
###  <a name="bkmk_row_context"></a> Row context  
  “行上下文”可以被视作“当前行”。 如果您在计算列中创建某一公式，则该公式的“行上下文”将包括来自当前行中所有列的值。 如果该表与其他表相关，则上下文还包括来自另一个表中与当前行相关的所有值。  
  
 例如，假设创建将同一表中的两列（Freight 和 Tax）的值相加的计算列 `=[Freight] + [Tax]`。 此公式仅自动获取指定列中当前行的值。  
  
 行上下文还会依照已定义的表之间的任何关系（包括使用 DAX 公式在计算列中定义的关系）来确定相关表中与当前行关联的行。  
  
 例如，下面的公式使用 RELATED 函数根据订单的发货目的地从相关表提取税金值。 通过使用当前表中的区域值，在相关表中查找该区域，然后从相关表中获取该区域的税率，从而确定税金值。  
  
```  
= [Freight] + RELATED('Region'[TaxRate])  
```  
  
 此公式从 Region 表中获取当前区域的税率，并将其与 Freight 列中的值相加。 在 DAX 公式中，您无需了解或指定连接各表的特定关系。  
  
#### <a name="multiple-row-context"></a>多行上下文  
 DAX 包括对表执行迭代计算的函数。 这些函数可以具有多个当前行，其中每个行都有自己的行上下文。  实际上，可以利用这些函数创建用于以递归方式对内部和外部循环进行操作的公式。  
  
 例如，假设您的模型包含一个 **Products** 表和一个 **Sales** 表。 用户可能想要遍历整个 Sales 表，该表中全都是涉及多个产品的交易，并且您还要找到在任何一个交易中为每个产品订购的最大数量。  
  
 使用 DAX，您可以生成返回正确值的单个公式，并且只要用户向表中添加数据，结果就自动更新。  
  
```  
=MAXX(FILTER(Sales,[ProdKey]=EARLIER([ProdKey])),Sales[OrderQty])  
```  
  
 有关此公式的详细演练，请参阅 [EARLIER 函数 (DAX)](http://msdn.microsoft.com/en-us/6d126c4d-2315-49ec-899d-cb396eefbae6)。  
  
 总之，该 EARLIER 函数存储来自当前运算之前的运算中的行上下文。 在任何时候，该函数都在内存中存储两组上下文：一组上下文表示公式的内部循环的当前行，另一组上下文表示公式的外部循环的当前行。 DAX 自动在两个循环之间馈送值，以便您可以创建复杂的聚合。  
  
####  <a name="bkmk_query_context"></a> Query context  
  “查询上下文”是指为公式隐式检索的数据子集。 当用户将度量值字段或其他值字段放入数据透视表或基于表格模型的报表后，引擎将检查行和列标题、切片器和报表筛选器以便确定上下文。 之后，将对数据源运行必要的查询以获取正确的数据子集，执行公式所定义的计算，然后填充数据透视表或报表中的每个单元。 检索的数据集是各单元的查询上下文。  
  
> [!WARNING]  
>  对于 DirectQuery 模式中的模型，先计算上下文，然后将用于检索正确的数据子集并计算结果的集运算转换为 SQL 语句。 随后直接对关系数据存储区运行这些语句。 因此，虽然用于获取数据并计算结果的方法是不同的，但上下文本身不会更改。  
  
 由于上下文会随公式位置的不同而不同，因此，公式的结果可能随之更改。  
  
 例如，假设您创建下面的简单公式，用来计算 **Sales** 表的 **Profit** 列中的各值之和： `=SUM('Sales'[Profit])`。  如果您在 **Sales** 表内的计算列中使用该公式，则该公式的结果对于整个表将是相同的，因为公式的查询上下文始终是 **Sales** 表的整个数据集。 结果会包含所有地区、所有产品、所有年份等的利润。  
  
 但是，用户通常不想数百次看到相同的结果，而是希望获取特定年份、特定国家/地区、特定产品或这些项的某些组合的利润，然后获取总计。  
  
 在数据透视表中，可以通过添加或删除列和行标题以及添加或删除切片器来更改上下文。 只要用户将列或行标题添加到数据透视表中，就可以更改在其中计算度量值的查询上下文。 切片和筛选运算也会影响上下文。  因此，对于每个单元，在不同的“查询上下文”中计算在度量值中使用的相同公式。  
  
####  <a name="bkmk_filter_context"></a> Filter context  
  “筛选上下文”是指每个列中允许存在的一组值，或可属于从相关表中检索到的值的一组值。 可以对设计器或表示层（报表和数据透视表）中的列应用筛选器。 也可以通过公式中的筛选表达式来显式定义筛选器。  
  
 通过在公式中使用参数，为列或表中允许存在的值集指定筛选约束时，将添加“筛选上下文”。 基于其他上下文（如行上下文或查询上下文）应用筛选上下文。  
  
 在表格模型中，可通过多种方式来创建筛选上下文。 可以使用模型，如 Power BI 报表、 客户端的上下文中的用户可以创建筛选器动态通过在行和列标题上添加切片器或报表筛选器。 还可以在公式中直接指定筛选表达式来执行以下操作：指定相关的值、筛选用作输入的表或动态获取计算中使用的值的上下文。 您还可以完全清除或有选择地清除特定列上的筛选器。 这在创建用于计算总计的公式时很有用。  
  
 有关如何在公式内创建筛选器的详细信息，请参阅 [FILTER 函数 (DAX)](http://msdn.microsoft.com/en-us/f1f6bee4-547b-407c-b70b-9216b2f3d3fd)。  
  
 有关如何清除筛选器以便创建总计的示例，请参阅 [ALL 函数 (DAX)](http://msdn.microsoft.com/en-us/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc)。  
  
 有关如何在公式内有选择地清除和应用筛选器的示例，请参阅 [ALLEXCEPT 函数 (DAX)](http://msdn.microsoft.com/en-us/a6f575a1-9803-4bb2-85b3-c95c060f1fb1)。  
  
####  <a name="bkmk_determine_context"></a> Determining context in formulas  
 在创建一个 DAX 公式时，首先会测试该公式的语法是否有效，然后测试该公式以确保其包含的列和表的名称位于当前上下文中。 如果找不到该公式指定的任一列或表，则将返回错误。  
  
 如前所述，通过使用模型中的可用表、表之间的所有关系和所应用的所有筛选器来确定验证（和重新计算操作）期间的上下文。  
  
 例如，如果刚刚将一些数据导入到一个新表中，而该表未与任何其他表关联（并且尚未应用任何筛选器），则当前上下文是表中的完整列集。 如果通过关系将该表与其他表链接，则当前上下文将包括相关的表。 如果将该表中的某个列添加到一个报表中，该报表具有切片器并且可能具有一些报表筛选器，则公式的上下文是报表的每个单元中的数据子集。  
  
 上下文是一个很有用的概念，但也可能导致很难排除公式问题。 我们建议您从简单的公式和关系入手，了解上下文的工作原理。 下一节提供了一些示例，说明公式如何使用不同类型的上下文来动态返回结果。  
  
##### <a name="examples-of-context-in-formulas"></a>公式中上下文的示例  
  
1.  [RELATED 函数 (DAX)](http://msdn.microsoft.com/en-us/0023fd13-c17a-4243-ab77-3779a4b502b6) 函数可展开当前行的上下文以包括相关列中的值。 这允许您执行查找。 该主题中的示例阐释筛选和行上下文的交互情况。  
  
2.  通过 [FILTER 函数 (DAX)](http://msdn.microsoft.com/en-us/f1f6bee4-547b-407c-b70b-9216b2f3d3fd) 函数可以指定要包括在当前上下文中的行。 该主题中的示例还演示如何在执行聚合的其他函数内嵌入筛选器。  
  
3.  [ALL 函数 (DAX)](http://msdn.microsoft.com/en-us/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc) 函数可在公式中设置上下文。 使用此函数可以覆盖因查询上下文而应用的筛选器。  
  
4.  通过 [ALLEXCEPT 函数 (DAX)](http://msdn.microsoft.com/en-us/a6f575a1-9803-4bb2-85b3-c95c060f1fb1) 函数可以删除你所指定的筛选器之外的所有筛选器。 以上两个主题包括的示例将引导您构建公式和了解复杂的上下文。  
  
5.  通过 [EARLIER 函数 (DAX)](http://msdn.microsoft.com/en-us/6d126c4d-2315-49ec-899d-cb396eefbae6) 和 [EARLIEST 函数 (DAX)](http://msdn.microsoft.com/en-us/9befa04d-78db-492e-a463-80b8b77206d6) 函数，可以执行计算以便循环遍历表，并引用内部循环中的值。 如果您熟悉递归的概念以及内部循环和外部循环，将领会到 EARLIER 和 EARLIEST 函数所提供的强大功能。 如果这些概念对您来说是全新的，则应仔细按照示例中的步骤执行，以便了解如何在计算中使用内部上下文和外部上下文。  
  
##  <a name="bkmk_RelModel"></a> Formulas and the tabular model  
 模型设计器中的，在 SSDT 中，是的区域，其中你可以使用多个表的数据，并连接表格模型中的表。 在此模型内，表通过具有公用值（键）的各列之间的关系联接起来。 利用表格模型，您可以将值链接到其他表中的列，从而创建更有趣的计算。 正如在关系数据库中一样，您可以连接多个级别的关系表，也可以在结果中使用任何表中的列。  
  
 例如，您可以链接销售表、产品表和产品类别表，用户可以在数据透视表和报表中使用列的各种组合。 关系字段可用于对连接的表进行筛选，或针对子集创建计算。 (如果尚不熟悉关系数据库和使用表和联接，请参阅[关系](../../analysis-services/tabular-models/relationships-ssas-tabular.md)。)  
  
 表格模型支持表之间的多种关系。 为避免混淆或结果错误，每次只将一个关系指定为活动关系，但您可以根据需要更改活动关系以便遍历计算数据中的不同连接。 [USERELATIONSHIP 函数 (DAX)](http://msdn.microsoft.com/en-us/200484ab-9da1-4570-a100-7f9ed20d33af) 可用于指定一个或多个要在特定计算中使用的关系。  
  
 在表格模型中，您应遵守以下公式设计规则：  
  
-   在通过关系连接表时，必须确保用作键的两列具有匹配的值。 但不强制引用完整性，因此有可能在键列中具有不匹配值的情况下仍创建关系。 如果发生这种情况，您应注意空值或不匹配值可能会影响公式的结果。  
  
-   使用关系在模型中链接表时，可以扩大公式的计算范围（或“上下文”）。 因添加新表、新关系或因活动关系改变而引起的上下文变化可能会导致结果发生意外变化。 有关详细信息，请参阅本主题前面的 [DAX 公式中的上下文](#bkmk_context) 。  
  
##  <a name="bkmk_tables"></a> Working with tables and columns  
 表格模型中的表在外观上与 Excel 表类似，但在处理数据和公式的方式上却有所不同：  
  
-   公式只使用表和列，而不使用各个单元格、范围引用或数组。  
  
-   公式可以使用关系从相关表中获取值。 检索到的值始终与当前行值相关。  
  
-   您不能像在 Excel 工作表中一样使用不规则或“不齐整”的数据。 表中每行所包含的列数必须相同。 然而，一些列中可以包含空值。 Excel 数据表和表格模型数据表不能互换。  
  
-   由于为每列都设置了数据类型，该列中的每个值必须同属一种类型。  
  
### <a name="referring-to-tables-and-columns-in-formulas"></a>在公式中引用表和列  
 可以通过名称来引用任何表和列。  例如，下面的公式说明如何通过使用“完全限定”的名称来引用两个表中的列：  
  
```  
=SUM('New Sales'[Amount]) + SUM('Past Sales'[Amount])  
```  
  
 计算公式时，模型设计器首先检查常规语法，然后根据当前上下文中的可能列和表检查所提供的列和表的名称。 如果名称不明确或者列或表无法找到，则您将收到有关公式的错误（在发生错误的单元格中，用 #ERROR 字符串代替数据值）。 有关对表、列和其他对象的命名要求的详细信息，请参阅 [DAX 语法参考](http://msdn.microsoft.com/en-us/098630f4-7d1d-467e-976c-99b2279430d5)中的“命名要求”。  
  
### <a name="table-relationships"></a>表关系  
 通过创建表之间的关系，可以在另一个表中查找数据，并使用相关值来执行复杂计算。 例如，可以使用计算列来查找与当前分销商相关的所有装运记录，然后对每个分销商的装运成本求和。 但在许多情况下，关系可能没有必要。 可以在公式中使用 LOOKUPVALUE 函数为满足在 search_column 和 search_value 参数中指定的条件的行返回 result_columnName 中的值。  
  
 很多 DAX 函数都要求两个表或多个表之间存在关系，以便定位所引用的列并返回有意义的结果。 其他函数将尝试确定关系；但是，为获得最佳结果，您始终应尽量创建关系。 有关详细信息，请参阅本主题前面的 [公式和表格模型](#bkmk_RelModel) 。  
  
##  <a name="bkmk_RefreshRecalc"></a> Updating the results of formulas (Process)  
  “数据处理”  和“重新计算”是两个独立但相关的操作。 在设计包含复杂公式、大量数据或从外部数据源获取的数据的模型时，应充分了解这些概念。  
  
  “处理数据”是用外部数据源的新数据更新模型中数据的过程。  
  
  “重新计算”是对公式结果进行更新的过程，用于反映对公式本身的任何更改以及基础数据中的更改。 重新计算会以下列方式影响性能：  
  
-   对计算列中的值进行计算并存储在模型中。 若要更新计算列中的值，必须使用以下三个处理命令之一处理该模型 —“处理全部”、“处理数据”或“处理重新计算”。 每当您更改公式时，必须始终针对整个列重新计算公式的结果。  
  
-   每当用户向数据透视表添加度量值或打开报告时，系统都会动态计算由该度量值计算的值；当用户修改上下文时，度量值所返回的值将发生变化。 度量值的结果将始终反映内存中缓存中的最新内容。  
  
 处理和重新计算对行筛选器公式没有影响，除非重新计算的结果返回不同的值，致使角色成员能够查询或不能查询该行。  
  
 有关详细信息，请参阅 [处理数据（SSAS 表格）](../../analysis-services/tabular-models/process-data-ssas-tabular.md)。  
  
##  <a name="bkmk_troubleshoot"></a> Troubleshooting errors in formulas  
 如果在定义公式时遇到错误，公式可能会包含“语法错误” 、“语义错误” 或“计算错误”。  
  
 语法错误最容易解决。 它们通常涉及缺少括号或逗号。 有关单独函数的语法的帮助，请参阅 [DAX 函数参考](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b)。  
  
 在语法无误时发生其他类型的错误，但引用的值或列在公式的上下文中没有意义。 此类语义和计算错误可能是由于下列任何问题导致的：  
  
-   公式中引用不存在的列、表或函数。  
  
-   公式似乎正确，但在数据引擎提取数据时，它发现一个类型不匹配，并引发错误。  
  
-   公式将错误的参数数目或类型传递到函数。  
  
-   公式中引用有错误的其他列，因此它的值无效。  
  
-   公式会引用尚未处理的列，这意味着，它有元数据，但没有用于计算的实际数据。  
  
 在前四种情况中，DAX 标记包含无效公式的整个列。 在最后一种情况中，DAX 会灰显该列，以便指示该列处于未处理的状态中。  
  
##  <a name="bkmk_addional_resources"></a> Additional resources  
 [表格建模（Adventure Works 教程）](../../analysis-services/tabular-modeling-adventure-works-tutorial.md)提供关于如何创建在计算列、度量值和行筛选器中包含许多计算的表格模型的分步说明。 对于大多数公式，都提供关于该公式的用途的说明。  
  
 [Analysis Services 团队博客](http://go.microsoft.com/fwlink/?LinkID=220949&clcid=0x409)提供最新信息、 提示、 新闻和公告。 
  
 [DAX 资源中心](http://go.microsoft.com/fwlink/?LinkID=220966&clcid=0x409) 同时提供关于 DAX 的内部和外部信息，包括由主要商业智能专业人员提交的大量 DAX 解决方案。  
  
## <a name="see-also"></a>另请参阅  
 [数据分析表达式 (DAX) 参考](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)   
 [度量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [计算的列](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [支持的数据源](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
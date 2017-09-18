---
title: "Power View 报表 (SSAS 表格) 的配置表行为属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.tablebehavior.f1
ms.assetid: 1386aae0-1d73-4a50-9c69-ae12405d855c
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 95a50d5ed10e8714b50e33ac4e182ff208c4c840
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="power-view---configure-table-behavior-properties-for-reports"></a>Power View-为报表配置表行为属性
  如果您将表格模型用作 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]的数据模型，则可以设置以更高粒度级别显示详细信息行的表行为属性。 设置表行为属性会更改详细信息行的分组行为，并为图块、卡片和图表布局中的标识信息（如名称、照片 ID 或徽标图像）生成更好的默认位置。  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 不同于其他报表应用程序，因为它在报表设计期间自动对项进行分组，其方法是对照您所使用的显示格式计算您放入报表字段列表中的列。 在大多数情况下，默认分组会产生最佳结果。 但对于某些表（主要是包含详细数据的表），默认分组行为有时将对不应分组的行进行分组。 对于此类表，您可以设置用于更改对组进行计算的方式的属性。  
  
 对于您主要关心其中各单独行的表（如员工记录或客户记录），建议设置表行为属性。 相比较而言，未从这些属性受益的表包括那些充当查找表的表（例如，日期表、产品目录表或部门表，其中，表由相对较少的行数和列数组成），或者摘要表（其中包含的行只在汇总时才有用，如按照性别、年龄或地理位置累计的人口普查数据）。 对于查找表和摘要表，默认的分组行为会产生最佳结果。  
  
> [!NOTE]  
>  表行为属性只影响在 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]中用作数据模型的表格模型。 Excel 透视报表不支持表行为属性。  
  
 表行为属性包括以下各项：  
  
-   **行标识符** ─ 指定只包含唯一值的一列，同时允许将该列用作内部分组键。  
  
-   **保留唯一行** - 指定哪些列提供应视为唯一的值，即使这些值重复也不例外（例如，员工的姓氏和名字，而两个或更多员工同名）。  
  
-   **默认标签** - 指定哪一列提供显示名称来表示行数据（例如，员工记录中的员工姓名）。  
  
-   **默认图像** - 指定哪一行提供用于表示行数据的图像（例如，员工记录中的照片 ID）。  
  
> [!NOTE]  
>  请参阅下面的章节，了解如何从特定显示格式的角度进行布局优化：  [针对特定布局进行优化](#bkmk_optimizeforlayout)。  
  
## <a name="opening-the-table-behavior-dialog-box"></a>打开“表行为”对话框  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击要为其配置默认字段列表的表。  
  
2.  在 **“属性”** 窗口的 **“表行为”** 属性中，单击 **“单击可编辑”**。  
  
3.  在 **“表行为”** 对话框中，设置 **“行标识符”**，然后在此对话框中指定其他属性。  
  
## <a name="setting-the-row-identifier-property"></a>设置行标识符属性  
 在该表中，行标识符指定单一列，其中仅包含唯一值且不包含空值。 “行标识符”属性用于更改分组，以便组不基于行的字段构成，而是基于始终用于唯一标识一行的固定列，无论在特定报表布局中使用哪些字段。  
  
 设置此属性后，会将默认分组行为从动态分组（基于画布上存在的列）更改为基于行标识符进行汇总的固定分组行为。 更改默认分组行为对于报表布局是相关的，例如矩阵，它原本针对行中的每列进行分组（或显示小计）。  
  
 在 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]中，设置行标识符可以启用以下附加属性： **“保留唯一行”** 属性、 **“默认标签”** 属性和 **“默认图像”** 属性。  
  
 您还可以将 **“行标识符”** 本身用作独立属性，以支持以下各项：  
  
-   在报表中使用二进制图像。 通过删除围绕行唯一性的不明确性， [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 可以确定如何为给定的行分配默认图像和默认标签。  
  
-   从矩阵报表中删除多余的小计。 在字段级别进行默认分组会为每个字段创建小计。 如果您只需要在行级别计算的单个小计，则设置行标识符将生成此结果。  
  
 您不能为标记为日期表的表设置行标识符。 对于日期表，当您标记表时指定行标识符。 有关详细信息，请参阅[“标记为日期表”对话框 (SSAS)](http://msdn.microsoft.com/library/698b5ef1-b79b-4d76-9847-39669b4f5bb9)。  
  
## <a name="setting-the-keep-unique-rows-property"></a>设置“保留唯一行”属性  
 借助此属性，您可以指定哪些列通过区分不同行的方式传达标识信息（例如，员工姓名或产品代码）。 在行看起来完全相同的情况下（例如，两个同名的客户），您为此属性指定的列将重复出现在报表表格中。  
  
 根据您添加到报表的列，您可能会找到被视为相同行的行，因为每行中的值看起来相同（例如，两个名为 Jon Yang 的客户）。 之所以可能发生这种情况，是因为可用于区别的其他列（如中间名、地址或生日）不在报表画布中。 在此类情况下，默认行为是将看起来完全相同的行分组为单行，同时从组合的各行中将任何计算的值汇总为单个较大的结果。  
  
 通过设置 **“保留唯一行”** 属性，只要您将应始终重复的一列或多列添加到报表画布，您就可以指定这些列，即使存在重复实例也不例外。 与此行关联的计算值现在将基于每个单独行进行分配，而不是累计到单个行。 当为  **“保留唯一行”** 属性选择列时，请选择其中包含唯一值或几乎都是唯一值的那些列。  
  
> [!NOTE]  
>  因为最终用户选择的列可能影响分组，这会更改用于表达式计算的筛选器上下文，所以，模型设计者在创建可返回正确结果的度量值时务必小心。 有关详细信息，请参阅 [Power View FAQ](http://go.microsoft.com/fwlink/?LinkId=220674)（Power View 常见问题解答）。  
  
## <a name="setting-a-default-label"></a>设置默认标签  
 此属性指定出现在图块报表的导航条中的标签。 当与默认图像结合使用时，默认标签将出现在图像下方。 如果没有图像，则显示默认标签本身。 当选择默认标签时，请挑选传达有关行的最多信息的列（如名称）。  
  
 在图块布局中，默认标签按照“默认图像”属性所确定的方式出现在图像之下的标题区域中。 例如，如果您有员工列表，则可以使用员工的照片 ID 作为默认图像，并将员工姓名用作默认标签，从而以图块方式显示员工信息。 在图块中，默认标签出现在默认图像之下。 这些列始终出现在图块中，即使您没有在报表字段列表中显式选择它们也不例外。  
  
## <a name="setting-a-default-image"></a>设置默认图像  
 此属性指定出现在图块报表的导航条中或卡片正面的图像。 在报表中，当您选择包含默认图像的列时，默认图像将出现在图块报表布局的导航条中或卡片正面。 默认图像应为可视内容。 示例包括员工表中的照片 ID、客户表中的客户徽标或地域表中的国家/地区形状。  
  
> [!NOTE]  
>  图像来源可以是 URL 地址到 Web 服务器上的图像文件，或者作为工作簿中嵌入的二进制数据。 如果图像基于 URL，请确保将列设置为图像类型，以便 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 检索图像，而不是将 URL 显示为报表中的文本数据。  
  
##  <a name="bkmk_optimizeforlayout"></a> 针对特定布局进行优化  
 下面的章节介绍从特定显示格式的角度和数据特性设置表行为属性的影响。 举例而言，如果您尝试精细优化矩阵报表的布局，则可以使用此信息来理解如何通过在模型中使用表行为属性来改进矩阵显示。  
  
### <a name="images-are-missing"></a>图像缺失  
 您在模型中设置的属性将决定图像是直观显示在报表中，还是在报表中显示为文本值。  
  
 ![图像 Url 显示为在报表中的文本](../../analysis-services/tabular-models/media/ssas-rptprop-noimageurl.gif "图像 Url 显示为在报表中的文本")  
  
 默认情况下，模型中的文本将被解释为报表中的文本。 如果文本列是指向报表图像的 URL 地址，请别忘记设置 **“图像 URL”** 属性，以便 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 检索图像文件。 对于二进制图像，请记住要设置 **“行标识符”** 属性。  
  
### <a name="tables-are-missing-one-or-more-rows"></a>表缺少一个或多个行  
 有时，默认分组行为导致与您的预期相反的结果；尤其是，出现在模型中的详细信息行不显示在报表中。 默认情况下， [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 对您添加到画布的列进行分组。 如果你向报表添加“国家/地区名称”，则每个国家/地区都会在画布上出现一次，即使基础表可能包含数千个包括每个国家/地区名称的多个实例的行  。 在这种情况下，默认分组行为产生正确的结果。  
  
 但是，请考虑一个不同的示例：您可能需要显示某行的多个实例，因为事实上，基础行包含有关不同实体的数据。 在此示例中，假定你有两个名为 **Jon Yang**的客户。 如果使用默认分组行为，则在报表中将只显示一个 **Jon Yang** 实例。 而且，因为列表中只显示一个实例，所以，度量值“年收入”是这两个客户的年收入值的总和  。  
  
 ![默认组将 2 集中到 1](../../analysis-services/tabular-models/media/ssas-jonyang-norowid.gif "默认组将 2 集中到 1")  
  
 若要更改默认分组行为，请设置 **“行标识符”** 和 **“保留唯一行”** 属性。 在 **“保留唯一行”**中，选择“姓氏”列，这样，此值将对某行重复，即使它已出现在不同行中。 当你更改属性并重新发布工作簿之后，你可以创建同一个报表，只有在此时，你才能看到这两个名为 **Jon Yang**的客户，且 **年收入** 正确地分配给其中每个人。  
  
 ![行数据包含重复项基于行 ID](../../analysis-services/tabular-models/media/ssas-jonyang.gif "行包含基于行 ID 的重复项的数据")  
  
### <a name="matrix-layout-is-too-crowded"></a>矩阵布局太拥挤  
 当您在矩阵中显示详细信息表时，默认分组提供每列的汇总值。 根据您的目标，这种汇总值可能比您需要的更多。 要更改此行为，您可以设置 **“行标识符”**。 不需要设置其他属性；设置行标识符就足以更改分组，以便基于每行的唯一行标识符对该行计算汇总值。  
  
 比较下面的设置之前和之后的图像，它们显示了设置此属性对于矩阵布局的影响。  
  
 **之前：默认分组基于矩阵中的字段**  
  
 ![矩阵布局分组在行标识符上](../../analysis-services/tabular-models/media/ssas-rptprop-matrixrowid.gif "矩阵布局分组在行标识符上")  
  
 **之后：基于行标识符进行分组**  
  
 ![矩阵布局分组在行标识符上](../../analysis-services/tabular-models/media/ssas-rptprop-matrixrowid.gif "矩阵布局分组在行标识符上")  
  
### <a name="chart-showing-too-many-items-and-levels-on-the-axis"></a>图表在轴上显示的项和级别过多  
 显示详细信息数据的图表报表应将行标识符用作轴。 如果没有行标识符，则轴是不确定的，这会导致最佳猜测的布局，而这种布局可能没有意义。 要更改此行为，您可以设置 **“行标识符”**。 不需要设置其他属性；设置行标识符就足以更改分组，以便基于每行的唯一行标识符对该行计算汇总值。  
  
 比较下面的设置之前和之后的图像，它们显示了设置此属性对于图表布局的影响。 它是同一报表，具有完全相同的字段和显示格式。 唯一的差别是底部图像显示对 Items 表设置 **“行标识符”** 之后的报表。  
  
 **之前：默认分组基于图表中的字段**  
  
 ![图表，根据默认分组在字段级别](../../analysis-services/tabular-models/media/ssas-rptprop-chartfieldgroup.gif "图表，根据默认分组在字段级别")  
  
 **之后：基于行标识符进行分组（行标识符变成轴）**  
  
 ![图表，根据行 ID 分组](../../analysis-services/tabular-models/media/ssas-rptprop-chartrowid.gif "图表，根据行 ID 分组")  
  
## <a name="next-steps"></a>后续步骤  
 在计算模型中的表并对包含详细信息行（这些行应始终显示为单独项）的表设置表行为属性之后，您可以通过其他属性或设置来进一步优化模型。  
  
  
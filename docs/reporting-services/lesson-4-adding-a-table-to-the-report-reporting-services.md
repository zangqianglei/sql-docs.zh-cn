---
title: "第 4 课： 将表添加到报表 (Reporting Services) |Microsoft 文档"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
caps.latest.revision: 64
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 76224139b629d797735b88bfcc692a1e8abce336
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>第 4 课：向报表添加表 (Reporting Services)
定义数据集后，您可以开始定义报表。 将要纳入报表的数据区域、文本框、图像和其他项拖放到设计图面上来创建报表布局。  
  
包含重复从基础数据集的数据行的项称为*数据区域*。 基本报表将只有一个数据区域，但是对于要将图表添加到表格报表等情况，则可以添加多个数据区域。 添加数据区域之后，可以向该数据区域添加字段。  
  
### <a name="to-add-a-table-data-region-and-fields-to-a-report-layout"></a>向报表布局中添加表数据区域和字段  
  
1.  在**工具箱**，单击**表**，然后在设计图面上单击并拖动鼠标。 报表设计器将在设计图面中心绘制一个具有三列的数据区域。 **工具箱**可能显示的左侧选项卡为**报表数据**窗格。 若要打开**工具箱**，将指针移**工具箱**选项卡。 如果**工具箱**不可见，请从**视图**菜单上，单击**工具箱**。
  
     ![ssrs_ssdt_addtable](../reporting-services/media/ssrs-ssdt-addtable.png) 
  
  你还可以从设计图面向报表添加表。  右键单击设计图面上，单击**插入**，然后单击**表**。
2.  在**报表数据**窗格中，展开数据集**AdventureWorksDataset**显示字段。  
  
3.  拖动*日期*字段从**报表数据**到表中的第一列的窗格。  
  
    将字段拖到第一列中时，会发生两件事。 首先，该数据单元格将显示的字段名称，称为*字段表达式*，括号中： `[Date]`。 其次，列标题值自动添加到紧邻字段表达式上面的标题行。 默认情况下，该列是字段的名称。 您可以选中标题行文本，然后键入一个新名称。  
  
4.  拖动*顺序*字段从**报表数据**到表中的第二个列的窗格。  
  
5.  拖动*产品*字段从**报表数据**到表中的第三个列的窗格。  
  
6.  将 Qty 字段拖到第三列的右边缘，直到显示一个垂直光标且鼠标指针带有加号 [+] 为止。 释放鼠标按钮后，将为 `[Qty]`创建第四列。  
![ssrs_tutorial_addcolumn](../reporting-services/media/ssrs-tutorial-addcolumn.png)  
  
7.  请以相同方式添加 LineTotal 字段，并创建第五列。 列标题是 Line Total。 报表设计器通过将 LineTotal 拆分为两个单词，自动创建该列的友好名称。  
  
  
以下关系图显示已由下列字段填充的表数据区域：Date、Order、Product、Qty 和 Line Total。  
![rs_BasicTableDetailsDesign](../reporting-services/media/rs-basictabledetailsdesign.png)  
  
## <a name="preview-your-report"></a>预览报表  
通过预览报表，您可以不必先将报表发布到报表服务器，即可查看呈现的报表。 您可能希望在设计时频繁预览报表。 预览报表还将对设计和数据连接进行验证，以便您可以在将报表发布到报表服务器之前更正错误和问题。  
  
#### <a name="to-preview-a-report"></a>预览报表  
  
-   单击 **预览** 选项卡。 报表设计器将运行此报表，并将其显示在“预览”视图中。
![ssrs_ssdt_preview](../reporting-services/media/ssrs-ssdt-preview.png)  
  
    下图显示了“预览”视图中的部分报表。  
  
    ![预览、 具有 5 列的表的详细信息行](../reporting-services/media/rs-basictabledetailspreview.png "预览版中，具有 5 列的表的详细信息行")  
  
    请注意，Line Total 列中货币的小数点后面有六个小数位，并且日期包含时间戳。 此格式问题将在下一课中进行修复。  
  
> [!NOTE]  
> 在 **“文件”** 菜单上单击 **“全部保存”** 可保存报表。  
  
## <a name="next-steps"></a>后续步骤  
您已成功地向报表添加了表数据区域、向数据区域添加了字段，并成功地预览了报表。 接下来，将设置列标题以及日期和货币值的格式。 请参阅[第 5 课： 格式设置报表 &#40;Reporting Services &#41;](../reporting-services/lesson-5-formatting-a-report-reporting-services.md).  
  
## <a name="see-also"></a>另請參閱  
[表（报表生成器和 SSRS）](../reporting-services/report-design/tables-report-builder-and-ssrs.md)  
[数据集字段集合（报表生成器和 SSRS）](../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  

---
title: "散点图 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2520ae24-0609-4890-807d-3267018aba8e
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f2b035836c2357feecf8f0a3763c9a3b2ba566b6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="scatter-charts-report-builder-and-ssrs"></a>散点图（报表生成器和 SSRS）
  散点图将序列显示为一组点。 值由点在图表中的位置表示。 类别由图表中的不同标记表示。 散点图通常用于比较跨类别的聚合数据。 有关如何将数据添加到散点图的详细信息，请参阅 [Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
 下图显示的是散点图示例。  
  
 ![散点图](../../reporting-services/report-design/media/rs-scatterchart.gif "散点图")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>变体  
  
-   **气泡图。** 气泡图根据气泡的大小来显示数据点的两个值之间的差。 气泡越大，两个值之间的差就越大。  
  
-   **三维气泡图**。 以三维形式显示的气泡图。  
  
## <a name="data-considerations-for-a-scatter-chart"></a>散点图的数据注意事项  
  
-   散点图通常用于显示和比较数值，例如科学数据、统计数据和工程数据。  
  
-   当要在不考虑时间的情况下比较大量数据点时，请使用散点图。 散点图中包含的数据越多，比较的效果就越好。  
  
-   气泡图要求每个数据点具有两个值（探顶值和探底值）。  
  
-   对于处理值的分布和数据点的分簇，散点图都很理想。 如果数据集中包含非常多的点（例如，几千个点），那么散点图便是最佳图表类型。 在点状图中显示多个序列看上去非常混乱，这种情况下，应避免使用点状图， 而应考虑使用折线图。  
  
-   默认情况下，散点图以圆圈显示数据点。 如果在散点图中有多个序列，请考虑将每个点的标记形状更改为方形、三角形、菱形或其他形状。  
  
## <a name="see-also"></a>另请参阅  
 [图表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [图表类型 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [格式设置图表 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [折线图 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)  
  
  
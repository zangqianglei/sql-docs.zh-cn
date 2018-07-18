---
title: 使用嵌套 FOR XML 查询 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], nested FOR XML
- nested FOR XML queries
ms.assetid: 7604161a-a958-446d-b102-7dee432979d0
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cf9e0d63af7283dfbb36a12d34224a6c379c111f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249657"
---
# <a name="use-nested-for-xml-queries"></a>使用嵌套 FOR XML 查询
  `xml`数据类型和[FOR XML 查询中的 TYPE 指令](type-directive-in-for-xml-queries.md)实现在服务器上以及在客户端上处理由 FOR XML 查询返回的 XML。  
  
## <a name="processing-with-xml-type-variables"></a>使用 xml 类型变量进行处理  
 您可以将 FOR XML 查询结果分配给 `xml` 类型变量，或使用 XQuery 查询结果，将该结果分配给 `xml` 类型变量以进行进一步处理。  
  
```  
DECLARE @x xml  
SET @x=(SELECT ProductModelID, Name  
        FROM Production.ProductModel  
        WHERE ProductModelID=122 or ProductModelID=119  
        FOR XML RAW, TYPE)  
SELECT @x  
-- Result  
--<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
--<row ProductModelID="119" Name="Bike Wash" />  
```  
  
 此外，您可以处理在变量中返回的 XML `@x`，通过使用其中一个`xml`数据类型方法。 例如，可以使用 `ProductModelID` value() 方法 [检索](/sql/t-sql/xml/value-method-xml-data-type)属性值。  
  
```  
DECLARE @i int;  
SET @i = (SELECT @x.value('/row[1]/@ProductModelID[1]', 'int'));  
SELECT @i;  
```  
  
 在以下示例中，`FOR XML` 查询结果将以 `xml` 类型返回，因为在 `TYPE` 子句中已指定了 `FOR XML` 指令。  
  
```  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=119 or ProductModelID=122  
FOR XML RAW, TYPE,ROOT('myRoot');  
  
```  
  
 结果如下：  
  
```  
<myRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
</myRoot>  
```  
  
 因为所得的结果的`xml`类型，您可以指定其中一个`xml`数据类型对此 XML 直接的方法，如下面的查询中所示。 在此查询中，[query() 方法（xml 数据类型）](/sql/t-sql/xml/query-method-xml-data-type)用于检索 <`myRoot`> 元素的第一个 <`row`> 子元素。  
  
```  
SELECT  (SELECT ProductModelID, Name  
         FROM Production.ProductModel  
         WHERE ProductModelID=119 or ProductModelID=122  
         FOR XML RAW, TYPE,ROOT('myRoot')).query('/myRoot[1]/row[1]');  
  
```  
  
 结果如下：  
  
```  
<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
```  
  
## <a name="returning-inner-for-xml-query-results-to-outer-queries-as-xml-type-instances"></a>将内部 FOR XML 查询的结果以 xml 类型实例的形式返回到外部查询  
 您可以编写嵌套`FOR XML`查询，其中内部查询的结果返回为`xml`到外部查询的类型。 例如：  
  
```  
SELECT Col1,   
       Col2,   
       ( SELECT Col3, Col4   
        FROM  T2  
        WHERE T2.Col = T1.Col  
        ...  
        FOR XML AUTO, TYPE )  
FROM T1  
WHERE ...  
FOR XML AUTO, TYPE;  
```  
  
 请注意上述查询的以下方面：  
  
-   将由内部 `FOR XML` 查询生成的 XML 添加到由外部 `FOR XML`生成的 XML。  
  
-   内部查询指定 `TYPE` 指令。 因此，由内部查询返回的 XML 数据为 `xml` 类型。 如果未指定 TYPE 指令，则将内部 `FOR XML` 查询的结果作为 `nvarchar(max)` 返回并对 XML 数据进行实体化。  
  
## <a name="controlling-the-shape-of-resulting-xml-data"></a>控制生成的 XML 数据的外形  
 通过嵌套 FOR XML 查询，您在定义生成的 XML 数据的外形时可以进行更好的控制。 可以使用嵌套 FOR XML 查询将 XML 构造为部分以属性为中心、部分以元素为中心。  
  
 有关使用嵌套 FOR XML 查询指定以属性为中心和以元素为中心的 XML 的详细信息，请参阅 [FOR XML 查询与嵌套 FOR XML 查询的比较](../xml/for-xml-query-compared-to-nested-for-xml-query.md) 和 [使用嵌套的 FOR XML 查询形成 XML](../xml/shape-xml-with-nested-for-xml-queries.md)。  
  
 可以通过指定嵌套 AUTO 模式的 FOR XML 查询生成包含同级的 XML 层次结构。 有关详细信息，请参阅 [使用嵌套 AUTO 模式查询生成同级](../xml/generate-siblings-with-a-nested-auto-mode-query.md)。  
  
 不管使用哪种模式，嵌套 FOR XML 查询均可对说明生成的 XML 的外形进行更好的控制。 可以使用这些查询替代 EXPLICIT 模式查询。  
  
## <a name="examples"></a>示例  
 下列主题提供嵌套 FOR XML 查询的示例。  
  
 [FOR XML 查询与嵌套 FOR XML 查询的比较](../xml/for-xml-query-compared-to-nested-for-xml-query.md)  
 将单一级别的 FOR XML 查询与嵌套 FOR XML 查询进行了比较。 此示例包含有关如何使查询结果同时包含以属性为中心和以元素为中心的 XML 的说明。  
  
 [使用嵌套 AUTO 模式查询生成同级](../xml/generate-siblings-with-a-nested-auto-mode-query.md)  
 显示如何使用嵌套 AUTO 模式查询生成同级  
  
 [在 ASP.NET 中使用嵌套 FOR XML 查询](use-nested-for-xml-queries-in-asp-net.md)  
 说明 ASPX 应用程序如何使用 FOR XML 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]返回 XML。  
  
 [使用嵌套的 FOR XML 查询形成 XML](../xml/shape-xml-with-nested-for-xml-queries.md)  
 显示如何使用嵌套 FOR XML 查询来控制由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建的 XML 文档的结构。  
  
  
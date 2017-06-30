---
title: "GetDatabaseVersionDisplayName 方法 (WMI) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GetDatabaseVersionDisplayName method
ms.assetid: e1286424-7043-4f12-a7ad-1cf69e81baa4
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b4743439f2edf3f3cfb253aa981af83350f5aff7
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="configurationsetting-method---getdatabaseversiondisplayname"></a>ConfigurationSetting 方法-GetDatabaseVersionDisplayName
  获取给定报表服务器数据库版本字符串的显示名称。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub GetDatabaseVersionDisplayName(Version As String, DisplayName As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetDatabaseVersionDisplayName(string Version, string DisplayName, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parameters  
 *版本*  
 包含报表服务器数据库的版本字符串的字符串。  
  
 *DisplayName*  
 [out] 包含与所提供版本相对应的显示名称的字符串。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="remarks"></a>注释  
 下表显示的是从数据库版本到显示字符串的映射。  
  
|**发行版本**|**版本**|**显示名称**|  
|-----------------|-----------------|----------------------|  
|RS 2005 SP2|@DBVersion= C.0.8.54|SQL Server 2005 SP2|  
|RS 2005 SP1|@DBVersion= C.0.8.43|SQL Server 2005 SP1|  
|RS 2005 RTM|@DBVersion= C.0.8.40|SQL Server 2005|  
|RS 2000 SP2|@DBVersion= C.0.6.54|SQL Server 2000 SP2|  
|RS 2000 SP1|@DBVersion= C.0.6.51|SQL Server 2000 SP1|  
|RS 2000 RTM|@DBVersion= C.0.6.43|SQL Server 2000|  
|修补程序||最接近的适用版本|  
  
 如果版本早于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000，返回的 HRESULT 为 ACT_E_BAD_VERSION。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="requirements"></a>要求  
 **命名空间:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
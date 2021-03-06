---
title: 创建IDispatchSTA转发器功能 - WPF非托管 API 引用
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- CreateIDispatchSTAForwarder
api_location:
- PresentationHost_v0400.dll
ms.assetid: 57a02dfa-f091-4ace-9c06-1f4ab52b3527
ms.openlocfilehash: e151ffa6eb5f1dc7479c699e0d7f9f3f57833ebd
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174714"
---
# <a name="createidispatchstaforwarder-function-wpf-unmanaged-api-reference"></a>创建IDispatchSTA转发器功能（WPF非托管 API 参考）
此 API 支持 Windows 演示基础 （WPF） 基础结构，不用于直接从代码中使用。  
  
 由 Windows 演示基础 （WPF） 基础结构用于线程和窗口管理。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CreateIDispatchSTAForwarder(  
   __in IDispatch *pDispatchDelegate,
   __deref_out IDispatch **ppForwarder  
)  
```  
  
## <a name="parameters"></a>parameters  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 p调度委托  
 指向接口的`IDispatch`指针。  
  
 pp 转发器  
 指向接口地址的`IDispatch`指针。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[.NET 框架系统要求](../../get-started/system-requirements.md)。  
  
 **Dll：**  
  
 在 .NET 框架 3.0 和 3.5 中：演示HostDLL.dll  
  
 在 .NET 框架 4 及更高版本：PresentationHost_v0400.dll  
  
 **.NET 框架版本：**[!INCLUDE[net_current_v30plus](../../../../includes/net-current-v30plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [WPF 非托管 API 参考](wpf-unmanaged-api-reference.md)

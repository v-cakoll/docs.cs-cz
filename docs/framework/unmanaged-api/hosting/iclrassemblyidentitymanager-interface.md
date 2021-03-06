---
title: ICLRAssemblyIdentityManager – rozhraní
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager
helpviewer_keywords:
- ICLRAssemblyIdentityManager interface [.NET Framework hosting]
ms.assetid: 6a81c6fe-cc22-4062-ae27-d6eeee03a7b9
topic_type:
- apiref
ms.openlocfilehash: 3611de471001d31c40984e71d49ce376bb3e4607
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504287"
---
# <a name="iclrassemblyidentitymanager-interface"></a>ICLRAssemblyIdentityManager – rozhraní
Poskytuje metody, které podporují komunikaci mezi hostitelem a modulem CLR (Common Language Runtime) o sestaveních.  
  
## <a name="methods"></a>Metody  
  
|Metoda|Description|  
|------------|-----------------|  
|[GetBindingIdentityFromFile – metoda](iclrassemblyidentitymanager-getbindingidentityfromfile-method.md)|Získá datovou vazbu identity sestavení pro sestavení v zadané cestě k souboru.|  
|[GetBindingIdentityFromStream – metoda](iclrassemblyidentitymanager-getbindingidentityfromstream-method.md)|Získá kanonická data identity sestavení pro sestavení v zadaném datovém proudu.|  
|[GetCLRAssemblyReferenceList – metoda](iclrassemblyidentitymanager-getclrassemblyreferencelist-method.md)|Načte instanci [ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md) ze zadaného seznamu částečných identit sestavení.|  
|[GetProbingAssembliesFromReference – metoda](iclrassemblyidentitymanager-getprobingassembliesfromreference-method.md)|Získá enumerátor [ICLRProbingAssemblyEnum –](iclrprobingassemblyenum-interface.md) pro identity sestavení odkazované sestavením se zadanou identitou.|  
|[GetReferencedAssembliesFromFile – metoda](iclrassemblyidentitymanager-getreferencedassembliesfromfile-method.md)|Získá instanci [ICLRReferenceAssemblyEnum –](iclrreferenceassemblyenum-interface.md) , která obsahuje seznam sestavení, na která odkazuje sestavení v zadané cestě k souboru.|  
|[GetReferencedAssembliesFromStream – metoda](iclrassemblyidentitymanager-getreferencedassembliesfromstream-method.md)|Získá ukazatel na `ICLRReferenceAssemblyEnum` objekt, který obsahuje data identity sestavení pro sestavení, na která odkazuje sestavení v zadaném proudu.|  
|[IsStronglyNamed – metoda](iclrassemblyidentitymanager-isstronglynamed-method.md)|Získá hodnotu, která označuje, zda je zadané sestavení silně pojmenované.|  
  
## <a name="remarks"></a>Poznámky  
 Slouží `ICLRAssemblyIdentityManager` k získání instancí `ICLRAssemblyReferenceList` a k zobrazení výčtu identit sestavení.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../get-started/system-requirements.md).  
  
 **Hlavička:** MSCorEE. h  
  
 **Knihovna:** Zahrnuto jako prostředek v knihovně MSCorEE. dll  
  
 **Verze .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ICLRAssemblyReferenceList – rozhraní](iclrassemblyreferencelist-interface.md)
- [ICLRProbingAssemblyEnum – rozhraní](iclrprobingassemblyenum-interface.md)
- [Rozhraní pro hostování](hosting-interfaces.md)

---
title: COR_GC_STAT_TYPES – výčet
ms.date: 03/30/2017
api_name:
- COR_GC_STAT_TYPES
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STAT_TYPES
helpviewer_keywords:
- COR_GC_STAT_TYPES enumeration [.NET Framework hosting]
ms.assetid: fc51d6db-f7f8-408b-b93d-c166fc712c99
topic_type:
- apiref
ms.openlocfilehash: d7e78dfc4beba67cc376b221d0cd49f7200f5d23
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501700"
---
# <a name="cor_gc_stat_types-enumeration"></a>COR_GC_STAT_TYPES – výčet
Určuje statistiku, která má být zaznamenána pro uvolňování paměti.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
typedef enum {  
    COR_GC_COUNTS                 = 0x00000001  
    COR_GC_MEMORYUSAGE            = 0x00000002  
} COR_GC_STAT_TYPES;  
```  
  
## <a name="remarks"></a>Poznámky  
 Tento výčet Určuje, které statistiky ve [COR_GC_STATS](cor-gc-stats-structure.md) struktuře mají být nastaveny pomocí metody [ICLRGCManager:: getstatistics](iclrgcmanager-getstats-method.md) .  
  
## <a name="members"></a>Členové  
  
|Člen|Description|  
|------------|-----------------|  
|`COR_GC_COUNTS`|Zaznamenává počet uvolňování paměti provedených pro každou generaci.|  
|`COR_GC_MEMORYUSAGE`|Zaznamenává využití paměti a statistiky velikosti uvolňování paměti.|  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../get-started/system-requirements.md).  
  
 **Hlavička:** GCHost. idl, GCHost. h  
  
 **Verze .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [COR_GC_STATS – struktura](cor-gc-stats-structure.md)
- [Výčty hostování](hosting-enumerations.md)

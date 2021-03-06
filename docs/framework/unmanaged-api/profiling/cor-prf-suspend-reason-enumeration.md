---
title: COR_PRF_SUSPEND_REASON – výčet
ms.date: 03/30/2017
api_name:
- COR_PRF_SUSPEND_REASON
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_SUSPEND_REASON
helpviewer_keywords:
- COR_PRF_SUSPEND_REASON enumeration [.NET Framework profiling]
ms.assetid: 75594833-bed3-47b2-a426-b75c5fe6fbcf
topic_type:
- apiref
ms.openlocfilehash: fdbcbb2da8f449b9275d820763c2a94cca86cd1e
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500751"
---
# <a name="cor_prf_suspend_reason-enumeration"></a>COR_PRF_SUSPEND_REASON – výčet
Označuje důvod, proč je modul runtime pozastaven.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
typedef enum {  
    COR_PRF_SUSPEND_OTHER                   = 0x00,  
    COR_PRF_SUSPEND_FOR_GC                  = 0x01,  
    COR_PRF_SUSPEND_FOR_APPDOMAIN_SHUTDOWN  = 0x02,  
    COR_PRF_SUSPEND_FOR_CODE_PITCHING       = 0x03,  
    COR_PRF_SUSPEND_FOR_SHUTDOWN            = 0x04,  
    COR_PRF_SUSPEND_FOR_INPROC_DEBUGGER     = 0x06,  
    COR_PRF_SUSPEND_FOR_GC_PREP             = 0x07,    COR_PRF_SUSPEND_FOR_REJIT               = 8  
} COR_PRF_SUSPEND_REASON;  
```  
  
## <a name="members"></a>Členové  
  
|Člen|Description|  
|------------|-----------------|  
|`COR_PRF_FIELD_SUSPEND_OTHER`|Modul runtime je pozastaven z nespecifikovaného důvodu.|  
|`COR_PRF_FIELD_SUSPEND_FOR_GC`|Modul runtime je pozastaven na obsluhu žádosti o uvolnění paměti.<br /><br /> Zpětná volání související s uvolňováním paměti nastávají mezi zpětnými voláními [ICorProfilerCallback:: RuntimeSuspendFinished –](icorprofilercallback-runtimesuspendfinished-method.md) a [ICorProfilerCallback:: RuntimeResumeStarted –](icorprofilercallback-runtimeresumestarted-method.md) .|  
|`COR_PRF_FIELD_SUSPEND_FOR_APPDOMAIN_SHUTDOWN`|Modul runtime je pozastaven, aby bylo `AppDomain` možné vypnout.<br /><br /> I když je modul runtime pozastaven, modul runtime určí, která vlákna jsou v modulu `AppDomain` , který je právě vypnutý, a nastaví je pro přerušení při obnovení. Během tohoto pozastavení nejsou k dispozici žádná `AppDomain` konkrétní zpětná volání.|  
|`COR_PRF_FIELD_SUSPEND_FOR_CODE_PITCHING`|Modul runtime je pozastaven, aby mohlo dojít k rozteči kódu.<br /><br /> Rozteč kódu platí pouze v případě, že je kompilátor JIT (just-in-time) aktivní se zapnutým příznakem pro rozteč kódu. Zpětná volání pro rozteč kódu se vyskytují `ICorProfilerCallback::RuntimeSuspendFinished` mezi `ICorProfilerCallback::RuntimeResumeStarted` zpětnými voláními a. **Poznámka:**  Kompilátor JIT CLR nemění funkce v .NET Framework verze 2,0, takže se tato hodnota nepoužívá v 2,0.|  
|`COR_PRF_FIELD_SUSPEND_FOR_SHUTDOWN`|Modul runtime je pozastaven, aby mohl být vypnut. Aby bylo možné operaci dokončit, je nutné pozastavit všechna vlákna.|  
|`COR_PRF_FIELD_SUSPEND_FOR_INPROC_DEBUGGER`|Modul runtime je pozastaven pro vnitroprocesové ladění.|  
|`COR_PRF_FIELD_SUSPEND_FOR_GC_PREP`|Modul runtime je pozastaven pro přípravu na uvolnění paměti.|  
|`COR_PRF_SUSPEND_FOR_REJIT`|Modul runtime je pozastaven pro rekompilaci JIT.|  
  
## <a name="remarks"></a>Poznámky  
 Všechna vlákna modulu runtime, která jsou v nespravovaném kódu, mohou pokračovat v běhu, dokud se nepokusí znovu zadat modul runtime. v takovém případě budou také pozastaveny, dokud modul runtime nebude pokračovat. To platí také pro nová vlákna, která vstupují do modulu runtime. Všechna vlákna v modulu runtime jsou okamžitě pozastavena, pokud jsou v kódu přerušitelné, nebo se po zobrazení výzvy k tomu, že mají přístup ke kódu přerušitelné, pozastaví.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../get-started/system-requirements.md).  
  
 **Hlavička:** CorProf. idl, CorProf. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [Výčty pro profilaci](profiling-enumerations.md)

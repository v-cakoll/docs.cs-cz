---
title: 'ICorProfilerCallback7:: ModuleInMemorySymbolsUpdated – metoda'
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback7.ModuleInMemorySymbolsUpdated
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.assetid: f362a896-3247-4894-9727-e48dbbcd2c78
ms.openlocfilehash: c7e53816c2f571fe6ff68b517ed827459a0f1562
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499087"
---
# <a name="icorprofilercallback7moduleinmemorysymbolsupdated-method"></a>ICorProfilerCallback7:: ModuleInMemorySymbolsUpdated – metoda
[Podporováno v .NET Framework 4.6.1 a novějších verzích]  
  
 Upozorní profiler vždy, když je aktualizován datový proud symbolu přidružený k modulu v paměti.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT ModuleInMemorySymbolsUpdated(  
     ModuleID moduleId  
);  
```  
  
## <a name="parameters"></a>Parametry  
 pro`moduleId`  
 Identifikátor modulu v paměti, jehož datový proud symbolů je aktualizovaný.  
  
## <a name="remarks"></a>Poznámky  
 Toto zpětné volání je řízeno nastavením příznaku masky události [COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED](cor-prf-high-monitor-enumeration.md) při volání metody [Icorprofilercallback5 –:: SetEventMask2 –](icorprofilerinfo5-seteventmask2-method.md) .  
  
> [!NOTE]
> Tato událost není aktuálně vyvolána pro symboly implicitně vytvořené nebo upravené prostřednictvím <xref:System.Reflection.Emit> rozhraní API.  
  
 I když jsou symboly poskytovány před voláním jednoho z přetížení spravovaných <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> metod, které obsahují `rawSymbolStore` argument pro určení symbolů pro sestavení, modul runtime nemusí ve skutečnosti přidružit symbolické údaje k modulu, dokud nedošlo ke zpětnému volání [ModuleLoadFinished –](icorprofilercallback-moduleloadfinished-method.md) . Tato událost poskytuje později možnost shromažďovat symboly pro tyto moduly.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../get-started/system-requirements.md).  
  
 **Hlavička:** CorProf. idl, CorProf. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:**[!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]  
  
## <a name="see-also"></a>Viz také:

- [ModuleLoadFinished – metoda](icorprofilercallback-moduleloadfinished-method.md)
- [Metoda SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)
- [ICorProfilerCallback7 – rozhraní](icorprofilercallback7-interface.md)

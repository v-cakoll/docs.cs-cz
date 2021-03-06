---
title: ICorDebugEval::CreateValue – metoda
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CreateValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CreateValue
helpviewer_keywords:
- ICorDebugEval::CreateValue method [.NET Framework debugging]
- CreateValue method [.NET Framework debugging]
ms.assetid: 9a1c0b47-6f10-4fcb-844a-4ab2d7990140
topic_type:
- apiref
ms.openlocfilehash: 55888786fdd8ff2b1d5610a74ee729db0d4fcfde
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976249"
---
# <a name="icordebugevalcreatevalue-method"></a>ICorDebugEval::CreateValue – metoda
Vytvoří hodnotu zadaného typu s počáteční hodnotou 0 nebo null.  
  
 Tato metoda je zastaralá ve verzi .NET Framework 2,0. Místo toho použijte [ICorDebugEval2:: createvaluefortype –](icordebugeval2-createvaluefortype-method.md) .  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT CreateValue (  
    [in] CorElementType     elementType,  
    [in] ICorDebugClass     *pElementClass,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>Parametry  
 `elementType`  
 pro Hodnota výčtu [CorElementType –](../metadata/corelementtype-enumeration.md) , která určuje typ hodnoty.  
  
 `pElementClass`  
 pro Ukazatel na objekt [ICorDebugClass](icordebugclass-interface.md) , který určuje třídu hodnoty, pokud typ není primitivní typ.  
  
 `ppValue`  
 mimo Ukazatel na adresu objektu "ICorDebugValue", který představuje hodnotu.  
  
## <a name="remarks"></a>Poznámky  
 `CreateValue`vytvoří `ICorDebugValue` objekt daného typu pro výhradní účely jeho použití ve vyhodnocení funkce. Tento objekt hodnoty lze použít k předání konstant uživatele jako parametrů.  
  
 Pokud je typ hodnoty primitivní typ, jeho počáteční hodnota je nula nebo null. Pomocí [ICorDebugGenericValue:: SetValue](icordebuggenericvalue-setvalue-method.md) nastavte hodnotu primitivního typu.  
  
 Pokud `elementType` je hodnota ELEMENT_TYPE_CLASS, získáte "ICorDebugReferenceValue" (vrácený v `ppValue`) reprezentující odkaz na objekt null. Tento objekt lze použít k předání hodnoty null do vyhodnocení funkce, které má parametry objektu reference. Nemůžete nastavit `ICorDebugValue` na cokoli; vždycky zůstane null.  
  
## <a name="requirements"></a>Požadavky  
 **Platformy:** Viz [požadavky na systém](../../get-started/system-requirements.md).  
  
 **Hlavička:** CorDebug. idl, CorDebug. h  
  
 **Knihovna:** CorGuids. lib  
  
 **Verze .NET Framework:** 1,1, 1,0  
  
## <a name="see-also"></a>Viz také

- [CreateValueForType – metoda](icordebugeval2-createvaluefortype-method.md)
- [ICorDebugEval – rozhraní](icordebugeval-interface.md)

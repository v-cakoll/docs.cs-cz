---
title: CreateALink – funkce
ms.date: 03/30/2017
api_name:
- CreateALink
api_location:
- alink.dll
api_type:
- DLLExport
f1_keywords:
- CreateALink
helpviewer_keywords:
- CreateALink function
- Alink API, CreateALink function
ms.assetid: fc73bcb9-6af6-44d8-bc39-2f4400325dae
topic_type:
- apiref
ms.openlocfilehash: 9165a4db7e65fb0f409a902b06d32e9c2988aa69
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/23/2019
ms.locfileid: "74446555"
---
# <a name="createalink-function"></a>CreateALink – funkce
Vytvoří instanci linkeru sestavení a nastaví ukazatel na zadané rozhraní.  
  
## <a name="syntax"></a>Syntaxe  
  
```cpp  
HRESULT CreateALink (  
   REFIID riid,  
   IUnknown **ppInterface  
);  
```  
  
## <a name="parameters"></a>Parametry  
  
|Parametr|Popis|  
|---------------|-----------------|  
|`riid`|Fyzický název jednoho z rozhraní linkeru sestavení.|  
|`ppInterface`|Umístění, které po úspěšném dokončení obsahuje ukazatel na rozhraní `riid`.|  
  
## <a name="requirements"></a>Požadavky  
 **Knihovna**: ALink. dll  
  
## <a name="see-also"></a>Viz také:

- [Al.exe (linker sestavení)](../../tools/al-exe-assembly-linker.md)

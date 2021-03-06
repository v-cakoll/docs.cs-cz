---
title: Short – datový typ
ms.date: 01/31/2018
f1_keywords:
- vb.Short
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- S literal type character [Visual Basic]
- Short data type
- literal type characters [Visual Basic], S
ms.assetid: 65fcbcf3-a841-400e-885e-301497729a8b
ms.openlocfilehash: 176d27c86127dac1d9c9c0231790f7a5c2a2fefc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415554"
---
# <a name="short-data-type-visual-basic"></a>Short – datový typ (Visual Basic)

Obsahuje 16bitová celá čísla se znaménkem (2 bajty), která mají rozsah hodnot od-32 768 do 32 767.  
  
## <a name="remarks"></a>Poznámky  

 `Short`Datový typ použijte k omezení celočíselných hodnot, které nevyžadují plnou šířku dat `Integer` . V některých případech může modul CLR (Common Language Runtime) sbalit `Short` proměnné společně a ušetřit spotřebu paměti.  
  
 Výchozí hodnota `Short` je 0.  
  
## <a name="literal-assignments"></a>Přiřazení literálů

Můžete deklarovat a inicializovat `Short` proměnnou přiřazením desítkového literálu, šestnáctkového literálu, osmičkového literálu nebo (začínajícího Visual Basic 2017) binárního literálu. Pokud je celočíselný literál mimo rozsah `Short` (tj. Pokud je menší <xref:System.Int16.MinValue?displayProperty=nameWithType> nebo větší než <xref:System.Int16.MaxValue?displayProperty=nameWithType> , dojde k chybě kompilace.

V následujícím příkladu jsou celá čísla rovnající se 1 034, která jsou reprezentována jako Desítková, šestnáctková a binární literála, implicitně převedena z [celého čísla](integer-data-type.md) na `Short` hodnoty.

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Short)]

> [!NOTE]
> Použijte předponu `&h` nebo `&H` k označení šestnáctkového literálu, předpony `&b` nebo `&B` označení binárního literálu a předpony `&o` nebo `&O` k označení osmičkového literálu. Desítkové literály nemají žádnou předponu.

Počínaje Visual Basic 2017 můžete také použít znak podtržítka, `_` jako oddělovač číslic pro zlepšení čitelnosti, jak ukazuje následující příklad.

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ShortS)]

Počínaje Visual Basic 15,5 můžete také použít znak podtržítka ( `_` ) jako úvodní oddělovač mezi předponou a šestnáctkovou, binární nebo osmičkovou číslicí. Příklad:

```vb
Dim number As Short = &H_3264
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

Číselné literály mohou také obsahovat `S` [znak typu](../../programming-guide/language-features/data-types/type-characters.md) , který označuje `Short` datový typ, jak ukazuje následující příklad.

```vb
Dim number = &H_3264S
```

## <a name="programming-tips"></a>Tipy k programování

- **Rozšiřující.** `Short`Datový typ se rozšíří na `Integer` ,, `Long` , `Decimal` `Single` nebo `Double` . To znamená, že můžete převést `Short` na některý z těchto typů bez výskytu <xref:System.OverflowException?displayProperty=nameWithType> chyby.  
  
- **Znaky typu.** Připojení znaku literálového typu `S` k literálu vynutí tento `Short` datový typ. `Short`nemá žádný znak typu identifikátoru.  
  
- **Typ rozhraní.** Odpovídající typ v .NET Framework je <xref:System.Int16?displayProperty=nameWithType> Struktura.  
  
## <a name="see-also"></a>Viz také

- <xref:System.Int16?displayProperty=nameWithType>
- [Datové typy](index.md)
- [Funkce pro převod typů](../functions/type-conversion-functions.md)
- [Souhrn převodu](../keywords/conversion-summary.md)
- [Integer – datový typ](integer-data-type.md)
- [Long – datový typ](long-data-type.md)
- [Účinné používání datových typů](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)

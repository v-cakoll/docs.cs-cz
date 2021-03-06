---
title: Předávání argumentů podle hodnoty a odkazu
ms.date: 07/20/2015
helpviewer_keywords:
- ByRef keyword [Visual Basic], passing arguments by reference
- Visual Basic code, procedures
- passing arguments [Visual Basic], by value or by reference
- ByVal keyword [Visual Basic], passing arguments by value
- arguments [Visual Basic], passing by value or by reference
- argument passing [Visual Basic], by value or by reference
ms.assetid: fd8a9de6-7178-44d5-a9bf-458d4ad907c2
ms.openlocfilehash: 3dd4be6ea6de9dfe8eb165e5d4ba9a990fc40585
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363951"
---
# <a name="passing-arguments-by-value-and-by-reference-visual-basic"></a>Předávání argumentů podle hodnoty a odkazu (Visual Basic)
V Visual Basic můžete předat argument proceduře *podle hodnoty* nebo *odkazu*. Toto je označováno jako *mechanismus předávání*a určuje, zda procedura může upravit programovací element podkladové argumentu v volajícím kódu. Deklarace procedury určuje mechanismus předávání pro každý parametr zadáním klíčového slova [ByVal](../../../language-reference/modifiers/byval.md) nebo [ByRef](../../../language-reference/modifiers/byref.md) .  
  
## <a name="distinctions"></a>Rozdíly  
 Při předání argumentu proceduře si uvědomte několik různých odlišností, které vzájemně komunikují:  
  
- Zda je základní prvek programování upravitelný nebo neupravitelný  
  
- Určuje, zda je argument sám upravitelný nebo neupravitelný.  
  
- Určuje, zda je argument předáván hodnotou nebo odkazem.  
  
- Určuje, zda je datovým typem argumentu typ hodnoty nebo typ odkazu.  
  
 Další informace naleznete v tématu [rozdíly mezi upravitelnými a neupravitelnými argumenty](./differences-between-modifiable-and-nonmodifiable-arguments.md) a [rozdíly mezi předáním argumentu podle hodnoty a odkazu](./differences-between-passing-an-argument-by-value-and-by-reference.md).  
  
## <a name="choice-of-passing-mechanism"></a>Volba mechanismu předávání  
 Měli byste zvolit pečlivě mechanismus předávání pro každý argument.  
  
- **Ochrana**. V rámci volby mezi dvěma mechanismy předávání je nejdůležitějším kritériem riziko volání proměnných, které se mají změnit. Výhodou předání argumentu `ByRef` je, že procedura může vrátit hodnotu volajícímu kódu prostřednictvím tohoto argumentu. Výhodou předání argumentu `ByVal` je, že chrání proměnnou před změnou pomocí procedury.  
  
- **Výkon**. I když mechanismus předávání může ovlivnit výkon kódu, rozdíl je obvykle nevýznamný. Jedinou výjimkou je předaný typ hodnoty `ByVal` . V tomto případě Visual Basic zkopíruje celý obsah tohoto argumentu. Proto pro velký typ hodnoty, jako je například struktura, může být efektivnější ho předat `ByRef` .  
  
     U typů odkazů se kopíruje jenom ukazatel na data (čtyři bajty na 32-bitových platformách, osm bajtů na 64 64bitových platformách). Proto můžete předat argumenty typu `String` nebo `Object` podle hodnoty bez poškození výkonu.  
  
## <a name="determination-of-the-passing-mechanism"></a>Určení mechanismu předávání  
 Deklarace procedury určuje mechanismus předávání pro každý parametr. Volající kód nemůže přepsat `ByVal` mechanismus.  
  
 Pokud je parametr deklarován pomocí `ByRef` , volající kód může vynutit mechanismus `ByVal` uzavřením názvu argumentu do závorek v volání. Další informace naleznete v tématu [How to: Force a argument by měl být předán hodnotou](./how-to-force-an-argument-to-be-passed-by-value.md).  
  
 Výchozí hodnotou v Visual Basic je předání argumentů podle hodnoty.  
  
## <a name="when-to-pass-an-argument-by-value"></a>Kdy předat argument podle hodnoty  
  
- Pokud je element volajícího kódu podkladovým argumentem neupravitelný element, deklarujte odpovídající parametr [ByVal](../../../language-reference/modifiers/byval.md). Žádný kód nemůže změnit hodnotu neupravitelného prvku.  
  
- Pokud je podkladový element upravitelný, ale nechcete, aby procedura mohla měnit jeho hodnotu, deklarujte parametr `ByVal` . Pouze volající kód může změnit hodnotu upravitelného prvku předaného hodnotou.  
  
## <a name="when-to-pass-an-argument-by-reference"></a>Kdy předat argument odkazem  
  
- Pokud má procedura originální nutnost změnit základní prvek v volajícím kódu, deklarujte odpovídající parametr [ByRef](../../../language-reference/modifiers/byref.md).  
  
- Je-li správné provedení kódu závislé na postupu změny podkladového prvku v kódu volajícího, deklarujte parametr `ByRef` . Pokud je předáte podle hodnoty nebo pokud volající kód přepíše `ByRef` mechanismus předávání uzavřením argumentu v závorkách, volání procedury může způsobit neočekávané výsledky.  
  
## <a name="example"></a>Příklad  
  
### <a name="description"></a>Description  
 Následující příklad ilustruje, kdy předat argumenty podle hodnoty a kdy je předat odkazem. Procedura `Calculate` má `ByVal` parametr a a `ByRef` . S ohledem na úrokovou sazbu, `rate` a součtem peněz, se `debt` úkolem této procedury je vypočítat novou hodnotu `debt` , která je výsledkem použití úrokové sazby na původní hodnotu `debt` . Vzhledem `debt` k tomu `ByRef` , že parametr je, nový součet se projeví v hodnotě argumentu v volajícím kódu, který odpovídá `debt` . Parametr `rate` je `ByVal` parametr, protože `Calculate` by neměl měnit jeho hodnotu.  
  
### <a name="code"></a>Kód  
 [!code-vb[VbVbcnProcedures#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class2.vb#74)]  
  
## <a name="see-also"></a>Viz také

- [Procedury](./index.md)
- [Parametry a argumenty procedury](./procedure-parameters-and-arguments.md)
- [Postupy: Předání argumentů proceduře](./how-to-pass-arguments-to-a-procedure.md)
- [Postupy: Změna hodnoty argumentu procedury](./how-to-change-the-value-of-a-procedure-argument.md)
- [Postupy: Ochrana argumentu procedury před změnami hodnoty](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [Postupy: Vynucení předání argumentu podle hodnoty](./how-to-force-an-argument-to-be-passed-by-value.md)
- [Předávání argumentů podle pozice a názvu](./passing-arguments-by-position-and-by-name.md)
- [Typy hodnot a typy odkazu](../data-types/value-types-and-reference-types.md)

---
title: Anonymní funkce – Průvodce programováním v C#
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], as anonymous functions
- anonymous functions [C#]
- anonymous methods [C#]
ms.assetid: 6ce3f04d-0c71-4728-9127-634c7e9a8365
ms.openlocfilehash: c99aaf4f35d2d294a9f07de54129bb3b4fbfbfde
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241900"
---
# <a name="anonymous-functions-c-programming-guide"></a>Anonymní funkce (Průvodce programováním v C#)

Anonymní funkce je "vložený" příkaz nebo výraz, který lze použít všude, kde je očekáván typ delegáta. Můžete ji použít k inicializaci pojmenovaného delegáta nebo ho předat místo pojmenovaného typu delegáta jako parametr metody.

Můžete použít [výraz lambda](lambda-expressions.md) nebo [anonymní metodu](../../language-reference/operators/delegate-operator.md) pro vytvoření anonymní funkce. Doporučujeme použít výrazy lambda, protože poskytují výstižnější a výrazný způsob psaní vloženého kódu. Na rozdíl od anonymních metod lze některé typy výrazů lambda převést na typy stromu výrazů.

## <a name="the-evolution-of-delegates-in-c"></a>Vývoj delegátů v jazyce C\#

 V C# 1,0 jste vytvořili instanci delegáta explicitně inicializací s metodou, která byla definována jinde v kódu. C# 2,0 představil koncept anonymních metod jako způsob zápisu nepojmenovaných bloků vložených příkazů, které mohou být provedeny při volání delegáta. C# 3,0 představil výrazy lambda, které jsou podobné v konceptu anonymním metodám, ale častěji a stručnější. Tyto dvě funkce se společně nazývají *anonymní funkce*. Obecně platí, že aplikace, které cílí na .NET Framework 3,5 nebo novější, by měly používat výrazy lambda.  
  
 Následující příklad ukazuje vývoj vytvoření delegáta z C# 1,0 na C# 3,0:  
  
 [!code-csharp[csProgGuideLINQ#65](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#65)]  
  
## <a name="c-language-specification"></a>specifikace jazyka C#

Další informace naleznete v části [výrazy anonymní funkce](~/_csharplang/spec/expressions.md#anonymous-function-expressions) [specifikace jazyka C#](~/_csharplang/spec/introduction.md).
  
## <a name="see-also"></a>Viz také

- [Příkazy, výrazy a operátory](./index.md)
- [Výrazy lambda](./lambda-expressions.md)
- [Delegáti](../delegates/index.md)
- [Stromy výrazů (C#)](../concepts/expression-trees/index.md)

---
title: do – reference jazyka C#
ms.date: 05/28/2018
f1_keywords:
- do_CSharpKeyword
- do
helpviewer_keywords:
- do keyword [C#]
ms.assetid: 50725f79-9ba6-4898-aa78-6e331568a1bb
ms.openlocfilehash: d75dd816278a876fa05d133e5eb189d606300a5c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401924"
---
# <a name="do-c-reference"></a>do (Referenční dokumentace jazyka C#)

`do`Příkaz provede příkaz nebo blok příkazů, zatímco se zadaný logický výraz vyhodnotí jako `true` . Vzhledem k tomu, že tento výraz je vyhodnocen po každém spuštění smyčky, `do-while` smyčka se spustí jednou nebo vícekrát. To se liší od smyčky [while](while.md) , která se spouští nula nebo vícekrát.

V jakémkoli bodě `do` bloku příkazu můžete přerušit smyčku pomocí příkazu [Break](break.md) .

Můžete přímo Krokovat s vyhodnocením `while` výrazu pomocí příkazu [Continue](continue.md) . Pokud se výraz vyhodnotí jako `true` , vykonání pokračuje v prvním příkazu smyčky. V opačném případě spuštění pokračuje v prvním příkazu za smyčkou.

Můžete také ukončit `do-while` smyčku příkazy [goto](goto.md), [return](return.md)nebo [throw](throw.md) .

## <a name="example"></a>Příklad

Následující příklad ukazuje použití `do` příkazu. Vyberte **Spustit** a spusťte ukázkový kód. Potom můžete kód upravit a znovu spustit.

[!code-csharp-interactive[do loop example](snippets/IterationKeywordsExamples.cs#4)]

## <a name="c-language-specification"></a>specifikace jazyka C#

Další informace naleznete v části do [příkazu](~/_csharplang/spec/statements.md#the-do-statement) do v tématu [specifikace jazyka C#](/dotnet/csharp/language-reference/language-specification/introduction).

## <a name="see-also"></a>Viz také

- [Reference jazyka C#](../index.md)
- [Průvodce programováním v C#](../../programming-guide/index.md)
- [Klíčová slova jazyka C#](index.md)
- [while – příkaz](while.md)

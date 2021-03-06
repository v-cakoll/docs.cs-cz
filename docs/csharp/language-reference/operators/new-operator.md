---
title: New – operátor – reference jazyka C#
ms.date: 06/25/2019
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: ed18c42cd28412a967c94a65c2a92b0b75097b52
ms.sourcegitcommit: 5988e9a29cedb8757320817deda3c08c6f44a6aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2020
ms.locfileid: "82199726"
---
# <a name="new-operator-c-reference"></a>New – operátor (Referenční dokumentace jazyka C#)

`new` Operátor vytvoří novou instanci typu.

`new` Klíčové slovo lze použít také jako [Modifikátor deklarace člena](../keywords/new-modifier.md) nebo [omezení obecného typu](../keywords/new-constraint.md).

## <a name="constructor-invocation"></a>Vyvolání konstruktoru

Chcete-li vytvořit novou instanci typu, obvykle vyvoláte jeden z [konstruktorů](../../programming-guide/classes-and-structs/constructors.md) tohoto typu pomocí `new` operátoru:

[!code-csharp-interactive[invoke constructor](snippets/NewOperator.cs#Constructor)]

Můžete použít [inicializátor objektu nebo kolekce](../../programming-guide/classes-and-structs/object-and-collection-initializers.md) s `new` operátorem pro vytvoření instance a inicializaci objektu v jednom příkazu, jak ukazuje následující příklad:

[!code-csharp-interactive[constructor with initializer](snippets/NewOperator.cs#ConstructorWithInitializer)]

## <a name="array-creation"></a>Vytvoření pole

`new` Operátor můžete také použít k vytvoření instance pole, jak ukazuje následující příklad:

[!code-csharp-interactive[create array](snippets/NewOperator.cs#Array)]

Pomocí syntaxe inicializace pole vytvořte instanci pole a naplňte ji prvky v jednom příkazu. Následující příklad ukazuje různé způsoby, jak to lze provést:

[!code-csharp-interactive[initialize array](snippets/NewOperator.cs#ArrayInitialization)]

Další informace o polích naleznete v tématu [Arrays](../../programming-guide/arrays/index.md).

## <a name="instantiation-of-anonymous-types"></a>Vytváření instancí anonymních typů

Chcete-li vytvořit instanci [anonymního typu](../../programming-guide/classes-and-structs/anonymous-types.md), použijte syntaxi `new` inicializátoru operátoru a objektu:

[!code-csharp-interactive[anonymous type](snippets/NewOperator.cs#AnonymousType)]

## <a name="destruction-of-type-instances"></a>Zničení instancí typů

Nemusíte zničit dřívější vytvořené instance typu. Instance obou typů odkaz i hodnota jsou zničeny automaticky. Instance typů hodnot jsou zničeny ihned po zničení kontextu, který je obsahuje. Instance typů odkazů jsou zničeny systémem [uvolňování paměti](../../../standard/garbage-collection/index.md) v některém nespecifikovaném čase po odebrání posledního odkazu na ně.

U instancí typu, které obsahují nespravované prostředky, například popisovač souboru, se doporučuje použít deterministické vyčištění, aby bylo zajištěno, že prostředky, které obsahují, budou zveřejněny co nejdříve. Další informace najdete v tématu Reference <xref:System.IDisposable?displayProperty=nameWithType> k rozhraní API a v článku o [příkazu Using](../keywords/using-statement.md) .

## <a name="operator-overloadability"></a>Přetížení operátoru

Uživatelsky definovaný typ nemůže přetížit `new` operátor.

## <a name="c-language-specification"></a>specifikace jazyka C#

Další informace naleznete v části [New operator](~/_csharplang/spec/expressions.md#the-new-operator) v tématu [specifikace jazyka C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Viz také

- [Referenční dokumentace k jazyku C#](../index.md)
- [Operátory jazyka C#](index.md)
- [Inicializátory objektu a kolekce](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)

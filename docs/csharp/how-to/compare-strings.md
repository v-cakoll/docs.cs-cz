---
title: Porovnávání řetězců – Průvodce C#
description: Přečtěte si, jak porovnat a seřadit řetězcové hodnoty s použitím nebo bez případu s použitím řazení konkrétní jazykové verze nebo bez něj.
ms.date: 10/03/2018
helpviewer_keywords:
- strings [C#], comparison
- comparing strings [C#]
ms.openlocfilehash: d1ea0fc3573714347580a2aaded2d0f3118681a8
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324185"
---
# <a name="how-to-compare-strings-in-c"></a>Jak porovnat řetězce v jazyce C\#

Porovnáte řetězce, abyste odpověděli na jednu ze dvou otázek: "jsou tyto dva řetězce stejné?" nebo "v jakém pořadí mají být tyto řetězce umístěny při jejich řazení?"

Tyto dvě otázky jsou složité faktory, které ovlivňují porovnávání řetězců:

- Můžete zvolit ordinální nebo jazykové porovnání.
- Můžete si vybrat, jestli se jedná o případové věci.
- Můžete zvolit porovnání specifické pro jazykovou verzi.
- Jazykové porovnání představují jazykovou verzi a závislé na platformě.

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

Při porovnávání řetězců definujete mezi nimi objednávku. K řazení posloupnosti řetězců slouží porovnávání. Jakmile je sekvence ve známém pořadí, je snazší hledat jak pro software, tak pro lidi. Jiné porovnání mohou kontrolovat, zda jsou řetězce stejné. Tyto sameness kontroly jsou podobné rovnosti, ale některé rozdíly, například rozdíly v různých velikostech, mohou být ignorovány.

## <a name="default-ordinal-comparisons"></a>Výchozí ordinální porovnávání

Standardně nejběžnější operace:

- <xref:System.String.CompareTo%2A?displayProperty=nameWithType>
- <xref:System.String.Equals%2A?displayProperty=nameWithType>
- <xref:System.String.op_Equality%2A?displayProperty=nameWithType>a, <xref:System.String.op_Inequality%2A?displayProperty=nameWithType> to znamená [operátory rovnosti `==` a `!=` ](../language-reference/operators/equality-operators.md#string-equality)v uvedeném pořadí

provede porovnávání v řádu rozlišující velká a malá písmena a v případě potřeby použije aktuální jazykovou verzi. Následující příklad ukazuje, že:

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet1":::

Výchozí ordinální porovnávání při porovnávání řetězců nebere v úvahu jazyková pravidla. Porovnává binární hodnotu každého <xref:System.Char> objektu ve dvou řetězcích. V důsledku toho výchozí ordinální porovnávání rozlišuje i velká a malá písmena.

Test rovnosti s <xref:System.String.Equals%2A?displayProperty=nameWithType> `==` operátory a a a se `!=` liší od porovnání řetězců pomocí <xref:System.String.CompareTo%2A?displayProperty=nameWithType> <xref:System.String.Compare(System.String,System.String)?displayProperty=nameWithType)> metod a. I když testy rovnosti provádějí ordinální porovnávání rozlišující velká a malá písmena, metody porovnání provádějí porovnání zohledňující velká a malá písmena s použitím aktuální jazykové verze. Vzhledem k tomu, že výchozí metody porovnání často provádějí různé typy porovnávání, doporučujeme, abyste vždy vymazali záměr kódu tím, že zavoláte přetížení, které explicitně určuje typ porovnání, které má být provedeno.

## <a name="case-insensitive-ordinal-comparisons"></a>Ordinální porovnávání bez rozlišení velkých a malých písmen

<xref:System.String.Equals(System.String,System.StringComparison)?displayProperty=nameWithType>Metoda umožňuje zadat <xref:System.StringComparison> hodnotu<xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType>
pro ordinální porovnávání bez rozlišování velkých a malých písmen. Existuje také statická <xref:System.String.Compare(System.String,System.String,System.StringComparison)?displayProperty=nameWithType> metoda, která provede porovnávání bez rozlišení velkých a malých písmen, pokud zadáte hodnotu <xref:System.StringComparison.OrdinalIgnoreCase?displayProperty=nameWithType> <xref:System.StringComparison> argumentu. Jsou uvedeny v následujícím kódu:

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet2":::

Při porovnávání podle pořadového čísla bez rozlišení velkých a malých písmen tyto metody používají konvence pro používání velkých a malých písmen v [neutrální jazykové verzi](xref:System.Globalization.CultureInfo.InvariantCulture).

## <a name="linguistic-comparisons"></a>Jazyková porovnání

Řetězce lze také seřadit pomocí lingvistických pravidel pro aktuální jazykovou verzi.
Někdy se označuje jako "pořadí řazení slov". Pokud provedete jazykové porovnání, některé nealfanumerické znaky Unicode mohou mít přiřazeny zvláštní váhy. Například spojovník "-" může mít přiřazenou malou váhu, aby se "Co-op" a "Coop" zobrazovaly vedle sebe v pořadí řazení. Kromě toho může být několik znaků Unicode ekvivalentní sekvenci <xref:System.Char> instancí. Následující příklad používá frázi "ty se roztancoval na ulici". v němčině s "SS" (U + 0073 U + 0073) v jednom řetězci a "ß" (U + 00DF) v jiném. V jazyku (ve Windows) se "SS" rovná Esszet německému znaku: "ß" v jazykových verzích "en-US" i "de-DE".

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet3":::

Tato ukázka demonstruje charakter jazykových porovnávání závislých na operačním systému. Hostitelem pro interaktivní okno je hostitel Linux. Jazykové a ordinální porovnávání vytváří stejné výsledky. Pokud spustíte stejnou ukázku na hostiteli Windows, zobrazí se následující výstup:

```console
<coop> is less than <co-op> using invariant culture
<coop> is greater than <co-op> using ordinal comparison
<coop> is less than <cop> using invariant culture
<coop> is less than <cop> using ordinal comparison
<co-op> is less than <cop> using invariant culture
<co-op> is less than <cop> using ordinal comparison
```

V systému Windows se pořadí řazení "COP", "Coop" a "Co-op" mění při změně z lingvistového porovnání na ordinální porovnávání. Dvě německé věty také porovnávají odlišně pomocí různých typů porovnání.

## <a name="comparisons-using-specific-cultures"></a>Porovnání pomocí konkrétní jazykové verze

Tento příklad ukládá <xref:System.Globalization.CultureInfo> objekty pro kultury en-US a de-de.
Porovnání jsou prováděna pomocí <xref:System.Globalization.CultureInfo> objektu pro zajištění porovnání specifického pro jazykovou verzi.

Použitá jazyková verze má vliv na jazyková porovnání. Následující příklad ukazuje výsledky porovnání dvou německých vět pomocí jazykové verze "en-US" a jazykové verze de-DE ":

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet4":::

Porovnávání závislé na jazykové verzi se obvykle používá k porovnání a řazení vstupu řetězců uživateli s jinými řetězci, které uživatelé používají. Tyto znaky a konvence řazení těchto řetězců se mohou lišit v závislosti na národním prostředí počítače uživatele. Dokonce i řetězce, které obsahují identické znaky, mohou být tříděny různě v závislosti na jazykové verzi aktuálního vlákna. Kromě toho vyzkoušejte tento ukázkový kód místně na počítači s Windows a získáte následující výsledky:

```console
<coop> is less than <co-op> using en-US culture
<coop> is greater than <co-op> using ordinal comparison
<coop> is less than <cop> using en-US culture
<coop> is less than <cop> using ordinal comparison
<co-op> is less than <cop> using en-US culture
<co-op> is less than <cop> using ordinal comparison
```

Jazykové porovnání jsou závislé na aktuální jazykové verzi a jsou závislé na operačním systému. Při práci s porovnáváním řetězců Vezměte v úvahu.

## <a name="linguistic-sorting-and-searching-strings-in-arrays"></a>Jazykové řazení a hledání řetězců v polích

Následující příklady ukazují, jak řadit a hledat řetězce v poli pomocí jazykového porovnání závislého na aktuální jazykové verzi. Použijete statické <xref:System.Array> metody, které přijímají <xref:System.StringComparer?displayProperty=nameWithType> parametr.

Tento příklad ukazuje, jak seřadit pole řetězců pomocí aktuální jazykové verze:

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet5":::

Po seřazení pole můžete vyhledat položky pomocí binárního vyhledávání. Binární vyhledávání začíná uprostřed kolekce, aby bylo možné zjistit, která polovina kolekce by obsahovala hledaný řetězec. Každé následné porovnání rozděluje zbývající část kolekce na polovinu.  Pole je řazeno pomocí <xref:System.StringComparer.CurrentCulture?displayProperty=nameWithType> . Místní funkce `ShowWhere` zobrazí informace o tom, kde byl řetězec nalezen. Pokud řetězec nebyl nalezen, vrácená hodnota označuje, kde by byla nalezena.

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet6":::

## <a name="ordinal-sorting-and-searching-in-collections"></a>Ordinální řazení a hledání v kolekcích

Následující kód používá <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> třídu kolekce k ukládání řetězců. Řetězce jsou řazeny pomocí <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> metody. Tato metoda vyžaduje delegáta, který porovnává a řadí dva řetězce. <xref:System.String.CompareTo%2A?displayProperty=nameWithType>Metoda poskytuje funkci porovnání. Spusťte ukázku a sledujte objednávku. Tato operace řazení používá řazení rozlišující velká a malá písmena. Použijte statické <xref:System.String.Compare%2A?displayProperty=nameWithType> metody k určení různých pravidel porovnání.

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet7":::

Po seřazení lze seznam řetězců vyhledat pomocí binárního vyhledávání. Následující příklad ukazuje, jak vyhledat seřazený seznam pomocí stejné funkce porovnání. Místní funkce `ShowWhere` zobrazuje, kde je požadovaný text nebo by byl:

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet8":::

Vždy nezapomeňte použít stejný typ porovnání pro řazení a vyhledávání. Použití různých typů porovnání pro řazení a vyhledávání vytváří neočekávané výsledky.

Třídy kolekce, jako například <xref:System.Collections.Hashtable?displayProperty=nameWithType> , <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> a <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> mají konstruktory, které přijímají <xref:System.StringComparer?displayProperty=nameWithType> parametr, pokud je typ elementů nebo klíčů `string` . Obecně byste měli používat tyto konstruktory, kdykoli je to možné, a zadat buď <xref:System.StringComparer.Ordinal?displayProperty=nameWithType> nebo <xref:System.StringComparer.OrdinalIgnoreCase?displayProperty=nameWithType> .

## <a name="reference-equality-and-string-interning"></a>Referenční rovnost a interning řetězců

Žádná z ukázek se nepoužila <xref:System.Object.ReferenceEquals%2A> . Tato metoda určuje, zda jsou dva řetězce stejného objektu, což může vést k nekonzistentním výsledkům při porovnávání řetězců. Následující příklad ukazuje funkci pro *učně řetězců* jazyka C#. Když program deklaruje dvě nebo více identických řetězcových proměnných, kompilátor je uloží do stejného umístění. Voláním <xref:System.Object.ReferenceEquals%2A> metody můžete vidět, že dva řetězce ve skutečnosti odkazují na stejný objekt v paměti. Použijte <xref:System.String.Copy%2A?displayProperty=nameWithType> metodu pro zamezení interning. Po provedení kopie mají tyto dva řetězce různá umístění úložiště, a to i v případě, že mají stejnou hodnotu. Spuštěním následujícího příkladu zobrazíte tyto řetězce `a` a `b` jsou *interně* , což znamená, že sdílejí stejné úložiště. Řetězce `a` a `c` nejsou.

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/CompareStrings.cs" id="Snippet9":::

> [!NOTE]
> Při testování rovnosti řetězců byste měli použít metody, které explicitně určují, jaký druh porovnání máte v úmyslu provést. Váš kód je mnohem udržovatelnější a čitelný. Použijte přetížení metod <xref:System.String?displayProperty=nameWithType> <xref:System.Array?displayProperty=nameWithType> třídy a, které přijímají <xref:System.StringComparison> parametr výčtu. Určíte, který typ porovnání se má provést. Nepoužívejte `==` operátory a `!=` při testování rovnosti. <xref:System.String.CompareTo%2A?displayProperty=nameWithType>Metody instance vždy provádějí porovnání rozlišující velká a malá písmena. Jsou primárně vhodné pro řazení řetězců abecedně.

Můžete interně vytvořit řetězec nebo načíst odkaz na existující interně volaný řetězec voláním <xref:System.String.Intern%2A?displayProperty=nameWithType> metody. Chcete-li zjistit, zda je řetězec interně, zavolejte <xref:System.String.IsInterned%2A?displayProperty=nameWithType> metodu.

## <a name="see-also"></a>Viz také

- <xref:System.Globalization.CultureInfo?displayProperty=nameWithType>
- <xref:System.StringComparer?displayProperty=nameWithType>
- [Řetězce](../programming-guide/strings/index.md)
- [Porovnávání řetězců](../../standard/base-types/comparing.md)
- [Globalizace a lokalizace aplikací](/visualstudio/ide/globalizing-and-localizing-applications)

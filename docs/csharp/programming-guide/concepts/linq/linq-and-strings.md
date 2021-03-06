---
title: LINQ a řetězce (C#)
description: LINQ může zadávat dotazy a transformovat řetězce a kolekce řetězců. Dotazy LINQ můžete kombinovat s řetězcovými funkcemi C# a regulárními výrazy.
ms.date: 07/20/2015
ms.assetid: dbe2d657-b3f3-487e-b645-21fb2d71cd7b
ms.openlocfilehash: c515a0c56ad6473f93c6339540e4ed0245bb5bd2
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165618"
---
# <a name="linq-and-strings-c"></a>LINQ a řetězce (C#)

LINQ lze použít k dotazování a transformaci řetězců a kolekcí řetězců. Může být obzvláště užitečná pro částečně strukturovaná data v textových souborech. Dotazy LINQ lze kombinovat s tradičními řetězcovými funkcemi a regulárními výrazy. Například můžete použít <xref:System.String.Split%2A?displayProperty=nameWithType> <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> metodu nebo k vytvoření pole řetězců, které můžete následně dotazovat nebo upravit pomocí LINQ. Můžete použít <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> metodu v `where` klauzuli dotazu LINQ. A můžete použít LINQ k dotazování nebo úpravám <xref:System.Text.RegularExpressions.MatchCollection> výsledků vrácených regulárním výrazem.

Pomocí technik popsaných v této části můžete také transformovat částečně strukturovaná textová data do formátu XML. Další informace najdete v tématu [generování XML ze souborů CSV](how-to-generate-xml-from-csv-files.md).

Příklady v této části spadají do dvou kategorií:

## <a name="querying-a-block-of-text"></a>Dotazování na blok textu

Můžete zadávat dotazy, analyzovat a upravovat textové bloky jejich rozdělením do pole Queryable menších řetězců pomocí <xref:System.String.Split%2A?displayProperty=nameWithType> metody nebo <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> metody. Zdrojový text můžete rozdělit na slova, věty, odstavce, stránky nebo jakákoli další kritéria a pak provést další rozdělení, pokud jsou v dotazu potřeba.

- [Jak spočítat výskyty slova v řetězci (LINQ) (C#)](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
  Ukazuje, jak použít LINQ pro jednoduché dotazování nad textem.

- [Dotazování na věty, které obsahují zadanou sadu slov (LINQ) (C#)](how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq.md)

  Ukazuje, jak rozdělit textové soubory na libovolné hranice a jak provádět dotazy proti každé části.

- [Dotazování na znaky v řetězci (LINQ) (C#)](how-to-query-for-characters-in-a-string-linq.md)

  Ukazuje, že řetězec je typu Queryable.

- [Jak kombinovat dotazy LINQ s regulárními výrazy (C#)](how-to-combine-linq-queries-with-regular-expressions.md)

  Ukazuje, jak použít regulární výrazy v dotazech LINQ pro komplexní porovnávání vzorů u filtrovaných výsledků dotazu.

## <a name="querying-semi-structured-data-in-text-format"></a>Dotazování na částečně strukturovaná data ve formátu textu

Mnoho různých typů textových souborů se skládá z řady řádků, často s podobným formátováním, jako jsou například tabulátory nebo soubory oddělené čárkami nebo řádky s pevnou délkou. Po přečtení takového textového souboru do paměti můžete použít LINQ k dotazování a úpravě řádků. Dotazy LINQ také zjednodušují úlohu kombinování dat z více zdrojů.

- [Jak najít množinu rozdílů mezi dvěma seznamy (LINQ) (C#)](how-to-find-the-set-difference-between-two-lists-linq.md)

  Ukazuje, jak najít všechny řetězce, které jsou k dispozici v jednom seznamu, ale nikoli druhý.

- [Postup řazení nebo filtrování textových dat podle libovolného slova nebo pole (LINQ) (C#)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)

  Ukazuje, jak seřadit řádky textu založené na jakémkoli slově nebo poli.

- [Změna pořadí polí souboru s oddělovači (LINQ) (C#)](how-to-reorder-the-fields-of-a-delimited-file-linq.md)

  Ukazuje, jak změnit pořadí polí v řádku v souboru. csv.

- [Postup kombinování a porovnávání kolekcí řetězců (LINQ) (C#)](how-to-combine-and-compare-string-collections-linq.md)

  Ukazuje, jak kombinovat seznamy řetězců různými způsoby.

- [Jak naplnit kolekce objektů z více zdrojů (LINQ) (C#)](how-to-populate-object-collections-from-multiple-sources-linq.md)

  Ukazuje, jak vytvořit kolekce objektů pomocí více textových souborů jako zdrojů dat.

- [Postup připojení obsahu z nepodobných souborů (LINQ) (C#)](how-to-join-content-from-dissimilar-files-linq.md)
  
  Ukazuje, jak kombinovat řetězce ve dvou seznamech do jednoho řetězce pomocí odpovídajícího klíče.

- [Rozdělení souboru na více souborů pomocí skupin (LINQ) (C#)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)
  
  Ukazuje, jak vytvořit nové soubory pomocí jednoho souboru jako zdroje dat.

- [Jak vypočítat hodnoty sloupce v textovém souboru CSV (LINQ) (C#)](how-to-compute-column-values-in-a-csv-text-file-linq.md)
  
  Ukazuje, jak provádět matematické výpočty s textovými daty v souborech. csv.

## <a name="see-also"></a>Viz také

- [LINQ (Language-Integrated Query) (C#)](index.md)
- [Jak generovat XML ze souborů CSV](how-to-generate-xml-from-csv-files.md)

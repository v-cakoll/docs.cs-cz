---
title: Seskupení dat (C#)
description: Seskupení vloží data do skupin prvků, které sdílejí atribut. Přečtěte si o standardních metodách operátoru dotazu v LINQ v jazyce C#, které seskupují datové prvky.
ms.date: 07/20/2015
ms.assetid: e414e9e4-343a-4e6e-858f-4a30c5e64492
ms.openlocfilehash: 5e1bca1d360b0f44a081cf2770118a0551629b5b
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103684"
---
# <a name="grouping-data-c"></a>Seskupení dat (C#)
Seskupení odkazuje na operaci vložení dat do skupin, aby elementy v každé skupině sdílely společný atribut.  
  
 Následující ilustrace znázorňuje výsledky seskupení sekvencí znaků. Klíč pro každou skupinu je znak.  
  
 ![Diagram, který znázorňuje operaci seskupení LINQ.](./media/grouping-data/linq-group-operation.png)  
  
 Standardní metody operátoru dotazu, které seskupují datové prvky, jsou uvedeny v následující části.  
  
## <a name="methods"></a>Metody  
  
|Název metody|Popis|Syntaxe výrazu dotazu v jazyce C#|Další informace|  
|-----------------|-----------------|---------------------------------|----------------------|  
|GroupBy|Seskupí prvky, které sdílejí společný atribut. Jednotlivé skupiny jsou reprezentovány <xref:System.Linq.IGrouping%602> objektem.|`group … by`<br /><br /> -nebo-<br /><br /> `group … by … into …`|<xref:System.Linq.Enumerable.GroupBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupBy%2A?displayProperty=nameWithType>|  
|ToLookup|Vloží prvky do <xref:System.Linq.Lookup%602> slovníku (do slovníku 1: n) na základě funkce selektoru klíče.|Neužívá se.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>Příklad syntaxe výrazu dotazu  
 Následující příklad kódu používá `group by` klauzuli pro seskupení celých čísel v seznamu podle toho, zda jsou sudé nebo liché.  
  
```csharp  
List<int> numbers = new List<int>() { 35, 44, 200, 84, 3987, 4, 199, 329, 446, 208 };  
  
IEnumerable<IGrouping<int, int>> query = from number in numbers  
                                         group number by number % 2;  
  
foreach (var group in query)  
{  
    Console.WriteLine(group.Key == 0 ? "\nEven numbers:" : "\nOdd numbers:");  
    foreach (int i in group)  
        Console.WriteLine(i);  
}  
  
/* This code produces the following output:  
  
    Odd numbers:  
    35  
    3987  
    199  
    329  
  
    Even numbers:  
    44  
    200  
    84  
    4  
    446  
    208  
*/  
```  
  
## <a name="see-also"></a>Viz také

- <xref:System.Linq>
- [Přehled standardních operátorů dotazů (C#)](./standard-query-operators-overview.md)
- [group – klauzule](../../../language-reference/keywords/group-clause.md)
- [Vytvoření vnořené skupiny](../../../linq/create-a-nested-group.md)
- [Postup seskupení souborů podle přípony (LINQ) (C#)](./how-to-group-files-by-extension-linq.md)
- [Seskupení výsledků dotazu](../../../linq/group-query-results.md)
- [Provádění poddotazů na skupinách](../../../linq/perform-a-subquery-on-a-grouping-operation.md)
- [Rozdělení souboru na více souborů pomocí skupin (LINQ) (C#)](./how-to-split-a-file-into-many-files-by-using-groups-linq.md)

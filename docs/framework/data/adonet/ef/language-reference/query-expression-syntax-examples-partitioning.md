---
title: 'Příklady syntaxe výrazů dotazů: Dělení'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7e41aed0-3be9-4f75-98de-860a85552a3c
ms.openlocfilehash: b845564c02b55b8729efc893d7eecc48bd60f710
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398552"
---
# <a name="query-expression-syntax-examples-partitioning"></a>Příklady syntaxe výrazů dotazů: Dělení
Příklady v tomto tématu ukazují, jak použít <xref:System.Linq.Enumerable.Skip%2A> metody a <xref:System.Linq.Enumerable.Take%2A> k dotazování [modelu prodeje AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) pomocí syntaxe výrazu dotazu. Model prodeje společnosti AdventureWorks použitý v těchto příkladech je sestaven z tabulek Contact, adresa, produkt, SalesOrderHeader a SalesOrderDetail v ukázkové databázi AdventureWorks.  
  
 Příklady v tomto tématu používají následující `using` / `Imports` příkazy:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="skip"></a>Skip  
  
### <a name="example"></a>Příklad  
 Následující příklad používá <xref:System.Linq.Enumerable.Skip%2A> metodu k získání všech kromě prvních dvou adres v Praze.  
  
 [!code-csharp[DP L2E Examples#SkipNested](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#skipnested)]
 [!code-vb[DP L2E Examples#SkipNested](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#skipnested)]  
  
## <a name="take"></a>Take  
  
### <a name="example"></a>Příklad  
 Následující příklad používá <xref:System.Linq.Enumerable.Take%2A> metodu k získání prvních tří adres v Praze.  
  
 [!code-csharp[DP L2E Examples#TakeNested](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#takenested)]
 [!code-vb[DP L2E Examples#TakeNested](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#takenested)]  
  
## <a name="see-also"></a>Viz také:

- [Dotazy v technologii LINQ to Entities](queries-in-linq-to-entities.md)

---
title: Vytvoření fondu objektů pomocí ConcurrentBag
ms.date: 05/01/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object pool, in .NET Framework
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
ms.openlocfilehash: 64d91162b27eba80fba63761d0a926e441b63440
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287858"
---
# <a name="create-an-object-pool-by-using-a-concurrentbag"></a>Vytvoření fondu objektů pomocí ConcurrentBag

Tento příklad ukazuje, jak použít <xref:System.Collections.Concurrent.ConcurrentBag%601> k implementaci fondu objektů. Fondy objektů můžou zlepšit výkon aplikace v situacích, kdy požadujete více instancí třídy a že je třída nenáročná na vytvoření nebo zničení. Když klientský program požádá o nový objekt, fond objektů se nejprve pokusí zadat, který již byl vytvořen a vrácen do fondu. Pokud není k dispozici žádný, je vytvořen nový objekt.

<xref:System.Collections.Concurrent.ConcurrentBag%601>Slouží k uložení objektů, protože podporuje rychlé vkládání a odebírání, zejména v případě, že stejné vlákno přidává i odebírá položky. Tento příklad může být dále rozšířen tak, aby byl sestaven kolem <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> , který implementuje strukturu dat balíčku, jako do <xref:System.Collections.Concurrent.ConcurrentQueue%601> a <xref:System.Collections.Concurrent.ConcurrentStack%601> .

> [!TIP]
> Tento článek popisuje, jak napsat vlastní implementaci fondu objektů pomocí základního souběžného typu pro ukládání objektů pro opakované použití. Tento typ však <xref:Microsoft.Extensions.ObjectPool.ObjectPool%601?displayProperty=nameWithType> v oboru názvů již existuje <xref:Microsoft.Extensions.ObjectPool?displayProperty=fullName> . Zvažte použití dostupného typu před vytvořením vlastní implementace, která zahrnuje mnoho dalších funkcí.

## <a name="example"></a>Příklad

[!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
[!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]

## <a name="see-also"></a>Viz také

- [Kolekce bezpečné pro přístup z více vláken](index.md)

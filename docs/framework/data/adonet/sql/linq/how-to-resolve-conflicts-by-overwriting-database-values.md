---
title: 'Postupy: Řešení konfliktů přepsáním hodnot v databázi'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd6db0b8-c29c-48ff-b768-31d28e7a148c
ms.openlocfilehash: 1da2abcbbb3b87d44aa99016112d9ef2674912c6
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781715"
---
# <a name="how-to-resolve-conflicts-by-overwriting-database-values"></a>Postupy: Řešení konfliktů přepsáním hodnot v databázi
Chcete-li sjednotit rozdíly mezi očekávanými a skutečnými hodnotami databáze před tím, než se pokusíte znovu <xref:System.Data.Linq.RefreshMode.KeepCurrentValues> odeslat změny, můžete použít k přepsání hodnot databáze. Další informace najdete v tématu [Optimistická souběžnost: Přehled](optimistic-concurrency-overview.md).  
  
> [!NOTE]
> Ve všech případech se záznam v klientovi poprvé aktualizuje načtením aktualizovaných dat z databáze. Tato akce zajistí, že se další pokus o aktualizaci nebude při stejných kontrolách souběžnosti selhat.  
  
## <a name="example"></a>Příklad  
 V tomto scénáři <xref:System.Data.Linq.ChangeConflictException> je vyvolána výjimka, když se uživatel1 pokusí odeslat změny, protože uživatel2 má mezitím změněné sloupce asistent a oddělení. V následující tabulce je uvedena situace.  
  
||Správce|Pomocníka|Oddělení|  
|------|-------------|---------------|----------------|  
|Původní stav databáze při dotazování od uživatele User1 a uživatel2.|Alfreds|Maria|Prodej|  
|Uživatel1 připraví odeslání těchto změn.|Alfred||Marketing|  
|Uživatel2 již odeslal tyto změny.||Marie|Služba|  
  
 Uživatel1 se rozhodne tento konflikt vyřešit přepsáním hodnot databáze s aktuálními hodnotami členů klienta.  
  
 Když uživatel1 vyřeší konflikt <xref:System.Data.Linq.RefreshMode.KeepCurrentValues>pomocí, je výsledek v databázi jako v následující tabulce:  
  
||Správce|Pomocníka|Oddělení|  
|------|-------------|---------------|----------------|  
|Nový stav po vyřešení konfliktu.|Alfred<br /><br /> (od uživatele user1)|Maria<br /><br /> původně|Marketing<br /><br /> (od uživatele user1)|  
  
 Následující příklad kódu ukazuje, jak přepsat hodnoty databáze aktuálními hodnotami členů klienta. (K žádné kontrole nebo vlastní manipulaci s jednotlivými členy nedochází.)  
  
 [!code-csharp[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.RefreshMode#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#2)]  
  
## <a name="see-also"></a>Viz také:

- [Postupy: Správa konfliktů změn](how-to-manage-change-conflicts.md)

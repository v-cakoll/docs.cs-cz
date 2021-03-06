---
title: Souhrn procesu odvození schématu datové sady
ms.date: 03/30/2017
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
ms.openlocfilehash: 35e9b67d2d0a47aa69eabdb4b7e94f95b0b9589f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833984"
---
# <a name="summary-of-the-dataset-schema-inference-process"></a>Souhrn procesu odvození schématu datové sady
Nejprve proces odvození určuje z dokumentu XML, které prvky budou odvozeny jako tabulky. Ze zbývajícího souboru XML určí proces odvození sloupce pro tyto tabulky. U vnořených tabulek generuje odvozený proces vytváření vnořených objektů <xref:System.Data.DataRelation> a <xref:System.Data.ForeignKeyConstraint>.  
  
 Následuje stručný souhrn odvozených pravidel:  
  
- Prvky, které mají atributy, jsou odvozeny jako tabulky.  
  
- Prvky, které mají podřízené prvky, jsou odvozeny jako tabulky.  
  
- Prvky, které se opakují, jsou odvozeny jako jedna tabulka.  
  
- Pokud dokument nebo root, element nemá žádné atributy a žádné podřízené prvky, které by byly odvozeny jako sloupce, je odvozena jako <xref:System.Data.DataSet>. V opačném případě je element dokumentu odvozen jako tabulka.  
  
- Atributy jsou odvozeny jako sloupce.  
  
- Prvky, které nemají žádné atributy ani podřízené prvky a které se neopakují, jsou odvozeny jako sloupce.  
  
- Pro prvky, které jsou odvozeny jako vnořené tabulky v rámci jiných prvků, které jsou rovněž odvozeny jako tabulky, je mezi dvěma tabulkami vytvořen vnořený objekt **DataRelation** . Do obou tabulek se přidá nový sloupec primárního klíče s názvem **TableName_Id** , který se používá v **datarelationu**. **Objekt ForeignKeyConstraint** se vytvoří mezi dvěma tabulkami pomocí sloupce **TableName_Id** .  
  
- Pro prvky, které jsou odvozeny jako tabulky a které obsahují text, ale nemají žádné podřízené prvky, je vytvořen nový sloupec s názvem **TableName_Text** pro text každého prvku. Pokud je element odvozen jako tabulka a má text, ale také má podřízené prvky, text se ignoruje.  
  
## <a name="see-also"></a>Viz také:

- [Odvození relační struktury datové sady z XML](inferring-dataset-relational-structure-from-xml.md)
- [Načtení datové sady z XML](loading-a-dataset-from-xml.md)
- [Načtení informací o schématu datové sady z XML](loading-dataset-schema-information-from-xml.md)
- [Použití XML v datové sadě](using-xml-in-a-dataset.md)
- [Datové sady, datové tabulky a datová zobrazení](index.md)
- [Přehled ADO.NET](../ado-net-overview.md)

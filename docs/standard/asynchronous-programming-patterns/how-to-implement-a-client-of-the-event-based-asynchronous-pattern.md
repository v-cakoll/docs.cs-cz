---
title: 'Postupy: Implementace klienta asynchronního vzoru založeného na událostech'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
ms.openlocfilehash: f834ce4a0ec2208eee80ce8c3ffebfa6fdeeb5b1
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289405"
---
# <a name="how-to-implement-a-client-of-the-event-based-asynchronous-pattern"></a>Postupy: Implementace klienta asynchronního vzoru založeného na událostech
Následující příklad kódu ukazuje, jak použít komponentu, která je v [přehledu asynchronního vzoru založeného na událostech](event-based-asynchronous-pattern-overview.md). Formulář pro tento příklad používá `PrimeNumberCalculator` komponentu popsanou v tématu [Postupy: Implementace komponenty, která podporuje asynchronní vzor založený na událostech](component-that-supports-the-event-based-asynchronous-pattern.md).  
  
 Když spustíte projekt, který používá tento příklad, zobrazí se ve formě kalkulačky "základní číslo" s mřížkou a dvěma tlačítky: **spustit novou úlohu** a **Zrušit**. Můžete kliknout na tlačítko **spustit novou úlohu** několikrát po úspěchu a při každém kliknutí na tuto asynchronní operaci zahájit výpočet, který určí, jestli je náhodně generované číslo testu primární. Ve formuláři se budou pravidelně zobrazovat průběh a přírůstkové výsledky. Každé operaci je přiřazeno jedinečné ID úlohy. Výsledek výpočtu se zobrazí ve sloupci **výsledek** . Pokud číslo testu není primární, je označeno jako **složené** a zobrazí se jeho první dělitel.  
  
 Můžete zrušit všechny probíhající operace tlačítkem **Storno** . Je možné provést vícenásobné výběry.  
  
> [!NOTE]
> Většina čísel nebude primární. Pokud jste nenašli základní číslo po několika dokončených operacích, stačí spustit více úkolů a nakonec najít některá hlavní čísla.  
  
## <a name="example"></a>Příklad  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#10)]  
  
## <a name="see-also"></a>Viz také

- <xref:System.ComponentModel.AsyncOperation>
- <xref:System.ComponentModel.AsyncOperationManager>
- <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>

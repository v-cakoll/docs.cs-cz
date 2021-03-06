---
title: 'Postupy: Implementace oznámení změn vlastností'
description: Povolit vlastnosti pro automatické upozorňování zdroje vazby při změně hodnoty vlastnosti v Windows Presentation Foundation (WPF).
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- notifications of change [WPF]
- data binding [WPF], property change notifications
- change notifications [WPF]
- properties [WPF], change notifications
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
ms.openlocfilehash: 6c298930b7b1f812e94ea6add8f53c67d3453530
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620778"
---
# <a name="how-to-implement-property-change-notification"></a>Postupy: Implementace oznámení změn vlastností
Aby bylo možné podporovat <xref:System.Windows.Data.BindingMode.OneWay> nebo <xref:System.Windows.Data.BindingMode.TwoWay> svázat vlastnosti cílové vazby, aby automaticky odrážely dynamické změny zdroje vazby (například pokud chcete, aby se podokno náhledu automaticky aktualizovalo při úpravách formuláře), vaše třída musí poskytovat správnou vlastnost změněných oznámení. Tento příklad ukazuje, jak vytvořit třídu, která implementuje <xref:System.ComponentModel.INotifyPropertyChanged> .  
  
## <a name="example"></a>Příklad  
 K implementaci musíte <xref:System.ComponentModel.INotifyPropertyChanged> deklarovat <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> událost a vytvořit `OnPropertyChanged` metodu. Potom můžete pro každou vlastnost, pro kterou chcete změnit oznámení, zavolat `OnPropertyChanged` vždy, když je vlastnost aktualizována.  
  
 [!code-csharp[SimpleBinding#PersonClass](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 Příklad toho `Person` , jak lze třídu použít pro podporu <xref:System.Windows.Data.BindingMode.TwoWay> vazby, naleznete v tématu [Control when text TextBox Update source](how-to-control-when-the-textbox-text-updates-the-source.md).  
  
## <a name="see-also"></a>Viz také:

- [Přehled zdrojů vazby](binding-sources-overview.md)
- [Přehled datových vazeb](../../../desktop-wpf/data/data-binding-overview.md)
- [– postupy](data-binding-how-to-topics.md)

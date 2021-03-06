---
title: 'Postupy: Skrytí ToolStripMenuItems'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- ToolStripMenuItems [Windows Forms], hiding
- MenuStrip control [Windows Forms], hiding menu items
- menus [Windows Forms], hiding menu items
- menu items [Windows Forms], hiding
- hiding menu items
ms.assetid: 418a768f-808a-44cd-8cef-f4e161883621
ms.openlocfilehash: 64c0f093063357c1e8db5933c035cc8295ad4f1e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623044"
---
# <a name="how-to-hide-toolstripmenuitems"></a>Postupy: Skrytí ToolStripMenuItems
Skrytí položek nabídky je způsob, jak ovládací prvek uživatelského rozhraní aplikace a omezit uživatelských příkazů. Často můžete skrýt celou nabídku, když jsou všechny položky nabídky na něm není k dispozici. To představuje méně rozptýlení pro daného uživatele. Kromě toho můžete chtít skrýt i zakázat nabídky nebo položku nabídky, protože skrytí samostatně nebrání uživateli přístup k příkazu nabídky pomocí klávesové zkratky.  
  
### <a name="to-hide-any-menu-item-programmatically"></a>Chcete-li skrýt všechny položky nabídky prostřednictvím kódu programu  
  
- V rámci metody, kde nastavíte vlastnosti položky nabídky, přidejte kód pro nastavení <xref:System.Windows.Forms.ToolStripItem.Visible%2A> vlastnost `false`.  
  
    ```vb  
    MenuItem3.Visible = False  
    ```  
  
    ```csharp  
    menuItem3.Visible = false;  
    ```  
  
    ```cpp  
    menuItem3->Visible = false;  
    ```  
  
## <a name="see-also"></a>Viz také:

- <xref:System.Windows.Forms.ToolStripItem.Visible%2A>
- <xref:System.Windows.Forms.MenuStrip>
- [Přehled ovládacího prvku MenuStrip](menustrip-control-overview-windows-forms.md)
- [Postupy: Zákaz ToolStripMenuItems](how-to-disable-toolstripmenuitems.md)

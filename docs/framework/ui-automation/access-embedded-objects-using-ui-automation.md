---
title: Přístup k vloženým objektům s použitím automatizace uživatelského rozhraní
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- embedded objects, accessing
- accessing embedded objects
- UI Automation, accessing embedded objects
ms.assetid: a5b513ec-7fa6-4460-869f-c18ff04f7cf2
ms.openlocfilehash: 75c63360eab2cde95698bdaded5c5249a3ca89fd
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/23/2019
ms.locfileid: "74447265"
---
# <a name="access-embedded-objects-using-ui-automation"></a>Přístup k vloženým objektům s použitím automatizace uživatelského rozhraní
> [!NOTE]
> Tato dokumentace je určena pro .NET Framework vývojářů, kteří chtějí používat spravované [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] třídy definované v oboru názvů <xref:System.Windows.Automation>. Nejnovější informace o [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]najdete v tématu [rozhraní API pro Windows Automation: automatizace uživatelského rozhraní](/windows/win32/winauto/entry-uiauto-win32).  
  
 V tomto tématu se dozvíte, jak lze [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] použít k vystavení objektů vložených do obsahu ovládacího prvku text.  
  
> [!NOTE]
> Vložené objekty mohou obsahovat obrázky, hypertextové odkazy, tlačítka, tabulky nebo ovládací prvky ActiveX.  
  
 Vložené objekty jsou považovány za podřízené objekty poskytovatele [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ho textu. To umožňuje, aby byly zpřístupněny prostřednictvím stejné struktury stromu automatizace uživatelského rozhraní jako všechny ostatní prvky [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]. Funkce jsou zase zpřístupněny prostřednictvím vzorů ovládacích prvků, které jsou obvykle vyžadovány typem ovládacího prvku vložené objekty (například vzhledem k tomu, že hypertextové odkazy jsou založené na textu, budou podporovat <xref:System.Windows.Automation.TextPattern>).  
  
 ![Vložené objekty v textovém kontejneru.](./media/uia-textpattern-embeddedobjects.PNG "UIA_TextPattern_EmbeddedObjects")  
Ukázkový dokument s textovým obsahem ("Víte, že víte?" ...) a dva vložené objekty (obrázek Whale a textový hypertextový odkaz) používané jako cíl pro příklady kódu.  
  
## <a name="example"></a>Příklad  
 Následující příklad kódu ukazuje, jak načíst kolekci vložených objektů z poskytovatele [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ho textu. Pro ukázkový dokument poskytnutý v úvodu by se vracely dva objekty (element obrázku a textový element).  
  
> [!NOTE]
> K elementu Image by měl být přidružen nějaký vnitřní text, který popisuje obrázek, obvykle v jeho <xref:System.Windows.Automation.AutomationElement.NameProperty> (například "modrý Whale"). Pokud se ale Získá rozsah textu, který pokrývá objekt obrázku, nevrátí se do textového streamu ani obrázek ani tento popisný text.  
  
[!code-csharp[FindText#StartApp](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#startapp)]
[!code-vb[FindText#StartApp](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#startapp)]  
[!code-csharp[FindText#FindTextProvider](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#findtextprovider)]
[!code-vb[FindText#FindTextProvider](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#findtextprovider)]  
[!code-csharp[FindText#GetChildren](../../../samples/snippets/csharp/VS_Snippets_Wpf/FindText/CSharp/SearchWindow.cs#getchildren)]
[!code-vb[FindText#GetChildren](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindText/VisualBasic/SearchWindow.vb#getchildren)]  
  
## <a name="example"></a>Příklad  
 Následující příklad kódu ukazuje, jak získat textovou oblast z vloženého objektu v rámci poskytovatele [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ho textu. Načtený rozsah textu je prázdný rozsah, ve kterém následuje počáteční koncový bod... spadající. (Space) "a koncový bod předchází konci". "představující vložený hypertextový odkaz (jak znázorňuje obrázek uvedený v úvodu). I když se jedná o prázdný rozsah, není považován za negenerovaný rozsah, protože má nenulové rozpětí.  
  
> [!NOTE]
> <xref:System.Windows.Automation.TextPattern> může načíst textový vložený objekt, jako je hypertextový odkaz; sekundární <xref:System.Windows.Automation.TextPattern> však bude nutné získat z vloženého objektu, aby bylo možné zobrazit jeho plnou funkčnost.  
  
 [!code-csharp[UIATextPattern_snip#GetRangeFromChild](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIATextPattern_snip/CSharp/SearchWindow.cs#getrangefromchild)]
 [!code-vb[UIATextPattern_snip#GetRangeFromChild](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIATextPattern_snip/VisualBasic/SearchWindow.vb#getrangefromchild)]  
  
## <a name="see-also"></a>Viz také:

- [Přehled prvku TextPattern automatizace uživatelského rozhraní](ui-automation-textpattern-overview.md)
- [Přehled vzorů ovládacích prvků pro automatizaci uživatelského rozhraní](ui-automation-control-patterns-overview.md)
- [Vzory ovládacích prvků automatizace uživatelského rozhraní pro klienty](ui-automation-control-patterns-for-clients.md)
- [Přidání obsahu textového pole s použitím automatizace uživatelského rozhraní](add-content-to-a-text-box-using-ui-automation.md)
- [Hledání a zvýrazňování textu s použitím automatizace uživatelského rozhraní](find-and-highlight-text-using-ui-automation.md)

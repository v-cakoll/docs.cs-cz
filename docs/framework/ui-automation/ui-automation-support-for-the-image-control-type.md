---
title: Podpora automatizace uživatelského rozhraní pro typ ovládacího prvku obrázek
description: Získejte informace o podpoře automatizace uživatelského rozhraní pro typ ovládacího prvku obrázek. Seznamte se s požadovanou stromovou strukturou, vlastnostmi, vzory ovládacích prvků a událostmi.
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Image control type
- control types, Image
- Image control type
ms.assetid: 4e0eeefb-e09b-46d2-b83b-0a7e35543ab8
ms.openlocfilehash: 97a71b31609566ca081dee1c66b911f0ad534a50
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166956"
---
# <a name="ui-automation-support-for-the-image-control-type"></a>Podpora automatizace uživatelského rozhraní pro typ ovládacího prvku obrázek
> [!NOTE]
> Tato dokumentace je určena pro .NET Framework vývojářů, kteří chtějí používat spravované [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] třídy definované v <xref:System.Windows.Automation> oboru názvů. Nejnovější informace o najdete [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] v tématu [rozhraní API služby Windows Automation: automatizace uživatelského rozhraní](/windows/win32/winauto/entry-uiauto-win32).  
  
 Toto téma poskytuje informace o [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] podpoře pro typ ovládacího prvku obrázek. V nástroji [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] je typ ovládacího prvku sada podmínek, které musí ovládací prvek splňovat, aby bylo možné vlastnost použít <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> . Podmínky zahrnují konkrétní pokyny pro [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromovou strukturu, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] hodnoty vlastností a vzory ovládacích prvků.  
  
 Ovládací prvky obrázku používané jako ikony, informační grafika a grafy budou podporovat typ ovládacího prvku obrázek. Ovládací prvky používané jako obrázky na pozadí nebo vodotisk nebudou podporovat typ ovládacího prvku obrázek.  
  
 Následující části definují požadovanou [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromovou strukturu, vlastnosti, vzory ovládacích prvků a události pro typ ovládacího prvku obrázek. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Požadavky platí pro všechny ovládací prvky obrázku, bez ohledu na to [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] , Win32 nebo model Windows Forms.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>
## <a name="required-ui-automation-tree-structure"></a>Požadovaná stromová struktura automatizace uživatelského rozhraní  
 Následující tabulka znázorňuje zobrazení ovládacího prvku a zobrazení obsahu [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromové struktury, které se vztahují k ovládacím prvkům obrázku, a popisuje, co může být v každém zobrazení obsaženo. Další informace o [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromové struktuře najdete v tématu [Přehled stromu automatizace uživatelského rozhraní](ui-automation-tree-overview.md).  
  
|Zobrazení ovládacích prvků|Zobrazení obsahu|  
|------------------|------------------|  
|Image|Obrázek (záleží na tom, jestli obrázek obsahuje informace (na základě hodnoty `IsContentElement` Vlastnosti))|  
  
<a name="Required_UI_Automation_Properties"></a>
## <a name="required-ui-automation-properties"></a>Požadované vlastnosti automatizace uživatelského rozhraní  
 V následující tabulce jsou uvedeny [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] vlastnosti, jejichž hodnota nebo definice je obzvláště relevantní pro typ ovládacího prvku obrázek. Další informace o [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] vlastnostech najdete v tématu [Vlastnosti automatizace uživatelského rozhraní pro klienty](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Majetek|Hodnota|Poznámky|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Viz poznámky.|Hodnota této vlastnosti musí být jedinečná napříč všemi ovládacími prvky v aplikaci.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Viz poznámky.|Vnější obdélník, který obsahuje celý ovládací prvek.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Viz poznámky.|Řídicí bod ovládacího prvku obrázku musí být bod v ohraničujícím obdélníku ovládacího prvku obrázek.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Viz poznámky.|Pokud ovládací prvek může obdržet fokus klávesnice, musí podporovat tuto vlastnost.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Viz poznámky.|Vlastnost Name musí být vystavena pro všechny ovládací prvky obrázku, které obsahují informace. Programový přístup k těmto informacím vyžaduje, aby byl k dispozici textový ekvivalent na grafiku. Je-li ovládací prvek obrázek čistě ozdobný, je nutné jej zobrazit pouze v zobrazení ovládacího prvku [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromu a není nutné mít název. Architektury uživatelského rozhraní musí pro obrázky, které lze nastavit v rámci svého rozhraní, podporovat alternativní vlastnost textu nebo alternativní text. Tato vlastnost se pak namapuje na [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] vlastnost Name.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Viz poznámky.|Pokud je popisek statický text, musí tato vlastnost vystavit odkaz na tento ovládací prvek.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Image|Tato hodnota je stejná pro všechny architektury uživatelského rozhraní.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|obrazu|Lokalizovaný řetězec odpovídající typu ovládacího prvku obrázek.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|Viz poznámky.|Ovládací prvek obrázek musí být součástí zobrazení obsahu [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromové struktury, pokud obsahuje smysluplné informace, které již nejsou vystaveny koncovému uživateli.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|Ano|Ovládací prvek obrázek je vždy součástí zobrazení ovládacího prvku [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] stromové struktury.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Viz poznámky.|Vlastnost HelpText zveřejňuje lokalizovaný řetězec, který popisuje skutečný vzhled ovládacího prvku (například červeného čtverce s bílým znakem ' X ') nebo jiné informace popisku přidružené k imagi.<br /><br /> Tato vlastnost musí být podporována, je-li nutné zadat dlouhý popis pro předávání dalších informací o ovládacím prvku obrázek. Například složitý graf nebo diagram. Tato vlastnost je mapována na značku HTML LongDesc a značku DESC Scalable Vector Graphics (SVG). Vývojáři, kteří pracují s ovládacími prvky obrázku, musí podporovat vlastnost, která umožňuje nastavení vizuálního popisu na ovládacím prvku. Tato vlastnost musí být namapovaná na vlastnost VisualDescription pro automatizaci uživatelského rozhraní.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ItemStatusProperty>|Viz poznámky.|Pokud ovládací prvek obrázek představuje informace o stavu konkrétní položky na obrazovce, ovládací prvek by měl být obsažen v rámci položky. Když je obrázek obsažen v položce, musí položka podporovat vlastnost status a vyvolat vhodná oznámení při změně stavu.<br /><br /> Je-li obrázek samostatným ovládacím prvkem a probíhá jeho stav, musí být tato vlastnost podporována.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>
## <a name="required-ui-automation-control-patterns"></a>Požadované vzory ovládacího prvku automatizace uživatelského rozhraní  
 V následující tabulce jsou uvedeny [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] vzory ovládacích prvků, které musí být podporovány všemi ovládacími prvky obrázku. Další informace o vzorech ovládacích prvků naleznete v tématu [Přehled vzorů ovládacích prvků automatizace uživatelského rozhraní](ui-automation-control-patterns-overview.md).  
  
|Vzor ovládacího prvku|Podpora|Poznámky|  
|---------------------|-------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider>|Závislosti|Ovládací prvek obrázek podporuje model položky mřížky, pokud je ovládací prvek v rámci kontejneru mřížky.|  
|<xref:System.Windows.Automation.Provider.ITableItemProvider>|Závislosti|Ovládací prvek obrázek podporuje model položky tabulky, je-li ovládací prvek v rámci kontejneru, který obsahuje ovládací prvky záhlaví.|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|Nikdy|Pokud ovládací prvek obrázek obsahuje obrázek, který je k zobrazení, ovládací prvek by měl podporovat typ ovládacího prvku, který podporuje vzor volání, jako je například typ ovládacího prvku tlačítko.|  
|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|Nikdy|Ovládací prvky obrázku by neměly podporovat vzorek položky výběru.|  
  
<a name="Required_UI_Automation_Events"></a>
## <a name="required-ui-automation-events"></a>Požadované události automatizace uživatelského rozhraní  
 V následující tabulce jsou uvedeny [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] události, které musí být podporovány všemi ovládacími prvky obrázku. Další informace o událostech najdete v tématu [Přehled událostí automatizace uživatelského rozhraní](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]Událostí|Podpora|Poznámky|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|Nikdy|Žádné|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementAddedToSelectionEvent>|Nikdy|Žádné|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementRemovedFromSelectionEvent>|Nikdy|Žádné|  
|<xref:System.Windows.Automation.SelectionItemPatternIdentifiers.ElementSelectedEvent>|Nikdy|Žádné|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>událost změny vlastnosti.|Povinné|Žádné|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>událost změny vlastnosti.|Povinné|Žádné|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>událost změny vlastnosti.|Povinné|Žádné|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>událost změny vlastnosti.|Povinné|Žádné|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Povinné|Žádné|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Povinné|Žádné|  
  
## <a name="see-also"></a>Viz také

- <xref:System.Windows.Automation.ControlType.Image>
- [Přehled typů ovládacích prvků pro automatizaci uživatelského rozhraní](ui-automation-control-types-overview.md)
- [Přehled automatizace uživatelského rozhraní](ui-automation-overview.md)

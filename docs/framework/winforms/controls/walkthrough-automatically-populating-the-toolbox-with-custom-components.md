---
title: 'Návod: Automatické vyplnění sady nástrojů vlastními komponentami'
ms.date: 03/30/2017
helpviewer_keywords:
- IToolboxService interface
- Toolbox [Windows Forms], populating
- custom components [Windows Forms], adding to Toolbox
ms.assetid: 2fa1e3e8-6b9f-42b2-97c0-2be57444dba4
ms.openlocfilehash: 876de650f9c182c0f82a02d1c5b356faa4f7f118
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211158"
---
# <a name="walkthrough-automatically-populating-the-toolbox-with-custom-components"></a>Návod: Automatické vyplnění sady nástrojů vlastními komponentami

Pokud vaše komponenty jsou definovány projektu v aktuálně otevřené řešení, se automaticky zobrazí v **nástrojů**, třeba akce. Můžete také ručně naplnit **nástrojů** pomocí vlastních součástí s použitím [tlačítko panelu nástrojů položky dialogové okno (Visual Studio)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/dyca0t6t(v=vs.100)), ale **nástrojů** bere v úvahu položky ve vašem řešení sestavení výstupy s následujícími charakteristikami:

- Implementuje <xref:System.ComponentModel.IComponent>;

- Nemá <xref:System.ComponentModel.ToolboxItemAttribute> nastavena na `false`;

- Nemá <xref:System.ComponentModel.DesignTimeVisibleAttribute> nastavena na `false`.

> [!NOTE]
> **Nástrojů** nedodržuje odkaz na řetězcích, proto by se nezobrazil položky, které nejsou sestaveny projekt ve vašem řešení.

Tento návod ukazuje, jak vlastní komponenty se automaticky zobrazí v **nástrojů** po sestavení komponenty. Úlohy v tomto návodu zahrnují:

- Vytvoření projektu Windows Forms.

- Vytvoření vlastní komponenty.

- Vytvoření instance vlastní komponenty.

- Uvolnění a opětovné načtení volitelná množina komponent.

Až budete hotovi, uvidíte, že **nástrojů** se vyplní komponentu, kterou jste vytvořili.

## <a name="create-the-project"></a>Vytvoření projektu

1. V sadě Visual Studio vytvořte projekt aplikace pro systém Windows s názvem `ToolboxExample` (**souboru** > **nový** > **projektu**  >  **Visual C#**  nebo **jazyka Visual Basic** > **klasický desktopový** > **Windows Forms Aplikace**).

2. Přidáte novou součást do projektu. Pojmenujte ji `DemoComponent`.

     Další informace najdete v tématu [jak: Přidání nových položek projektu](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w0572c5b(v=vs.100)).

3. Sestavte projekt.

4. Z **nástroje** nabídky, klikněte na tlačítko **možnosti** položky. Klikněte na tlačítko **Obecné** pod **Návrháře formulářů Windows** položku a ověřte, že **AutoToolboxPopulate** je možnost nastavená na **True**.

## <a name="create-an-instance-of-a-custom-component"></a>Vytvoření instance vlastní komponenty

Dalším krokem je vytvoření instance vlastní komponenty ve formuláři. Vzhledem k tomu, **nástrojů** automaticky účty pro novou komponentu, to je stejně jednoduché jako vytvoření jakékoli součást nebo ovládací prvek.

1. Otevřete formulář v projektu v **Návrháře formulářů**.

2. V **nástrojů**, klikněte na novou kartu **ToolboxExample komponenty**.

     Po kliknutí na kartě, zobrazí se **DemoComponent**.

    > [!NOTE]
    > Z důvodů výkonu komponenty v oblasti vyplní automaticky **nástrojů** vlastních rastrových obrázků, se nezobrazí a <xref:System.Drawing.ToolboxBitmapAttribute> se nepodporuje. Zobrazit ikonu pro vlastní komponenty v **nástrojů**, použijte **zvolit položky nástrojů** dialogové okno načíst vaše komponenta.

3. Přetáhněte komponenty do formuláře.

     Je vytvořen a přidán do instance komponenty **komponent**.

## <a name="unload-and-reload-a-custom-component"></a>Odebrat a znovu načíst vlastní komponenty

**Nástrojů** přihlíží komponent v každém načtení projektu a projekt je uvolněna, odebere odkazy na součásti projektu.

1. Uvolněte projekt z řešení.

     Další informace o uvolnění projektů, naleznete v tématu [jak: Odebrat a znovu načíst projekty](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/tt479x1t(v=vs.100)). Pokud se zobrazí výzva k uložení, zvolte **Ano**.

2. Přidat nový **aplikace Windows** projektu do řešení. Otevřete formulář v nástrojích pro **návrháře**.

     **ToolboxExample součásti** kartu z předchozí projektu je teď pryč.

3. Znovu načíst `ToolboxExample` projektu.

     **ToolboxExample součásti** kartě nyní zobrazí znovu.

## <a name="next-steps"></a>Další kroky

Tento návod ukazuje, že **nástrojů** bere v úvahu součástí projektu, ale **nástrojů** je také přihlíží ovládacích prvků. Přidáváním a odebíráním ovládací prvek projekty z řešení můžete experimentovat s vlastní ovládací prvky.

## <a name="see-also"></a>Viz také:

- [Obecné, Návrhář formulářů Windows, dialogové okno Možnosti](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/5aazxs78(v=vs.100))
- [Postupy: Manipulace s karty panelu nástrojů](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/66kwe227(v=vs.100))
- [Zvolte dialogové okno položky panelu nástrojů (Visual Studio)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/dyca0t6t(v=vs.100))
- [Vkládání ovládacích prvků do Windows Forms](putting-controls-on-windows-forms.md)

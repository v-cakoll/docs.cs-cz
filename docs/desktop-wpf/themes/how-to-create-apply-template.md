---
title: Vytvoření šablony v prostředí WPF – .NET Desktop
description: Naučte se vytvořit a odkazovat na šablonu ovládacího prvku v Windows Presentation Foundation a .NET Core.
author: adegeo
ms.author: adegeo
ms.date: 11/15/2019
no-loc:
- <Window>
- <ControlTemplate>
- <Ellipse>
- <ContentPresenter>
- <Trigger>
- <Setter>
- <PropertyTrigger>
- <Grid>
- <VisualStateManager.VisualStateGroups>
- <VisualStateGroup>
- <VisualState>
- <Storyboard>
- SizeToContent
- MinWidth
- TargetType
- Title
helpviewer_keywords:
- control contract [WPF]
- controls [WPF], visual structure changes
- ControlTemplate [WPF], customizing for existing controls
- skinning controls [WPF]
- controls [WPF], appearance specified by state
- templates [WPF], custom for existing controls
ms.openlocfilehash: c372659676b450cde789c96e45c7ec5de2aea194
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325726"
---
# <a name="create-a-template-for-a-control"></a>Vytvoření šablony pro ovládací prvek

Pomocí Windows Presentation Foundation (WPF) můžete přizpůsobit vizuální strukturu a chování existující ovládacímu prvku pomocí vlastní opakovaně použitelné šablony. Šablony lze globálně použít pro vaši aplikaci, okna a stránky nebo přímo k ovládacím prvkům. Pro většinu scénářů, které vyžadují vytvoření nového ovládacího prvku, se místo toho dá vytvořit nová šablona pro existující ovládací prvek.

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

V tomto článku budete zkoumat vytvoření nového <xref:System.Windows.Controls.ControlTemplate> <xref:System.Windows.Controls.Button> ovládacího prvku.

## <a name="when-to-create-a-controltemplate"></a>Kdy vytvořit ControlTemplate

Ovládací prvky mají mnoho vlastností, jako jsou <xref:System.Windows.Controls.Border.Background%2A> , <xref:System.Windows.Controls.Control.Foreground%2A> a <xref:System.Windows.Controls.Control.FontFamily%2A> . Tyto vlastnosti řídí různé aspekty vzhledu ovládacího prvku, ale změny, které můžete provést nastavením těchto vlastností, jsou omezené. Můžete například nastavit <xref:System.Windows.Controls.Control.Foreground%2A> vlastnost na modrou a <xref:System.Windows.Controls.Control.FontStyle%2A> na kurzívu na <xref:System.Windows.Controls.CheckBox> . Pokud chcete přizpůsobit vzhled ovládacího prvku nad rámec toho, co nastavení dalších vlastností ovládacího prvku může udělat, vytvoříte <xref:System.Windows.Controls.ControlTemplate> .

Ve většině uživatelských rozhraní má tlačítko stejný obecný vzhled: obdélník s nějakým textem. Pokud jste chtěli vytvořit zaoblené tlačítko, mohli byste vytvořit nový ovládací prvek, který dědí z tlačítka, nebo znovu vytvořit funkci tlačítka. Kromě toho nový uživatelský ovládací prvek poskytne kruhový vizuál.

Vytváření nových ovládacích prvků můžete vyhnout přizpůsobením vizuálního rozložení existujícího ovládacího prvku. Pomocí zaobleného tlačítka vytvoříte <xref:System.Windows.Controls.ControlTemplate> s požadovaným rozložením vizuálu.

Na druhé straně, pokud potřebujete ovládací prvek s novými funkcemi, různými vlastnostmi a novými nastaveními, měli byste vytvořit nový <xref:System.Windows.Controls.UserControl> .

## <a name="prerequisites"></a>Požadované součásti

Vytvořte novou aplikaci WPF a v *MainWindow. XAML* (nebo jiném okně podle vašeho výběru) nastavte následující vlastnosti **\<Window>** elementu:

|     |     |
| --- | --- |
| **Title**         | `Template Intro Sample` |
| **SizeToContent** | `WidthAndHeight` |
| **MinWidth**      | `250` |

Nastavte obsah **\<Window>** elementu na následující XAML:

[!code-xaml[Initial](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window1.xaml#Initial)]

V elementu end by soubor *MainWindow. XAML* měl vypadat nějak takto:

[!code-xaml[InitialWhole](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window1.xaml#InitialWhole)]

Pokud aplikaci spouštíte, vypadá to jako na následujícím:

![Okno WPF se dvěma nestyle tlačítky](media/create-apply-template/unstyled-button.png)

## <a name="create-a-controltemplate"></a>Vytvoření ControlTemplate

Nejběžnější způsob, jak deklarovat, <xref:System.Windows.Controls.ControlTemplate> je jako prostředek v `Resources` oddílu v souboru XAML. Vzhledem k tomu, že šablony jsou prostředky, řídí se stejnými pravidly oboru, která se vztahují na všechny prostředky. Jednoduše řečeno, kde deklarujete šablonu, má vliv na to, kde lze šablonu použít. Například pokud deklarujete šablonu v kořenovém elementu souboru XAML definice aplikace, šablonu lze použít kdekoli v aplikaci. Definujete-li šablonu v okně, mohou šablonu používat pouze ovládací prvky v tomto okně.

Chcete-li začít s, přidejte `Window.Resources` element do souboru *MainWindow. XAML* :

[!code-xaml[WindowResStart](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window2.xaml#WindowResStart)]

Vytvořte nový **\<ControlTemplate>** s následujícími vlastnostmi:

|     |     |
| --- | --- |
| **X:Key –**         | `roundbutton` |
| **TargetType**    | `Button` |

Tato šablona ovládacího prvku bude jednoduchá:

- kořenový element ovládacího prvku,<xref:System.Windows.Controls.Grid>
- <xref:System.Windows.Shapes.Ellipse>vykreslení zaobleného vzhledu tlačítka
- <xref:System.Windows.Controls.ContentPresenter>pro zobrazení obsahu tlačítka zadaného uživatelem

[!code-xaml[ControlTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window3.xaml#ControlTemplate)]

### <a name="templatebinding"></a>TemplateBinding

Když vytvoříte nový <xref:System.Windows.Controls.ControlTemplate> , můžete přesto chtít použít veřejné vlastnosti ke změně vzhledu ovládacího prvku. Rozšíření značek [TemplateBinding](../../framework/wpf/advanced/templatebinding-markup-extension.md) váže vlastnost prvku, který je v <xref:System.Windows.Controls.ControlTemplate> vlastnosti Public, která je definována ovládacím prvkem. Když použijete [TemplateBinding](../../framework/wpf/advanced/templatebinding-markup-extension.md), povolíte vlastnosti ovládacího prvku tak, aby sloužily jako parametry šablony. To znamená, že když je nastavena vlastnost ovládacího prvku, je tato hodnota předána prvku, který má [TemplateBinding](../../framework/wpf/advanced/templatebinding-markup-extension.md) .

### <a name="ellipse"></a>Elipsa

Všimněte si, **:::no-loc text="Fill":::** že **:::no-loc text="Stroke":::** vlastnosti a **\<Ellipse>** prvku jsou vázány k ovládacím prvkům <xref:System.Windows.Controls.Control.Foreground> a <xref:System.Windows.Controls.Control.Background> vlastnostem.

### <a name="contentpresenter"></a>ContentPresenter

[\<ContentPresenter>](xref:System.Windows.Controls.ContentPresenter)Do šablony se přidá také element. Vzhledem k tomu, že je tato šablona navržena pro tlačítko, vezměte v úvahu, že tlačítko dědí z <xref:System.Windows.Controls.ContentControl> . Tlačítko zobrazí obsah elementu. Můžete nastavit cokoli uvnitř tlačítka, jako je prostý text nebo i jiný ovládací prvek. Níže jsou uvedené platná tlačítka:

```xaml
<Button>My Text</Button>

<!-- and -->

<Button>
    <CheckBox>Checkbox in a button</CheckBox>
</Button>
```

V obou předchozích příkladech se text a zaškrtávací políčko nastaví jako vlastnost [Button. Content](xref:System.Windows.Controls.ContentControl.Content) . Bez ohledu na to, jak je možné obsah prezentovat prostřednictvím **\<ContentPresenter>** , což je to, co dělá šablona.

Pokud <xref:System.Windows.Controls.ControlTemplate> je použit na <xref:System.Windows.Controls.ContentControl> typ, například `Button` ,, <xref:System.Windows.Controls.ContentPresenter> je prohledán ve stromu elementu. Pokud `ContentPresenter` je nalezen, šablona automaticky váže vlastnost ovládacího prvku <xref:System.Windows.Controls.ContentControl.Content> na `ContentPresenter` .

## <a name="use-the-template"></a>Použití šablony

Najděte tlačítka, která byla deklarována na začátku tohoto článku.

[!code-xaml[Initial](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window1.xaml#Initial)]

Nastavte vlastnost druhého tlačítka <xref:System.Windows.Controls.Control.Template> na `roundbutton` prostředek:

[!code-xaml[StyledButton](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window3.xaml#StyledButton)]

Pokud projekt spustíte a podíváte se na výsledek, uvidíte, že tlačítko má zaoblené pozadí.

![Okno WPF s jedním tlačítkem šablony – tlačítko elipsa](media/create-apply-template/styled-button.png)

Možná jste si všimli, že tlačítko není kruh, ale je zkosený. Vzhledem k tomu, jak **\<Ellipse>** element funguje, se vždy rozšíří, aby vyplnilo dostupný prostor. Označit kroužek jako Uniform změnou vlastností Button a na **:::no-loc text="width":::** **:::no-loc text="height":::** stejnou hodnotu:

[!code-xaml[StyledButtonSize](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window3.xaml#StyledButtonSize)]

![Okno WPF s jedním kulatým tlačítkem šablony](media/create-apply-template/styled-uniform-button.png)

## <a name="add-a-trigger"></a>Přidání triggeru

I když tlačítko s použitou šablonou vypadá jinak, chová se stejně jako jakékoli jiné tlačítko. Po stisknutí tlačítka se <xref:System.Windows.Controls.Primitives.ButtonBase.Click> událost aktivuje. Ale možná jste si všimli, že když přesunete ukazatel myši na tlačítko, vizuály tlačítka se nezmění. Tyto interakce vizuálů jsou všechny definované šablonou.

Díky dynamickým systémům událostí a vlastností, které poskytuje WPF, můžete sledovat konkrétní vlastnost pro určitou hodnotu a pak šablonu v případě potřeby přeformátovat. V tomto příkladu budete sledovat <xref:System.Windows.UIElement.IsMouseOver> vlastnost tlačítka. Když je ukazatel myši nad ovládacím prvkem, styl **\<Ellipse>** s novou barvou. Tento typ triggeru se označuje jako *PropertyTrigger*.

Aby to fungovalo, budete muset přidat název do **\<Ellipse>** , na který můžete odkazovat. Dejte mu název **backgroundElement**.

[!code-xaml[EllipseName](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window4.xaml#EllipseName)]

Dále přidejte nový <xref:System.Windows.Trigger> do kolekce [ControlTemplate. Triggers](xref:System.Windows.Controls.ControlTemplate.Triggers) . Aktivační událost bude sledovat `IsMouseOver` událost pro danou hodnotu `true` .

[!code-xaml[ControlTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window4.xaml?name=ControlTemplate&highlight=6-10)]

Dále přidejte do, **\<Setter>** **\<Trigger>** který změní vlastnost **Fill** na **\<Ellipse>** novou barvu.

[!code-xaml[MouseOver](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window5.xaml#MouseOver)]

Spusťte projekt. Všimněte si, že když přesunete ukazatel myši na tlačítko, barva **\<Ellipse>** změn.

![Změna barvy výplně tlačítkem myši se pohybuje přes tlačítko WPF](media/create-apply-template/mouse-move-over-button.gif)

## <a name="use-a-visualstate"></a>Použití VisualState

Vizuální stavy jsou definovány a aktivovány ovládacím prvkem. Například když se ukazatel myši přesune nad ovládací prvek, `CommonStates.MouseOver` stav se aktivuje. Můžete animovat změny vlastností na základě aktuálního stavu ovládacího prvku. V předchozí části **\<PropertyTrigger>** byl použit příkaz pro změnu popředí tlačítka na hodnotu, `AliceBlue` Pokud `IsMouseOver` byla vlastnost `true` . Místo toho vytvořte vizuální stav, který animuje změnu této barvy, čímž zajistíte hladký přechod. Další informace o *VisualStates*naleznete v tématu [styly a šablony v WPF](../fundamentals/styles-templates-overview.md#visual-states).

Chcete-li převést na **\<PropertyTrigger>** animovaný vizuální stav, nejprve odeberte **\<ControlTemplate.Triggers>** prvek ze šablony.

[!code-xaml[CleanTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window5.xaml#CleanTemplate)]

Dále v **\<Grid>** kořenovém adresáři šablony ovládacího prvku přidejte **\<VisualStateManager.VisualStateGroups>** element **\<VisualStateGroup>** pro `CommonStates` . Definujte dva stavy `Normal` a `MouseOver` .

[!code-xaml[VisualState](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window6.xaml#VisualState)]

V **\<VisualState>** případě, že je tento stav aktivován, jsou aplikovány jakékoli animace definované v. Vytváření animací pro každý stav Animace jsou umístěny uvnitř **\<Storyboard>** elementu. Další informace o scénářích najdete v tématu [Přehled scénářů](../../framework/wpf/graphics-multimedia/storyboards-overview.md).

- Normální

  Tento stav animuje výplň elipsy a obnoví ji do barvy ovládacího prvku `Background` .

  [!code-xaml[NormalState](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window6.xaml#NormalState)]

- MouseOver

  Tento stav animuje barvu elipsy `Background` na novou barvu: `Yellow` .

  [!code-xaml[MouseOverState](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window6.xaml#MouseOverState)]

**\<ControlTemplate>** By měl nyní vypadat takto.

[!code-xaml[FinalTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window7.xaml#FinalTemplate)]

Spusťte projekt. Všimněte si, že když přesunete ukazatel myši na tlačítko, barva **\<Ellipse>** animace.

![Změna barvy výplně tlačítkem myši se pohybuje přes tlačítko WPF](media/create-apply-template/mouse-move-over-button-visualstate.gif)

## <a name="next-steps"></a>Další kroky

- [Vytvoření stylu pro ovládací prvek v subsystému WPF](../fundamentals/styles-templates-create-apply-style.md)
- [Styly a šablony v subsystému WPF](../fundamentals/styles-templates-overview.md)
- [Přehled prostředků XAML](../fundamentals/xaml-resources-define.md)

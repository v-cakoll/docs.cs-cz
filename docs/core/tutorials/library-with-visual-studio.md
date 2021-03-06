---
title: Vytvoření .NET Standard knihovny tříd pomocí sady Visual Studio
description: Naučte se vytvářet .NET Standard knihovny tříd pomocí sady Visual Studio.
ms.date: 06/08/2020
dev_langs:
- csharp
- vb
ms.custom: vs-dotnet
ms.openlocfilehash: 69259b1d47a8e30945c578db10c6d697c81fa261
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2020
ms.locfileid: "87164401"
---
# <a name="tutorial-create-a-net-standard-library-using-visual-studio"></a>Kurz: Vytvoření knihovny .NET Standard pomocí sady Visual Studio

V tomto kurzu vytvoříte jednoduchou knihovnu nástrojů, která obsahuje jedinou metodu pro zpracování řetězců. Implementujete ho jako [metodu rozšíření](../../csharp/programming-guide/classes-and-structs/extension-methods.md) , takže ji můžete zavolat, jako kdyby byla členem <xref:System.String> třídy.

*Knihovna tříd* definuje typy a metody, které jsou volány aplikací. Knihovna tříd, která cílí na .NET Standard 2,0, umožňuje, aby byla vaše knihovna volána jakoukoli implementací .NET, která podporuje tuto verzi .NET Standard. Po dokončení knihovny tříd ji můžete distribuovat jako součást třetí strany nebo jako součást balíčku s jednou nebo více aplikacemi.

## <a name="prerequisites"></a>Požadavky

- [Visual Studio 2019 verze 16,6 nebo novější](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) s nainstalovanou úlohou **vývoje .NET Core pro různé platformy** . Sada .NET Core 3,1 SDK se automaticky nainstaluje při výběru této úlohy.

  Další informace najdete v části [instalace pomocí sady Visual Studio](../install/sdk.md?pivots=os-windows#install-with-visual-studio) v článku [instalace .NET Core SDK](../install/sdk.md?pivots=os-windows) .

## <a name="create-a-solution"></a>Vytvoření řešení

Začněte vytvořením prázdného řešení pro vložení projektu knihovny tříd do. Řešení sady Visual Studio slouží jako kontejner pro jeden nebo více projektů. Do stejného řešení přidáte další související projekty.

Vytvoření prázdného řešení:

1. Spusťte Visual Studio.

2. V okně Start vyberte možnost **vytvořit nový projekt**.

3. Na stránce **vytvořit nový projekt** zadejte do vyhledávacího pole **řešení** . Zvolte šablonu **prázdného řešení** a klikněte na tlačítko **Další**.

   ![Prázdná šablona řešení v aplikaci Visual Studio](media/library-with-visual-studio/blank-solution.png)

4. Na stránce **Konfigurovat nový projekt** zadejte do pole **název projektu** **ClassLibraryProjects** . Potom zvolte **Create** (Vytvořit).

## <a name="create-a-class-library-project"></a>Vytvořit projekt knihovny tříd

1. Přidejte do řešení nový projekt knihovny tříd .NET Standard s názvem "StringLibrary".

   1. V **Průzkumník řešení** klikněte pravým tlačítkem na řešení a vyberte **Přidat**  >  **Nový projekt**.

   1. Na stránce **Přidat nový projekt** zadejte do vyhledávacího pole **Library** . V seznamu jazyk vyberte **C#** nebo **Visual Basic** a pak vyberte **všechny platformy** ze seznamu platforem. Zvolte šablonu **Knihovna tříd (.NET Standard)** a klikněte na tlačítko **Další**.

   1. Na stránce **Konfigurovat nový projekt** zadejte do pole **název projektu** **StringLibrary** . Pak zvolte **vytvořit**.

1. Zkontrolujte, zda je knihovna cílena na správnou verzi .NET Standard. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt knihovny a pak vyberte **vlastnosti**. Textové pole **cílové rozhraní** uvádí, že cíle projektu .NET Standard 2,0.

   ![Vlastnosti projektu pro knihovnu tříd](./media/library-with-visual-studio/library-project-properties.png)

1. Pokud používáte Visual Basic, vymažte text v textovém poli **kořenový obor názvů** .

   ![Vlastnosti projektu pro knihovnu tříd](./media/library-with-visual-studio/vb/library-project-properties.png)

   Pro každý projekt Visual Basic automaticky vytvoří obor názvů, který odpovídá názvu projektu. V tomto kurzu definujete obor názvů nejvyšší úrovně pomocí [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md) klíčového slova v souboru kódu.

1. Nahraďte kód v okně Code pro *Class1.cs* nebo *Class1. vb* následujícím kódem a uložte soubor. Pokud jazyk, který chcete použít, není zobrazen, změňte selektor jazyka v horní části stránky.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/StringLibrary/Class1.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/StringLibrary/Class1.vb":::

   Knihovna tříd, `UtilityLibraries.StringLibrary` , obsahuje metodu s názvem `StartsWithUpper` . Tato metoda vrací <xref:System.Boolean> hodnotu, která označuje, zda aktuální instance řetězce začíná velkým znakem. Standard Unicode rozlišuje velká písmena od malých písmen. <xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType>Metoda vrátí, `true` zda je znak velkými písmeny.

1. Na panelu nabídek vyberte **sestavit**  >  **sestavení řešení** a ověřte, že se projekt zkompiluje bez chyby.

## <a name="add-a-console-app-to-the-solution"></a>Přidání konzolové aplikace do řešení

Přidejte konzolovou aplikaci, která používá knihovnu tříd. Aplikace vyzve uživatele, aby zadal řetězec a nahlásil, jestli řetězec začíná velkým znakem.

1. Do řešení přidejte novou konzolovou aplikaci .NET Core s názvem prezentující.

   1. V **Průzkumník řešení** klikněte pravým tlačítkem na řešení a vyberte **Přidat**  >  **Nový projekt**.

   1. Na stránce **Přidat nový projekt** zadejte do vyhledávacího pole **Console** . V seznamu jazyk vyberte **C#** nebo **Visual Basic** a pak vyberte **všechny platformy** ze seznamu platforem.

   1. Zvolte šablonu **Konzolová aplikace (.NET Core)** a klikněte na tlačítko **Další**.

   1. Na stránce **Konfigurovat nový projekt** zadejte do pole **název projektu** **prezentující** . Potom zvolte **Create** (Vytvořit).

1. V okně kódu pro soubor *program.cs* nebo *program. vb* nahraďte celý kód následujícím kódem.

   :::code language="csharp" source="./snippets/library-with-visual-studio/csharp/ShowCase/Program.cs":::
   :::code language="vb" source="./snippets/library-with-visual-studio/vb/ShowCase/Program.vb":::

   Kód používá `row` proměnnou k udržování počtu řádků dat zapsaných do okna konzoly. Pokaždé, když je větší nebo rovno 25, kód vymaže okno konzoly a zobrazí uživateli zprávu.

   Program vyzve uživatele k zadání řetězce. Označuje, zda řetězec začíná velkým znakem. Pokud uživatel stiskne klávesu <kbd>ENTER</kbd> bez zadání řetězce, aplikace skončí a okno konzoly se zavře.

## <a name="add-a-project-reference"></a>Přidat odkaz na projekt

Zpočátku má nový projekt konzolové aplikace přístup ke knihovně tříd. Chcete-li, aby mohla volat metody v knihovně tříd, vytvořte odkaz na projekt knihovny tříd.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na `ShowCase` uzel **závislosti** projektu a vyberte možnost **Přidat odkaz na projekt**.

   ![Přidat kontextovou nabídku odkazu v aplikaci Visual Studio](media/library-with-visual-studio/add-reference-context-menu.png)

1. V dialogovém okně **Správce odkazů** vyberte projekt **StringLibrary** a vyberte **OK**.

   ![Dialog Správce odkazů s vybraným StringLibrary](media/library-with-visual-studio/manage-project-references.png)

## <a name="run-the-app"></a>Spuštění aplikace

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **prezentace** a v místní nabídce vyberte **nastavit jako spouštěný projekt** .

   ![Místní nabídka projektu sady Visual Studio pro nastavení spouštěného projektu](media/library-with-visual-studio/set-startup-project-context-menu.png)

1. Stisknutím klávesy <kbd>CTRL</kbd> + <kbd>F5</kbd> zkompilujete a spustíte program bez ladění.

   ![Panel nástrojů projekt sady Visual Studio zobrazující tlačítko ladění](media/library-with-visual-studio/visual-studio-project-toolbar.png)

1. Vyzkoušejte program zadáním řetězců a stisknutím klávesy <kbd>ENTER</kbd>a stisknutím klávesy <kbd>ENTER</kbd> ukončete.

   :::image type="content" source="media/library-with-visual-studio/run-showcase.png" alt-text="Okno konzoly s předvedením":::

## <a name="additional-resources"></a>Další zdroje

* [Vývoj knihoven pomocí .NET Core CLI](libraries.md)
* [.NET Standard verze a podporované platformy](../../standard/net-standard.md).

## <a name="next-steps"></a>Další kroky

V tomto kurzu jste vytvořili řešení, přidali projekt knihovny a Přidali jste projekt konzolové aplikace, který používá knihovnu. V dalším kurzu přidáte do řešení projekt testování částí.

> [!div class="nextstepaction"]
> [Testování knihovny .NET Standard pomocí .NET Core pomocí sady Visual Studio](testing-library-with-visual-studio.md)

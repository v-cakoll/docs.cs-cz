---
title: Použití pojmenovaných a nepovinných argumentů v programování pro systém Office – Průvodce programováním v C#
description: Naučte se používat pojmenované argumenty a volitelné argumenty pro usnadnění přístupu k rozhraním COM, jako jsou systém Microsoft Office rozhraní API pro automatizaci.
ms.date: 07/20/2015
helpviewer_keywords:
- named and optional arguments [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
ms.assetid: 65b8a222-bcd8-454c-845f-84adff5a356f
ms.openlocfilehash: 7e24331d37e8fdbe2bc66a2d9f73a5f6a7242af9
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/21/2020
ms.locfileid: "86864342"
---
# <a name="how-to-use-named-and-optional-arguments-in-office-programming-c-programming-guide"></a>Použití pojmenovaných a nepovinných argumentů v programování pro systém Office (Průvodce programováním v C#)

Pojmenované argumenty a nepovinné argumenty, představené v C# 4, vylepšují pohodlí, flexibilitu a čitelnost v programování v jazyce C#. Kromě toho tyto funkce významně usnadňují přístup k rozhraním COM, jako jsou systém Microsoft Office rozhraní API pro automatizaci.

V následujícím příkladu má metoda [ConvertToTable](<xref:Microsoft.Office.Interop.Word.Range.ConvertToTable%2A>) šestnáct parametrů, které reprezentují vlastnosti tabulky, jako je počet sloupců a řádků, formátování, ohraničení, písma a barvy. Všechny šestnácté parametry jsou volitelné, protože většina času neumožňuje zadat konkrétní hodnoty pro všechny. Bez pojmenovaných a nepovinných argumentů však musí být pro každý parametr zadána hodnota nebo zástupný symbol. U pojmenovaných a nepovinných argumentů zadáte hodnoty pouze pro parametry, které jsou požadovány pro váš projekt.

Aby bylo možné dokončit tyto postupy, je nutné, aby byl v počítači nainstalován systém Microsoft Office Word.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-a-new-console-application"></a>Vytvoření nové konzolové aplikace

1. Spusťte Visual Studio.

2. V nabídce **soubor** přejděte na příkaz **Nový**a klikněte na **projekt**.

3. V podokně **Kategorie šablon** rozbalte položku **Visual C#** a potom klikněte na možnost **Windows**.

4. Podívejte se v horní části podokna **šablony** , abyste se ujistili, že se v poli **cílová architektura** zobrazí **.NET Framework 4** .

5. V podokně **šablony** klikněte na **Konzolová aplikace**.

6. Do pole **název** zadejte název projektu.

7. Klikněte na **OK**.

     Nový projekt se zobrazí v **Průzkumník řešení**.

## <a name="to-add-a-reference"></a>Přidání odkazu

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na název projektu a pak klikněte na **Přidat odkaz**. Zobrazí se dialogové okno **Přidat odkaz** .

2. Na stránce **.NET** vyberte v seznamu **název součásti** možnost **Microsoft. Office. Interop. Word** .

3. Klikněte na **OK**.

## <a name="to-add-necessary-using-directives"></a>Přidání nezbytných direktiv using

1. V **Průzkumník řešení**klikněte pravým tlačítkem na soubor *program.cs* a pak klikněte na **Zobrazit kód**.

2. `using`Do horní části souboru kódu přidejte následující direktivy:

     [!code-csharp[csProgGuideNamedAndOptional#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#4)]

## <a name="to-display-text-in-a-word-document"></a>Zobrazení textu v dokumentu aplikace Word

1. Do `Program` třídy v *program.cs*přidejte následující metodu pro vytvoření aplikace Word a wordového dokumentu. Metoda [Add](<xref:Microsoft.Office.Interop.Word.Documents.Add%2A>) má čtyři volitelné parametry. V tomto příkladu se používají výchozí hodnoty. Proto nejsou v příkazu call nutné žádné argumenty.

     [!code-csharp[csProgGuideNamedAndOptional#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#6)]

2. Na konec metody přidejte následující kód, který definuje, kde se má v dokumentu zobrazovat text, a zobrazený text:

     [!code-csharp[csProgGuideNamedAndOptional#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#7)]

## <a name="to-run-the-application"></a>Spuštění aplikace

1. Přidejte následující příkaz do Main:

     [!code-csharp[csProgGuideNamedAndOptional#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#8)]

2. Stisknutím klávesy <kbd>CTRL</kbd> + <kbd>F5</kbd> spusťte projekt. Zobrazí se dokument aplikace Word obsahující zadaný text.

## <a name="to-change-the-text-to-a-table"></a>Změna textu na tabulku
  
1. `ConvertToTable`K uzavření textu v tabulce použijte metodu. Metoda má 16 nepovinných parametrů. IntelliSense vloží volitelné parametry do závorek, jak je znázorněno na následujícím obrázku.

     ![Seznam parametrů pro metodu ConvertToTable](./media/how-to-use-named-and-optional-arguments-in-office-programming/convert-table-parameters.png)

     Pojmenované a volitelné argumenty umožňují zadat hodnoty pouze pro parametry, které chcete změnit. Přidejte následující kód na konec metody `DisplayInWord` pro vytvoření jednoduché tabulky. Argument určuje, že čárky v textovém řetězci jsou `range` oddělené buňkami v tabulce.

     [!code-csharp[csProgGuideNamedAndOptional#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#9)]

     V dřívějších verzích jazyka C# volání `ConvertToTable` vyžaduje pro každý parametr odkazový argument, jak je znázorněno v následujícím kódu:
  
     [!code-csharp[csProgGuideNamedAndOptional#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#14)]

2. Stisknutím klávesy <kbd>CTRL</kbd> + <kbd>F5</kbd> spusťte projekt.

## <a name="to-experiment-with-other-parameters"></a>Experimentování s jinými parametry

1. Chcete-li změnit tabulku tak, aby měla jeden sloupec a tři řádky, nahraďte poslední řádek v `DisplayInWord` následujícím příkazem a zadejte <kbd>klávesu CTRL</kbd> + <kbd>F5</kbd>.  

     [!code-csharp[csProgGuideNamedAndOptional#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#10)]

2. Chcete-li pro tabulku zadat předdefinovaný formát, nahraďte poslední řádek příkazem `DisplayInWord` následujícím příkazem a zadejte <kbd>klávesu CTRL</kbd> + <kbd>F5</kbd>. Formát může být libovolná konstanta [WdTableFormat](<xref:Microsoft.Office.Interop.Word.WdTableFormat>) .

     [!code-csharp[csProgGuideNamedAndOptional#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#11)]

## <a name="example"></a>Příklad

Následující kód obsahuje úplný příklad:

 [!code-csharp[csProgGuideNamedAndOptional#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#12)]

## <a name="see-also"></a>Viz také

- [Pojmenované a nepovinné argumenty](./named-and-optional-arguments.md)

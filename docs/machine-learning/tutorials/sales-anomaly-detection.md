---
title: 'Kurz: zjištění anomálií v prodeji produktu'
description: Naučte se, jak vytvořit aplikaci pro detekci anomálií pro prodejní data produktu. Tento kurz vytvoří konzolovou aplikaci .NET Core pomocí jazyka C# v aplikaci Visual Studio 2019.
ms.date: 06/30/2020
ms.topic: tutorial
ms.custom: mvc, title-hack-0612
ms.openlocfilehash: cf61f197e4befebdbb1fbf2ca4cbcdc61c48780a
ms.sourcegitcommit: 97ce5363efa88179dd76e09de0103a500ca9b659
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/13/2020
ms.locfileid: "86281664"
---
# <a name="tutorial-detect-anomalies-in-product-sales-with-mlnet"></a>Kurz: zjištění anomálií v prodeji produktů pomocí ML.NET

Naučte se, jak vytvořit aplikaci pro detekci anomálií pro prodejní data produktu. Tento kurz vytvoří konzolovou aplikaci .NET Core pomocí jazyka C# v aplikaci Visual Studio.

V tomto kurzu se naučíte:
> [!div class="checklist"]
>
> * Načtení dat
> * Vytvoření transformace pro detekci anomálií špičky
> * Zjištění anomálií špičky pomocí transformace
> * Vytvoření transformace pro detekci anomálií bodu změny
> * Detekovat anomálie změn bodů pomocí transformace

Zdrojový kód pro tento kurz najdete v úložišti [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) .

## <a name="prerequisites"></a>Požadavky

* [Visual Studio 2017 verze 15,6 nebo novější](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) s nainstalovanou úlohou vývoj .NET Core pro různé platformy.

* [Datová sada product-sales.csv](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)

>[!NOTE]
> Formát dat v nástroji `product-sales.csv` je založen na datové sadě "šampon Sales" za tříleté období "původně nacházejícím z datového trhu a poskytovaných pomocí TSDL (Time Series data Library), které vytvořila Rob Hyndman.
> "Nemožnost prodeje za tři roky v rámci" datové sady ", která je licencovaná na základě výchozího Open License pro datamarketo.

## <a name="create-a-console-application"></a>Vytvoření konzolové aplikace

1. Vytvořte **konzolovou aplikaci .NET Core** nazvanou "ProductSalesAnomalyDetection".

2. Vytvořte v projektu adresář s názvem *data* a uložte soubory sady dat.

3. Nainstalujte **balíček NuGet Microsoft.ml**:

    [!INCLUDE [mlnet-current-nuget-version](../../../includes/mlnet-current-nuget-version.md)]

    V Průzkumník řešení klikněte pravým tlačítkem na projekt a vyberte **Spravovat balíčky NuGet**. Jako zdroj balíčku zvolte "nuget.org", vyberte kartu Procházet, vyhledejte **Microsoft.ml** a vyberte tlačítko **nainstalovat** . Pokud souhlasíte s licenčními podmínkami pro uvedené balíčky, klikněte na tlačítko **OK** v dialogovém okně **Náhled změn** a potom v dialogovém okně pro **přijetí licence** vyberte tlačítko **přijmout** . Opakujte tento postup pro **Microsoft. ml. časové řady**.

4. Do `using` horní části souboru *program.cs* přidejte následující příkazy:

    [!code-csharp[AddUsings](./snippets/sales-anomaly-detection/csharp/Program.cs#AddUsings "Add necessary usings")]

### <a name="download-your-data"></a>Stažení vašich dat

1. Stáhněte si datovou sadu a uložte ji do složky *dat* , kterou jste vytvořili dříve:

   * Klikněte pravým tlačítkem na [*product-sales.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv) a vyberte Uložit odkaz (nebo cíl) jako...

     Ujistěte se \* , že soubor. csv buď uložíte do složky *dat* , nebo když ho uložíte jinam, přesuňte \* soubor. CSV do složky *data* .

2. V Průzkumník řešení klikněte pravým tlačítkem na \* soubor. csv a vyberte **vlastnosti**. V části **Upřesnit**změňte hodnotu **Kopírovat do výstupního adresáře** na **Kopírovat, pokud je novější**.

Následující tabulka je náhled dat ze \* souboru. CSV:

|Month  |ProductSales |
|-------|-------------|
|1 – leden  |    271      |
|2 – leden  |    150,9    |
|.....  |    .....    |
|1 – únor  |    199,3    |
|.....  |    .....    |

### <a name="create-classes-and-define-paths"></a>Vytváření tříd a definování cest

Dále definujte vstupní a předpovědní datové struktury třídy.

Přidejte do projektu novou třídu:

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat > nová položka**.

2. V **dialogovém okně Přidat novou položku**vyberte **třída** a změňte pole **název** na *ProductSalesData.cs*. Pak vyberte tlačítko **Přidat** .

   V editoru kódu se otevře soubor *ProductSalesData.cs* .

3. `using`Do horní části *ProductSalesData.cs*přidejte následující příkaz:

   ```csharp
   using Microsoft.ML.Data;
   ```

4. Odeberte existující definici třídy a přidejte následující kód, který má dvě třídy `ProductSalesData` a `ProductSalesPrediction` , do souboru *ProductSalesData.cs* :

    [!code-csharp[DeclareTypes](./snippets/sales-anomaly-detection/csharp/ProductSalesData.cs#DeclareTypes "Declare data record types")]

    `ProductSalesData`Určuje vstupní datovou třídu. Atribut [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) určuje, které sloupce (podle indexu sloupce) v datové sadě by měly být načteny.

    `ProductSalesPrediction`Určuje třídu dat předpovědi. Pro detekci anomálií se předpověď skládá z výstrahy, která indikuje, jestli existuje anomálie, hrubá skóre a hodnota p-. Bližší hodnota p je 0, pravděpodobnější je, že došlo k anomálii.

5. Vytvořte dvě globální pole, která budou uchovávat nedávno staženou cestu k souboru datové sady a uloženou cestu k souboru modelu:

    * `_dataPath`má cestu k datové sadě, která se používá ke výukě modelu.
    * `_docsize`obsahuje počet záznamů v souboru datové sady. Použijete `_docSize` k výpočtu `pvalueHistoryLength` .

6. Přidejte následující kód na řádek přímo nad `Main` metodu pro určení těchto cest:

    [!code-csharp[Declare global variables](./snippets/sales-anomaly-detection/csharp/Program.cs#DeclareGlobalVariables "Declare global variables")]

### <a name="initialize-variables-in-main"></a>Inicializovat proměnné v Main

1. Nahraďte `Console.WriteLine("Hello World!")` řádek v `Main` metodě následujícím kódem pro deklaraci a inicializaci `mlContext` proměnné:

    [!code-csharp[CreateMLContext](./snippets/sales-anomaly-detection/csharp/Program.cs#CreateMLContext "Create the ML Context")]

    [Třída MLContext](xref:Microsoft.ML.MLContext) je výchozím bodem pro všechny operace ml.NET a inicializace `mlContext` vytvoří nové prostředí ml.NET, které lze sdílet napříč objekty pracovního postupu vytváření modelů. Je podobný, koncepčně, na `DBContext` v Entity Framework.

### <a name="load-the-data"></a>Načtení dat

Data v ML.NET jsou reprezentována jako [Třída IDataView](xref:Microsoft.ML.IDataView). `IDataView`je flexibilní a efektivní způsob, jak popsat tabulková data (číselná a text). Data je možné načíst z textového souboru nebo z jiných zdrojů (například databáze SQL nebo souborů protokolu) do `IDataView` objektu.

1. Jako další řádek metody přidejte následující kód `Main()` :

    [!code-csharp[LoadData](./snippets/sales-anomaly-detection/csharp/Program.cs#LoadData "loading dataset")]

    [LoadFromTextFile ()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29) definuje schéma dat a čte data v souboru. Převezme proměnné cesty k datům a vrátí `IDataView` .

## <a name="time-series-anomaly-detection"></a>Detekce anomálií časové řady

Detekce anomálií označuje neočekávané nebo neobvyklé události nebo chování. Dává v tom, kde hledat problémy a pomáhá zodpovědět otázku "je to divné?".

![Příklad detekce anomálií "je tímto divné".](./media/sales-anomaly-detection/time-series-anomaly-detection.png)

Detekce anomálií je proces zjišťování nezaložených dat časových řad. body v dané vstupní časové řadě, kde chování není očekávané, nebo "divné".

Detekce anomálií může být užitečná v mnoha různých ohledech. Například:

Pokud máte auto, možná budete chtít vědět, že je tento měřič ropy čten běžným způsobem nebo mám netěsnost?
Pokud sledujete spotřebu energie, měli byste si být vědomi, že dochází k výpadku.

Existují dva typy anomálií časových řad, které je možné zjistit:

* **Špičky** označují dočasné shluky chování neobvyklé v systému.

* **Body změny** označují začátek trvalých změn v průběhu času v systému.

V ML.NET jsou algoritmy detekce špičky IID nebo identifikátory identifikátoru IID pro [nezávislou a identickou distribuovanou](https://en.wikipedia.org/wiki/Independent_and_identically_distributed_random_variables)datovou sadu vhodné.

Na rozdíl od modelů v ostatních kurzech transformace detektoru časové řady transformují provoz přímo na vstupní data. `IEstimator.Fit()`Metoda nepotřebuje k tvorbě transformace data školení. To sice potřebuje schéma dat, které je dostupné v zobrazení dat vygenerovaném z prázdného seznamu `ProductSalesData` .

Budete analyzovat stejná prodejní data produktu za účelem detekce Špičk a změn bodů. Proces vytváření a školicích modelů je stejný pro detekci špičky a detekci bodu změny; Hlavním rozdílem je konkrétní použitý algoritmus detekce.

## <a name="spike-detection"></a>Detekce špičky

Cílem detekce špičky je identifikovat náhlé ještě dočasné shluky, které se významně liší od většiny hodnot dat časových řad. Je důležité detekovat tyto podezřelé výjimečné položky, události nebo pozorování včas, aby byly minimalizovány. K detekci nejrůznějších anomálií, jako jsou výpadky, internetoví útoky nebo virové webovému obsahu, se dá použít následující přístup. Následující obrázek je příkladem špičky v datové sadě časových řad:

![Snímek obrazovky, který zobrazuje dvě detekce špičky.](./media/sales-anomaly-detection/two-spike-detections.png)

### <a name="add-the-createemptydataview-method"></a>Přidání metody CreateEmptyDataView ()

Přidejte následující metodu do `Program.cs` :

[!code-csharp[CreateEmptyDataView](./snippets/sales-anomaly-detection/csharp/Program.cs#CreateEmptyDataView)]

`CreateEmptyDataView()`Vytvoří prázdný objekt zobrazení dat se správným schématem, který se použije jako vstup do `IEstimator.Fit()` metody.

### <a name="create-the-detectspike-method"></a>Vytvoření metody DetectSpike ()

`DetectSpike()`Metoda:

* Vytvoří transformaci z Estimator.
* Detekuje špičky na základě historických dat o prodeji.
* Zobrazí výsledky.

1. Vytvořte `DetectSpike()` metodu hned za `Main()` metodou pomocí následujícího kódu:

    ```csharp
    static void DetectSpike(MLContext mlContext, int docSize, IDataView productSales)
    {

    }
    ```

1. Pomocí [IidSpikeEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidSpikeEstimator) můžete vyškolit model pro detekci špičky. Přidejte ho do `DetectSpike()` metody s následujícím kódem:

    [!code-csharp[AddSpikeTrainer](./snippets/sales-anomaly-detection/csharp/Program.cs#AddSpikeTrainer)]

1. Vytvořte transformaci detekce špičkou přidáním následujícího jako další řádek kódu v `DetectSpike()` metodě:

    [!code-csharp[TrainModel1](./snippets/sales-anomaly-detection/csharp/Program.cs#TrainModel1)]

1. Přidejte následující řádek kódu pro transformaci `productSales` dat jako další řádek v `DetectSpike()` metodě:

    [!code-csharp[TransformData1](./snippets/sales-anomaly-detection/csharp/Program.cs#TransformData1)]

    Předchozí kód používá metodu [Transform ()](xref:Microsoft.ML.ITransformer.Transform%2A) k vytvoření předpovědi pro více vstupních řádků datové sady.

1. Převeďte `transformedData` do silného typu `IEnumerable` pro snazší zobrazení pomocí metody [CreateEnumerable ()](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) s následujícím kódem:

    [!code-csharp[CreateEnumerable1](./snippets/sales-anomaly-detection/csharp/Program.cs#CreateEnumerable1)]

1. Pomocí následujícího kódu vytvořte řádek záhlaví zobrazení <xref:System.Console.WriteLine?displayProperty=nameWithType> :

    [!code-csharp[DisplayHeader1](./snippets/sales-anomaly-detection/csharp/Program.cs#DisplayHeader1)]

    Ve výsledcích detekce špičky zobrazíte následující informace:

    * `Alert`Označuje upozornění špičky pro daný datový bod.
    * `Score`je `ProductSales` hodnota pro daný datový bod v datové sadě.
    * `P-Value`"P" představuje pravděpodobnost. Bližší hodnota p je 0, pravděpodobnější je, že datový bod je anomálie.

1. Použijte následující kód k iterování `predictions` `IEnumerable` a zobrazení výsledků:

    [!code-csharp[DisplayResults1](./snippets/sales-anomaly-detection/csharp/Program.cs#DisplayResults1)]

1. Přidejte volání do `DetectSpike()` metody v `Main()` metodě:

    [!code-csharp[CallDetectSpike](./snippets/sales-anomaly-detection/csharp/Program.cs#CallDetectSpike)]

## <a name="spike-detection-results"></a>Výsledky detekce špičky

Výsledky by měly vypadat podobně jako následující. Během zpracování se zobrazí zprávy. Můžou se zobrazovat upozornění nebo zpracovávat zprávy. Některé zprávy byly pro přehlednost odebrány z následujících výsledků.

```console
Detect temporary changes in pattern
=============== Training the model ===============
=============== End of training process ===============
Alert   Score   P-Value
0       271.00  0.50
0       150.90  0.00
0       188.10  0.41
0       124.30  0.13
0       185.30  0.47
0       173.50  0.47
0       236.80  0.19
0       229.50  0.27
0       197.80  0.48
0       127.90  0.13
1       341.50  0.00 <-- Spike detected
0       190.90  0.48
0       199.30  0.48
0       154.50  0.24
0       215.10  0.42
0       278.30  0.19
0       196.40  0.43
0       292.00  0.17
0       231.00  0.45
0       308.60  0.18
0       294.90  0.19
1       426.60  0.00 <-- Spike detected
0       269.50  0.47
0       347.30  0.21
0       344.70  0.27
0       445.40  0.06
0       320.90  0.49
0       444.30  0.12
0       406.30  0.29
0       442.40  0.21
1       580.50  0.00 <-- Spike detected
0       412.60  0.45
1       687.00  0.01 <-- Spike detected
0       480.30  0.40
0       586.30  0.20
0       651.90  0.14
```

## <a name="change-point-detection"></a>Detekce bodu změny

`Change points`jsou trvalé změny v průběhu distribuce hodnot datového proudu událostí, jako jsou například změny úrovně a trendy. Tyto trvalé změny jsou poslední mnohem delší než `spikes` a mohly označovat závažné události. `Change points`nejsou obvykle viditelné pro holé oči, ale lze je zjistit ve vašich datech pomocí přístupů, jako je například v následující metodě.  Následující obrázek je příkladem detekce bodu změny:

![Snímek obrazovky, který ukazuje detekci bodu změny.](./media/sales-anomaly-detection/change-point-detection.png)

### <a name="create-the-detectchangepoint-method"></a>Vytvoření metody DetectChangepoint ()

`DetectChangepoint()`Metoda provádí následující úlohy:

* Vytvoří transformaci z Estimator.
* Detekuje body změn na základě historických dat o prodeji.
* Zobrazí výsledky.

1. Vytvořte `DetectChangepoint()` metodu hned za `Main()` metodou pomocí následujícího kódu:

    ```csharp
    static void DetectChangepoint(MLContext mlContext, int docSize, IDataView productSales)
    {

    }
    ```

1. Vytvořte [iidChangePointEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidChangePointEstimator) v `DetectChangepoint()` metodě s následujícím kódem:

    [!code-csharp[AddChangepointTrainer](./snippets/sales-anomaly-detection/csharp/Program.cs#AddChangepointTrainer)]

1. Jak jste předtím pracovali, vytvořte transformaci z Estimator přidáním následujícího řádku kódu do `DetectChangePoint()` metody:

    [!code-csharp[TrainModel2](./snippets/sales-anomaly-detection/csharp/Program.cs#TrainModel2)]

1. Použijte `Transform()` metodu pro transformaci dat přidáním následujícího kódu do `DetectChangePoint()` :

    [!code-csharp[TransformData2](./snippets/sales-anomaly-detection/csharp/Program.cs#TransformData2)]

1. Jak jste předtím pracovali, převeďte `transformedData` na silný typ `IEnumerable` pro snadnější zobrazení pomocí `CreateEnumerable()` metody s následujícím kódem:

    [!code-csharp[CreateEnumerable2](./snippets/sales-anomaly-detection/csharp/Program.cs#CreateEnumerable2)]

1. Vytvořte záhlaví zobrazení s následujícím kódem jako další řádek v `DetectChangePoint()` metodě:

    [!code-csharp[DisplayHeader2](./snippets/sales-anomaly-detection/csharp/Program.cs#DisplayHeader2)]

    Ve výsledcích detekce bodů změny se zobrazí následující informace:

    * `Alert`Označuje upozornění na změnu bodu pro daný datový bod.
    * `Score`je `ProductSales` hodnota pro daný datový bod v datové sadě.
    * `P-Value`"P" představuje pravděpodobnost. Bližší hodnota P je 0, pravděpodobnější je, že datový bod je anomálie.
    * `Martingale value`slouží k identifikaci způsobu, jakým je "divné" a datovým bodem "na základě sekvence hodnot P.

1. Iterujte pomocí `predictions` `IEnumerable` a zobrazte výsledky s následujícím kódem:

    [!code-csharp[DisplayResults2](./snippets/sales-anomaly-detection/csharp/Program.cs#DisplayResults2)]

1. Do metody přidejte následující volání `DetectChangepoint()` metody `Main()` :

    [!code-csharp[CallDetectChangepoint](./snippets/sales-anomaly-detection/csharp/Program.cs#CallDetectChangepoint)]

## <a name="change-point-detection-results"></a>Výsledky detekce bodu změny

Výsledky by měly vypadat podobně jako následující. Během zpracování se zobrazí zprávy. Můžou se zobrazovat upozornění nebo zpracovávat zprávy. Některé zprávy byly pro přehlednost odebrány z následujících výsledků.

```console
Detect Persistent changes in pattern
=============== Training the model Using Change Point Detection Algorithm===============
=============== End of training process ===============
Alert   Score   P-Value Martingale value
0       271.00  0.50    0.00
0       150.90  0.00    2.33
0       188.10  0.41    2.80
0       124.30  0.13    9.16
0       185.30  0.47    9.77
0       173.50  0.47    10.41
0       236.80  0.19    24.46
0       229.50  0.27    42.38
1       197.80  0.48    44.23 <-- alert is on, predicted changepoint
0       127.90  0.13    145.25
0       341.50  0.00    0.01
0       190.90  0.48    0.01
0       199.30  0.48    0.00
0       154.50  0.24    0.00
0       215.10  0.42    0.00
0       278.30  0.19    0.00
0       196.40  0.43    0.00
0       292.00  0.17    0.01
0       231.00  0.45    0.00
0       308.60  0.18    0.00
0       294.90  0.19    0.00
0       426.60  0.00    0.00
0       269.50  0.47    0.00
0       347.30  0.21    0.00
0       344.70  0.27    0.00
0       445.40  0.06    0.02
0       320.90  0.49    0.01
0       444.30  0.12    0.02
0       406.30  0.29    0.01
0       442.40  0.21    0.01
0       580.50  0.00    0.01
0       412.60  0.45    0.01
0       687.00  0.01    0.12
0       480.30  0.40    0.08
0       586.30  0.20    0.03
0       651.90  0.14    0.09
```

Blahopřejeme! Teď jste úspěšně vytvořili modely strojového učení pro zjišťování špiček a anomálií bodů změn v prodejních datech.

Zdrojový kód pro tento kurz najdete v úložišti [dotnet/Samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) .

V tomto kurzu jste se naučili:
> [!div class="checklist"]
>
> * Načtení dat
> * Vyškolit model pro detekci anomálií špičky
> * Zjištění anomálií špičky pomocí trained model
> * Výuka modelu pro detekci anomálií bodů změn
> * Detekovat anomálie bodů změny v proškolených režimech

## <a name="next-steps"></a>Další kroky

Podívejte se na úložiště GitHub Samples Machine Learning a prozkoumejte ukázku detekce anomálií spotřeby energie.
> [!div class="nextstepaction"]
> [dotnet/machinelearning-Samples – úložiště GitHub](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/AnomalyDetection_PowerMeterReadings)

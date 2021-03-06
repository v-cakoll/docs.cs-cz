---
title: Vytváření pracovních postupů, aktivit a výrazů pomocí imperativního kódu
description: Definice pracovního postupu v rámci Workflow Foundation je stromem nakonfigurovaných objektů aktivit. Pomocí kódu můžete vytvářet definice pracovních postupů, aktivity a výrazy.
ms.date: 03/30/2017
ms.assetid: cefc9cfc-2882-4eb9-8c94-7a6da957f2b2
ms.openlocfilehash: d8b4cb8b85d3ea3759d58e15df823a72146772e8
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421550"
---
# <a name="authoring-workflows-activities-and-expressions-using-imperative-code"></a>Vytváření pracovních postupů, aktivit a výrazů pomocí imperativního kódu
Definice pracovního postupu je stromem nakonfigurovaných objektů aktivity. Tento strom aktivit lze definovat mnoha způsoby, například ruční úpravou kódu XAML nebo pomocí Návrhář postupu provádění k vytvoření XAML. Použití XAML však není požadavkem. Definice pracovních postupů je také možné vytvářet programově. Toto téma poskytuje přehled o vytváření definic, aktivit a výrazů pracovního postupu pomocí kódu. Příklady práce s pracovními postupy XAML pomocí kódu naleznete v tématu [serializace pracovních postupů a aktivit do a z jazyka XAML](serializing-workflows-and-activities-to-and-from-xaml.md).  
  
## <a name="creating-workflow-definitions"></a>Vytváření definic pracovních postupů  
 Definici pracovního postupu lze vytvořit vytvořením instance typu aktivity a konfigurací vlastností objektu aktivity. Pro aktivity, které neobsahují podřízené aktivity, lze to provést pomocí několika řádků kódu.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#47](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#47)]  
  
> [!NOTE]
> Příklady v tomto tématu slouží <xref:System.Activities.WorkflowInvoker> ke spuštění ukázkových pracovních postupů. Další informace o vyvolání pracovních postupů, předávání argumentů a různých možností hostování, které jsou k dispozici, najdete v tématu [použití WorkflowInvoker a WorkflowApplication](using-workflowinvoker-and-workflowapplication.md).  
  
 V tomto příkladu je vytvořen pracovní postup, který se skládá z jedné <xref:System.Activities.Statements.WriteLine> aktivity. <xref:System.Activities.Statements.WriteLine> <xref:System.Activities.Statements.WriteLine.Text%2A> Argument aktivity je nastaven a je vyvolán pracovní postup. Pokud aktivita obsahuje podřízené aktivity, je metoda konstrukce podobná. V následujícím příkladu je použita <xref:System.Activities.Statements.Sequence> aktivita, která obsahuje dvě <xref:System.Activities.Statements.WriteLine> aktivity.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#48](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#48)]  
  
### <a name="using-object-initializers"></a>Použití inicializátorů objektů  
 Příklady v tomto tématu používají syntaxi inicializace objektu. Syntaxe inicializace objektu může být užitečný způsob, jak vytvořit definice pracovních postupů v kódu, protože poskytuje hierarchické zobrazení aktivit v pracovním postupu a znázorňuje vztah mezi aktivitami. Při vytváření pracovních postupů prostřednictvím kódu programu není nutné používat syntaxi inicializace objektu. Následující příklad je funkčně ekvivalentní k předchozímu příkladu.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#49](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#49)]  
  
 Další informace o inicializátorech objektů naleznete v tématu [How to: Initialize Objects bez volání konstruktoru (Průvodce programováním v C#)](../../csharp/programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md) a [Postupy: deklarace objektu pomocí inicializátoru objektu](../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md).  
  
### <a name="working-with-variables-literal-values-and-expressions"></a>Práce s proměnnými, hodnotami literálů a výrazy  
 Při vytváření definice pracovního postupu pomocí kódu si uvědomte, jaký kód je proveden jako součást vytvoření definice pracovního postupu a jaký kód je proveden jako součást provádění instance daného pracovního postupu. Například následující pracovní postup má za cíl Generovat náhodné číslo a zapsat ho do konzoly.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#50](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#50)]  
  
 Když je tento kód definice pracovního postupu proveden, volání `Random.Next` je provedeno a výsledek je uložen do definice pracovního postupu jako hodnota literálu. Je možné vyvolat mnoho instancí tohoto pracovního postupu a vše by zobrazilo stejné číslo. Aby došlo k vytvoření náhodného čísla během provádění pracovního postupu, je nutné použít výraz, který je vyhodnocen při každém spuštění pracovního postupu. V následujícím příkladu se výraz Visual Basic používá s <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> .  
  
 [!code-csharp[CFX_WorkflowApplicationExample#51](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#51)]  
  
 Výraz v předchozím příkladu může být také implementován pomocí <xref:Microsoft.CSharp.Activities.CSharpValue%601> výrazu a jazyka C#.  
  
```csharp  
new Assign<int>  
{  
    To = n,  
    Value = new CSharpValue<int>("new Random().Next(1, 101)")  
}  
```  
  
 Výrazy jazyka C# musí být zkompilovány před tím, než je vyvolán pracovní postup, který je obsahuje. Pokud nejsou výrazy jazyka C# kompilovány, <xref:System.NotSupportedException> je vyvolána při vyvolání pracovního postupu s následující zprávou: ``Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`` ve většině scénářů zahrnujícím pracovní postupy vytvořené v aplikaci Visual Studio jsou výrazy jazyka c# kompilovány automaticky, ale v některých scénářích, jako jsou například pracovní postupy kódu, musí být výrazy jazyka c# manuálně zkompilovány. Příklad, jak zkompilovat výrazy jazyka C#, naleznete v části [using c# Expressions v tématu Code Workflows in](csharp-expressions.md#CodeWorkflows) [Expressions jazyka c#](csharp-expressions.md) .  
  
 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>Představuje výraz v Visual Basic syntaxi, kterou lze použít jako r-hodnotu ve výrazu a <xref:Microsoft.CSharp.Activities.CSharpValue%601> představuje výraz v syntaxi jazyka C#, který lze použít jako r-hodnotu ve výrazu. Tyto výrazy jsou vyhodnocovány při každém spuštění aktivity obsahující. Výsledek výrazu je přiřazen proměnné pracovního postupu `n` a tyto výsledky jsou používány další aktivitou v pracovním postupu. Pro přístup k hodnotě proměnné pracovního postupu `n` za běhu se <xref:System.Activities.ActivityContext> vyžaduje. K tomuto lze přistupovat pomocí následujícího výrazu lambda.  
  
> [!NOTE]
> Všimněte si, že oba tyto kódy jsou příklady použití jazyka C# jako programovacího jazyka, ale jedna používá <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> a jeden používá <xref:Microsoft.CSharp.Activities.CSharpValue%601> . <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>a <xref:Microsoft.CSharp.Activities.CSharpValue%601> lze jej použít v projektech Visual Basic i C#. Ve výchozím nastavení se výrazy vytvořené v Návrháři pracovních postupů shodují s jazykem hostujícího projektu. Při vytváření pracovních postupů v kódu je požadovaný jazyk na uvážení autora pracovního postupu.  
  
 V těchto příkladech je výsledek výrazu přiřazen proměnné pracovního postupu `n` a tyto výsledky jsou využívány další aktivitou v pracovním postupu. Pro přístup k hodnotě proměnné pracovního postupu `n` za běhu se <xref:System.Activities.ActivityContext> vyžaduje. K tomuto lze přistupovat pomocí následujícího výrazu lambda.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#52](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#52)]  
  
 Další informace o výrazech lambda naleznete v tématu [lambda Expressions (C# Programming Guide)](../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) nebo [lambda výrazy (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 Výrazy lambda nelze serializovat do formátu XAML. Je-li proveden pokus o serializaci pracovního postupu s výrazy lambda, <xref:System.Activities.Expressions.LambdaSerializationException> je vyvolána následující zpráva: "Tento pracovní postup obsahuje lambda výrazy zadané v kódu. Tyto výrazy nejsou serializovatelný v jazyce XAML. Aby bylo možné vytvořit serializovatelný pracovní postup v jazyce XAML, buď použijte VisualBasicValue/VisualBasicReference nebo ExpressionServices. Convert (lambda). Tato akce převede výrazy lambda na aktivity výrazu. " Chcete-li tento výraz kompatibilní s jazykem XAML, použijte <xref:System.Activities.Expressions.ExpressionServices> a <xref:System.Activities.Expressions.ExpressionServices.Convert%2A> , jak je znázorněno v následujícím příkladu.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#53](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#53)]  
  
 Lze <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> také použít. Všimněte si, že při použití výrazu Visual Basic není vyžadován žádný výraz lambda.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#54](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#54)]  
  
 V době běhu jsou Visual Basic výrazy kompilovány do výrazů LINQ. Oba předchozí příklady jsou serializovatelné na XAML, ale pokud je serializovaný kód XAML určen k zobrazení a úpravám v Návrháři pracovních postupů, použijte <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> pro své výrazy. Serializované pracovní postupy, které používají, `ExpressionServices.Convert` lze otevřít v návrháři, ale hodnota výrazu bude prázdná. Další informace o serializaci pracovních postupů do jazyka XAML naleznete v tématu [serializace pracovních postupů a aktivit do a z jazyka XAML](serializing-workflows-and-activities-to-and-from-xaml.md).  
  
#### <a name="literal-expressions-and-reference-types"></a>Literálové výrazy a typy odkazů  
 Literálové výrazy jsou v pracovních postupech zastoupeny <xref:System.Activities.Expressions.Literal%601> aktivitou. Následující <xref:System.Activities.Statements.WriteLine> aktivity jsou funkčně ekvivalentní.  
  
```csharp  
new WriteLine  
{  
    Text = "Hello World."  
},  
new WriteLine  
{  
    Text = new Literal<string>("Hello World.")  
}  
```  
  
 Není platná inicializace literálového výrazu s jakýmkoli odkazovým typem s výjimkou <xref:System.String> . V následujícím příkladu <xref:System.Activities.Statements.Assign> <xref:System.Activities.Statements.Assign.Value%2A> je vlastnost aktivity inicializována s výrazem literálu pomocí `List<string>` .  
  
```csharp  
new Assign  
{  
    To = new OutArgument<List<string>>(items),  
    Value = new InArgument<List<string>>(new List<string>())  
},  
```  
  
 Když se ověří pracovní postup obsahující tuto aktivitu, vrátí se následující chyba ověřování: "Literal podporuje jenom typy hodnot a neměnný typ System. String. Typ System. Collections. Generic. list ' 1 [System. String] nelze použít jako literál. " Pokud je pracovní postup vyvolán, <xref:System.Activities.InvalidWorkflowException> je vyvolána výjimka, která obsahuje text chyby ověření. Jedná se o chybu ověřování, protože při vytváření literálového výrazu s odkazovým typem není vytvořena nová instance typu odkazu pro každou instanci pracovního postupu. Chcete-li tento problém vyřešit, nahraďte literálový výraz jedním z nich, který vytvoří a vrátí novou instanci typu odkazu.  
  
```csharp  
new Assign  
{  
    To = new OutArgument<List<string>>(items),  
    Value = new InArgument<List<string>>(new VisualBasicValue<List<string>>("New List(Of String)"))  
},  
```  
  
 Další informace o výrazech naleznete v tématu [Expressions](expressions.md).  
  
#### <a name="invoking-methods-on-objects-using-expressions-and-the-invokemethod-activity"></a>Vyvolání metod u objektů pomocí výrazů a aktivity InvokeMethod  
 <xref:System.Activities.Expressions.InvokeMethod%601>Aktivitu lze použít k vyvolání statických a instančních metod třídy v .NET Framework. V předchozím příkladu v tomto tématu bylo vygenerováno náhodné číslo pomocí <xref:System.Random> třídy.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#51](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#51)]  
  
 <xref:System.Activities.Expressions.InvokeMethod%601>Aktivita může být také použita k volání <xref:System.Random.Next%2A> metody <xref:System.Random> třídy.  
  
```csharp  
new InvokeMethod<int>  
{  
    TargetObject = new InArgument<Random>(new VisualBasicValue<Random>("New Random()")),  
    MethodName = "Next",  
    Parameters =
    {  
        new InArgument<int>(1),  
        new InArgument<int>(101)  
    },  
    Result = n  
}  
```  
  
 Vzhledem k tomu <xref:System.Random.Next%2A> , že není statická metoda, <xref:System.Random> je pro vlastnost zadána instance třídy <xref:System.Activities.Expressions.InvokeMethod%601.TargetObject%2A> . V tomto příkladu je nová instance vytvořena pomocí výrazu Visual Basic, ale mohla být také vytvořena dříve a uložena v proměnné pracovního postupu. V tomto příkladu by bylo jednodušší použít <xref:System.Activities.Statements.Assign%601> aktivitu namísto <xref:System.Activities.Expressions.InvokeMethod%601> aktivity. Pokud volání metody, které nakonec vyvolaly <xref:System.Activities.Statements.Assign%601> <xref:System.Activities.Expressions.InvokeMethod%601> aktivity nebo, má dlouhodobě spuštěný, <xref:System.Activities.Expressions.InvokeMethod%601> má výhodu, protože má <xref:System.Activities.Expressions.InvokeMethod%601.RunAsynchronously%2A> vlastnost. Pokud je tato vlastnost nastavena na `true` , vyvolaná metoda bude spuštěna asynchronně s ohledem na pracovní postup. Pokud jsou paralelně jiné aktivity, nebudou při asynchronním provádění metody zablokovány. Také, pokud metoda, která má být vyvolána, nemá žádnou návratovou hodnotu, pak <xref:System.Activities.Expressions.InvokeMethod%601> je vhodným způsobem, jak metodu vyvolat.  
  
## <a name="arguments-and-dynamic-activities"></a>Argumenty a dynamické aktivity  
 Definice pracovního postupu je vytvořena v kódu sestavením aktivit do stromu aktivity a konfigurací jakýchkoli vlastností a argumentů. Existující argumenty mohou být vázány, ale do aktivit nelze přidávat nové argumenty. Patří sem argumenty pracovního postupu, které jsou předány kořenové aktivitě. V imperativním kódu jsou argumenty pracovního postupu zadány jako vlastnosti pro nový typ CLR a v jazyce XAML jsou deklarovány pomocí `x:Class` a `x:Member` . Vzhledem k tomu, že není vytvořen žádný nový typ CLR, když je definice pracovního postupu vytvořena jako strom objektů v paměti, nelze přidat argumenty. Argumenty však lze přidat do <xref:System.Activities.DynamicActivity> . V tomto příkladu <xref:System.Activities.DynamicActivity%601> je vytvořena, který přijímá dva celočíselné argumenty, přidá je dohromady a vrátí výsledek. Vytvoří <xref:System.Activities.DynamicActivityProperty> se pro každý argument a výsledek operace je přiřazen k <xref:System.Activities.Activity%601.Result%2A> argumentu <xref:System.Activities.DynamicActivity%601> .  
  
 [!code-csharp[CFX_WorkflowApplicationExample#55](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#55)]  
  
 Další informace o dynamických aktivitách najdete v tématu [vytvoření aktivity za běhu](creating-an-activity-at-runtime-with-dynamicactivity.md).  
  
## <a name="compiled-activities"></a>Zkompilované aktivity  
 Dynamické aktivity představují jeden ze způsobů, jak definovat aktivity, které obsahují argumenty pomocí kódu, ale aktivity lze také vytvořit v kódu a kompilovat do typů. Je možné vytvořit jednoduché aktivity, které jsou odvozeny z <xref:System.Activities.CodeActivity> a asynchronní aktivity odvozené z <xref:System.Activities.AsyncCodeActivity> . Tyto aktivity mohou mít argumenty, vracet hodnoty a definovat jejich logiku pomocí imperativního kódu. Příklady vytváření těchto typů aktivit naleznete v tématu [základní třída CodeActivity](workflow-activity-authoring-using-the-codeactivity-class.md) a [Vytváření asynchronních aktivit](creating-asynchronous-activities-in-wf.md).  
  
 Aktivity, které jsou odvozeny z, <xref:System.Activities.NativeActivity> mohou definovat svou logiku pomocí imperativního kódu a mohou také obsahovat podřízené aktivity, které definují logiku. Mají také plný přístup k funkcím modulu runtime, jako je vytváření záložek. Příklady vytváření <xref:System.Activities.NativeActivity> aktivit na základě naleznete v tématu [základní třída NativeActivity](nativeactivity-base-class.md), [Postupy: vytvoření aktivity](how-to-create-an-activity.md)a [vlastní složený s použitím nativní aktivity](./samples/custom-composite-using-native-activity.md) Sample.  
  
 Aktivity, které jsou odvozeny z <xref:System.Activities.Activity> definice své logiky výhradně prostřednictvím použití podřízených aktivit. Tyto aktivity jsou obvykle vytvářeny pomocí návrháře pracovních postupů, ale lze je také definovat pomocí kódu. V následujícím příkladu `Square` je definována aktivita, která je odvozena z `Activity<int>` . `Square`Aktivita má jednu <xref:System.Activities.InArgument%601> s názvem `Value` a definuje její logiku zadáním <xref:System.Activities.Statements.Sequence> aktivity pomocí <xref:System.Activities.Activity.Implementation%2A> Vlastnosti. <xref:System.Activities.Statements.Sequence>Aktivita obsahuje <xref:System.Activities.Statements.WriteLine> aktivitu a <xref:System.Activities.Statements.Assign%601> aktivitu. Tyto tři aktivity společně implementují logiku `Square` aktivity.  
  
```csharp  
class Square : Activity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Value { get; set; }  
  
    public Square()  
    {  
        this.Implementation = () => new Sequence  
        {  
            Activities =  
            {  
                new WriteLine  
                {  
                    Text = new InArgument<string>((env) => "Squaring the value: " + this.Value.Get(env))  
                },  
                new Assign<int>  
                {  
                    To = new OutArgument<int>((env) => this.Result.Get(env)),  
                    Value = new InArgument<int>((env) => this.Value.Get(env) * this.Value.Get(env))  
                }  
            }  
        };  
    }  
}  
```  
  
 V následujícím příkladu je vyvolána definice pracovního postupu skládající se z jedné `Square` aktivity pomocí <xref:System.Activities.WorkflowInvoker> .  
  
```csharp  
Dictionary<string, object> inputs = new Dictionary<string, object> {{ "Value", 5}};  
int result = WorkflowInvoker.Invoke(new Square(), inputs);  
Console.WriteLine("Result: {0}", result);  
```  
  
 Po vyvolání pracovního postupu se do konzoly zobrazí následující výstup:  
  
 **Umocnění hodnotu: 5**  
**Výsledek: 25**

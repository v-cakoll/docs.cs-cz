---
title: Návrh parametru
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- member design guidelines [.NET Framework], parameters
- members [.NET Framework], parameters
- names [.NET Framework], parameters
- parameters, design guidelines
- reserved parameters
ms.assetid: 3f33bf46-4a7b-43b3-bb78-1ffebe0dcfa6
ms.openlocfilehash: e0bc52f5679a7771d5690be9f903e677ce611605
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621584"
---
# <a name="parameter-design"></a>Návrh parametru

Tato část obsahuje obecné pokyny pro návrh parametrů, včetně oddílů s pokyny pro kontrolu argumentů. Kromě toho byste měli postupovat podle pokynů popsaných v tématu [parametry pojmenování](naming-parameters.md).

 ✔️ použít nejmenší odvozený typ parametru, který poskytuje funkce vyžadované členem.

 Předpokládejme například, že chcete navrhnout metodu, která vytvoří výčet kolekce a vytiskne každou položku do konzoly. Taková metoda by měla být provedena <xref:System.Collections.IEnumerable> jako parametr, nikoli <xref:System.Collections.ArrayList> nebo <xref:System.Collections.IList> , například.

 ❌Nepoužívejte rezervované parametry.

 Pokud je v některé budoucí verzi potřeba více vstupů ke členu, může být přidáno nové přetížení.

 ❌Nemají veřejně vystavené metody, které přebírají ukazatele, pole ukazatelů nebo multidimenzionální pole jako parametry.

 Ukazatele a multidimenzionální pole jsou poměrně obtížné použít. Ve většině případů je možné rozhraní API přenavrhovat, aby se předešlo přebírání těchto typů jako parametrů.

 ✔️ umístit všechny `out` parametry za všechny parametry podle hodnoty a `ref` parametrů (kromě polí parametrů), a to i v případě, že výsledkem je nekonzistence v pořadí parametrů mezi přetíženími (viz téma [přetížení člena](member-overloading.md)).

 `out`Parametry lze zobrazit jako nadbytečné návratové hodnoty a jejich seskupení usnadňuje pochopení signatury metody.

 ✔️ být v parametrech pojmenování konzistentní při přepisování členů nebo implementaci členů rozhraní.

 Tím se lépe komunikuje vztah mezi metodami.

### <a name="choosing-between-enum-and-boolean-parameters"></a>Volba mezi výčtovým a logickým parametrem  
 ✔️ použít výčty, pokud by měl člen jinak mít dva nebo více logických parametrů.

 ❌Nepoužívejte logické hodnoty, pokud nebudete naprosto jisti, že nikdy nebude potřeba více než dvě hodnoty.

 Výčty umožňují určit místo pro budoucí sčítání hodnot, ale měli byste si uvědomit o všech důsledcích přidávání hodnot do výčtů, které jsou popsány v [návrhu výčtu](enum.md).

 ✔️ Zvažte použití logických hodnot pro parametry konstruktoru, které jsou skutečné hodnoty dvou stavů a slouží pouze k inicializaci logických vlastností.

### <a name="validating-arguments"></a>Ověřují se argumenty
 ✔️ PROVÉST ověření argumentů předaných veřejným, chráněným nebo explicitně implementovaným členům. Throw <xref:System.ArgumentException?displayProperty=nameWithType> nebo jedna z jejích podtříd, pokud se ověřování nezdařilo.

 Všimněte si, že skutečné ověření nemusí nutně probíhat ve veřejném nebo chráněném členu. Může dojít na nižší úrovni v některé soukromé nebo interní rutině. Hlavním bodem je, že celá oblast Surface, která je vystavena koncovým uživatelům, kontroluje argumenty.

 ✔️ Vyvolejte <xref:System.ArgumentNullException> , pokud je předán argument null a člen nepodporuje argumenty null.

 ✔️ PROVÉST ověření parametrů výčtu.

 Nepředpokládat argumenty výčtu budou v rozsahu definovaném výčtem. Modul CLR umožňuje přetypování libovolné celočíselné hodnoty do hodnoty Enum i v případě, že ve výčtu není definována hodnota.

 ❌Nepoužívejte <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> pro kontroly rozsahu výčtu.

 ✔️ Upozorňujeme, že po ověření se mohly změnit proměnlivé argumenty.

 Pokud je člen citlivý na zabezpečení, doporučujeme vytvořit kopii a pak ověřit a zpracovat argument.

### <a name="parameter-passing"></a>Předávání parametrů
 Z perspektivy návrháře architektury existují tři hlavní skupiny parametrů: parametry podle hodnoty, `ref` parametry a `out` parametry.

 Pokud je předán argument pomocí parametru podle hodnoty, člen obdrží kopii skutečného předaného argumentu. Pokud je argumentem hodnotový typ, je kopie argumentu vložena do zásobníku. Pokud je argumentem odkazový typ, kopie odkazu je vložena do zásobníku. Nejoblíbenější jazyky CLR, jako je C#, VB.NET a C++, ve výchozím nastavení předávání parametrů podle hodnoty.

 Když je argument předán pomocí `ref` parametru, člen obdrží odkaz na vlastní předaný argument. Pokud je argumentem hodnotový typ, odkaz na argument je vložen do zásobníku. Pokud je argumentem odkazový typ, odkaz na odkaz je vložen do zásobníku. `Ref`parametry lze použít k umožnění člena upravovat argumenty předané volajícím.

 `Out`parametry jsou podobné `ref` parametrům s malým rozdílem. Parametr je zpočátku považován za nepřiřazený a nemůže být načten v těle členu před tím, než se mu přiřadí nějaká hodnota. Parametr musí být také přiřazen určitou hodnotu před tím, než se člen vrátí.

 ❌Vyhněte se použití `out` `ref` parametrů nebo.

 Použití `out` `ref` parametrů or vyžaduje zkušenosti s ukazateli, porozumění způsobu, jakým se liší typy hodnot a typy odkazů, a metody zpracování s více návratových hodnot. Také rozdíl mezi `out` parametry a není `ref` široce srozumitelný. Architektura architekt návrhu pro obecnou cílovou skupinu by neměla očekávat, že uživatelé budou hlavní pracovat s `out` `ref` parametry nebo.

 ❌Nepředávejte odkazový typ odkazem.

 Na pravidlo existují omezené výjimky, jako je například metoda, kterou lze použít k prohození odkazů.

### <a name="members-with-variable-number-of-parameters"></a>Členové s proměnným počtem parametrů
 Členy, kteří mohou převzít proměnný počet argumentů, jsou vyjádřeny zadáním parametru Array. Například <xref:System.String> poskytuje následující metodu:

```csharp
public class String {
    public static string Format(string format, object[] parameters);
}
```

 Uživatel pak může zavolat <xref:System.String.Format%2A?displayProperty=nameWithType> metodu následujícím způsobem:

 `String.Format("File {0} not found in {1}",new object[]{filename,directory});`

 Přidáním klíčového slova param parametrů jazyka C# do parametru pole se změní parametr na parametr pole param, který se nazývá, a poskytuje zástupce pro vytvoření dočasného pole.

```csharp
public class String {
    public static string Format(string format, params object[] parameters);
}
```

 Díky tomu může uživatel volat metodu předáním prvků pole přímo v seznamu argumentů.

 `String.Format("File {0} not found in {1}",filename,directory);`

 Všimněte si, že klíčové slovo params lze přidat pouze k poslednímu parametru v seznamu parametrů.

 ✔️ Zvažte přidání klíčového slova params do parametrů pole, pokud očekáváte, že koncoví uživatelé budou předávat pole s malým počtem prvků. Pokud se očekává, že se v běžných scénářích budou předávat i celá řada prvků, uživatelé pravděpodobně nebudou tyto prvky vložit do seznamu, takže klíčové slovo params není nutné.

 ❌Vyhněte se použití polí param, pokud by volající téměř vždy měl vstup v poli.

 Například členy s parametry bajtového pole by se téměř nikdy nevolaly předáním jednotlivých bajtů. Z tohoto důvodu parametry bajtového pole v .NET Framework nepoužívají klíčové slovo params.

 ❌Nepoužívejte pole param, pokud je pole upraveno členem, který přebírá parametr pole params.

 Vzhledem k tomu, že mnoho kompilátorů přepíná argumenty člena do dočasného pole na webu volání, pole může být dočasným objektem, a proto dojde ke ztrátě všech změn v poli.

 ✔️ Zvažte použití klíčového slova params v jednoduchém přetížení, a to i v případě, že se složitější přetížení nemůže použít.

 Zeptejte se sami, pokud by uživatelé měli hodnotu pole params v jednom přetížení, i když to nebylo ve všech přetíženích.

 ✔️ se pokusíte seřadit parametry, aby bylo možné použít klíčové slovo params.

 ✔️ Zvažte poskytnutí speciálních přetížení a cest kódu pro volání s malým počtem argumentů v rozhraních API s extrémně citlivými na výkon.

 Díky tomu je možné vyhnout se vytváření objektů pole při volání rozhraní API s malým počtem argumentů. Vytvořte názvy parametrů tak, že převezmete jednotný tvar parametru Array a přidáte číselnou příponu.

 Tuto věc byste měli provést pouze v případě, že se chystáte o zvláštní cestu k celému kódu, ne pouze vytvořit pole a volat obecnější metodu.

 ✔️ Upozorňujeme, že hodnota null by mohla být předána jako argument pole param.

 Před zpracováním byste měli ověřit, že pole není null.

 ❌Nepoužívejte `varargs` metody, jinak označované jako tři tečky.

 Některé jazyky CLR, jako je například C++, podporují alternativní konvenci pro předávání seznamů parametrů proměnných nazývaných `varargs` metody. Konvence by se neměla používat v rozhraních, protože není kompatibilní se specifikací CLS.

### <a name="pointer-parameters"></a>Parametry ukazatele
 Obecně platí, že by ukazatelé neměl být uveden v oblasti veřejného povrchu dobře navržené architektury spravovaného kódu. Ve většině případů by měly být ukazatele zapouzdřeny. V některých případech se ale vyžaduje, aby se v případě interoperability a používání ukazatelů v takových případech používaly příslušné ukazatele.

 ✔️ poskytují alternativu pro každého člena, který přebírá argument ukazatele, protože ukazatelé nejsou kompatibilní se specifikací CLS.

 ❌Vyhněte se provádění náročných kontrol argumentů ukazatelů.

 ✔️ se při navrhování členů s ukazateli řídit běžnými konvencemi souvisejícími s ukazateli.

 Například není nutné předávat počáteční index, protože k dosažení stejného výsledku lze použít jednoduchou aritmetickou akci s ukazatelem.

 *Částečně &copy; 2005, 2009 Microsoft Corporation. Všechna práva vyhrazena.*

 *Přetištěno oprávněním Pearsonova vzdělávání, Inc. z [pokynů pro návrh rozhraní: konvence, idiomy a vzory pro opakovaně použitelné knihovny .NET, druhá edice](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) od Krzysztof Cwalina a Brad Abrams, publikovaly 22. října 2008 Addison-Wesley Professional jako součást sady Microsoft Windows Development Series.*

## <a name="see-also"></a>Viz také:

- [Pokyny pro návrh členů](member.md)
- [Pokyny k návrhu architektury](index.md)

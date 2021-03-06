---
title: Typy a proměnné jazyka c# – prohlídka jazyka C#
description: 'Informace o definování typů a deklaraci proměnných v jazyce C #'
ms.date: 04/24/2020
ms.assetid: f8a8051e-0049-43f1-b594-9c84cc7b1224
ms.openlocfilehash: a14291d1eec4d090b0275875326c5a580e5abe9d
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174124"
---
# <a name="types-and-variables"></a>Typy a proměnné

V jazyce C# existují dva druhy typů: *typy hodnot* a *typy odkazů*. Proměnné typů hodnot přímo obsahují svá data, zatímco proměnné typu odkazu ukládají odkazy na jejich data, přičemž ta se označují jako objekty. U typů odkazů je možné, aby dvě proměnné odkazovaly na stejný objekt a bylo tak možné, aby operace s jednou proměnnou ovlivnily objekt, na který je odkazováno z jiné proměnné. S typy hodnot mají proměnné, které mají svou vlastní kopii dat, a není možné, že operace na jednom mají vliv na ostatní (s výjimkou `ref` `out` proměnných parametrů a).

Typy hodnot jazyka C# jsou dále rozděleny na *jednoduché typy*, *výčtové typy*, *typy struktury*a *typy s možnou hodnotou null*. Referenční typy jazyka C# jsou dále rozděleny do *typů tříd*, *typů rozhraní*, *typů polí*a *typů delegátů*.

Následující přehled poskytuje přehled systému typů jazyka C#.

- [Typy hodnot][ValueTypes]
  - [Jednoduché typy][SimpleTypes]
    - Podepsané integrály: `sbyte` , `short` , `int` ,`long`
    - Unsigned integrál: `byte` , `ushort` , `uint` ,`ulong`
    - Znaky Unicode:`char`
    - Binární bod IEEE s plovoucí desetinnou čárkou: `float` ,`double`
    - Desetinná čárka s vysokou přesností:`decimal`
    - Datového`bool`
  - [Výčtové typy][EnumTypes]
    - Uživatelem definované typy formuláře`enum E {...}`
  - [Typy struktury][StructTypes]
    - Uživatelem definované typy formuláře`struct S {...}`
  - [Typy hodnot s povolenou hodnotou Null][NullableTypes]
    - Rozšíření všech ostatních typů hodnot s `null` hodnotou
  - [Typy hodnot řazené kolekce členů][TupleTypes]
    - Uživatelem definované typy formuláře`(T1, T2, ...)`
- [Odkazové typy][ReferenceTypes]
  - [Typy tříd][ClassTypes]
    - Nejvyšší základní třída všech ostatních typů:`object`
    - Řetězce Unicode:`string`
    - Uživatelem definované typy formuláře`class C {...}`
  - [Typy rozhraní][InterfaceTypes]
    - Uživatelem definované typy formuláře`interface I {...}`
  - [Typy polí][ArrayTypes]
    - Jednoduché a multidimenzionální, například `int[]` a`int[,]`
  - [Typy delegátů][DelegateTypes]
    - Uživatelem definované typy formuláře`delegate int D(...)`

[ValueTypes]: ../language-reference/builtin-types/value-types.md
[SimpleTypes]: ../language-reference/builtin-types/value-types.md#built-in-value-types
[EnumTypes]: ../language-reference/builtin-types/enum.md
[StructTypes]: ../language-reference/builtin-types/struct.md
[NullableTypes]: ../language-reference/builtin-types/nullable-value-types.md
[TupleTypes]: ../language-reference/builtin-types/value-tuples.md
[ReferenceTypes]: ../language-reference/keywords/reference-types.md
[ClassTypes]: ../language-reference/keywords/class.md
[InterfaceTypes]: ../language-reference/keywords/interface.md
[DelegateTypes]: ../language-reference/keywords/delegate.md
[ArrayTypes]: ../programming-guide/arrays/index.md

Další informace o číselných typech naleznete v tématu [celočíselné typy](../language-reference/builtin-types/integral-numeric-types.md) a [tabulky typů s plovoucí desetinnou](../language-reference/builtin-types/floating-point-numeric-types.md)čárkou.

Typ jazyka C# `bool` slouží k reprezentaci logických hodnot – hodnot, které jsou buď `true` nebo `false` .

Zpracování znaků a řetězců v jazyce C# používá kódování Unicode. `char`Typ představuje jednotku kódu UTF-16 a `string` Typ představuje sekvenci jednotek kódu UTF-16.

Programy v jazyce C# používají *deklarace typů* k vytváření nových typů. Deklarace typu Určuje název a členy nového typu. Pět kategorií typů v jazyce C# je uživatelsky definované: typy tříd, typy struktury, typy rozhraní, výčtové typy a typy delegátů.

`class`Typ definuje datovou strukturu obsahující datové členy (pole) a členy funkce (metody, vlastnosti a další). Typy tříd podporují jednu dědičnost a polymorfismus, mechanismy, které mohou odvozené třídy roztáhnout a specializovat základní třídy.

`struct`Typ je podobný typu třídy v tom, že představuje strukturu s datovými členy a členy funkce. Nicméně na rozdíl od tříd, struktury jsou typy hodnot a obvykle nevyžadují přidělení haldy. Typy struktury nepodporují uživatelem zadanou dědičnost a všechny typy struktury implicitně dědí z typu `object` .

`interface`Typ definuje kontrakt jako pojmenovanou sadu členů veřejné funkce. `class`Nebo `struct` , který implementuje, `interface` musí poskytnout implementace členů funkce rozhraní. `interface`Může dědit z více základních rozhraní a `class` nebo `struct` může implementovat více rozhraní.

`delegate`Typ představuje odkazy na metody s konkrétním seznamem parametrů a návratovým typem. Delegáti umožňují zacházet s metodami jako s entitami, které lze přiřadit proměnným a předávat jako parametry. Delegáti jsou analogické jako typy funkcí poskytované funkčními jazyky. Jsou také podobné konceptu ukazatelů funkcí nalezených v některých jiných jazycích. Na rozdíl od ukazatelů na funkce jsou delegáti objektově orientovaný a typově bezpečný.

`class`Typy, `struct` , `interface` a `delegate` podporují obecné typy, na jejichž základě lze parametry používat s jinými typy.

`enum`Typ je odlišný typ s pojmenovanými konstantami. Každý `enum` typ má nadřízený typ, který musí být jedním z osmi integrálních typů. Sada hodnot `enum` typu je stejná jako sada hodnot základního typu.

Jazyk C# podporuje jedno a multidimenzionální pole libovolného typu. Na rozdíl od typů uvedených výše nemusí být typy polí deklarovány dříve, než mohou být použity. Místo toho jsou typy polí konstruovány pomocí názvu typu s hranatými závorkami. Například je jednorozměrné pole `int[]` `int` , `int[,]` je dvourozměrné pole `int` , a je jednorozměrné pole jednorozměrného `int[][]` pole v poli `int` .

Typy hodnot s možnou hodnotou null také nemusí být deklarovány dříve, než mohou být použity. Pro každý typ hodnoty `T` , která není null, existuje odpovídající typ hodnoty s možnou hodnotou null `T?` , který může obsahovat další hodnotu, `null` . Například `int?` je typ, který může obsahovat libovolné 32 celé číslo nebo hodnotu `null` .

Systém typů jazyka C# je sjednocením, aby hodnota libovolného typu mohla být považována za `object` . Každý typ v jazyce C# přímo nebo nepřímo je odvozen z `object` typu třídy a `object` je nejvyšší základní třídou všech typů. Hodnoty typů odkazů se považují za objekty pouhým zobrazením hodnot jako typu `object` . Hodnoty typů hodnot se považují za objekty prováděním operací *zabalení* a *rozbalení*. V následujícím příkladu `int` je hodnota převedena na `object` a zpět na `int` .

[!code-csharp[Boxing](../../../samples/snippets/csharp/tour/types-and-variables/Program.cs#L1-L10)]

Při přiřazení hodnoty typu hodnoty k `object` odkazu je "pole" přiděleno pro uchování hodnoty. Toto pole je instancí typu odkazu a hodnota je zkopírována do tohoto pole. Naopak, pokud `object` je odkaz přetypování na typ hodnoty, je provedena kontrolu, že odkazovaná `object` je pole správného typu hodnoty. Pokud je ověření úspěšné, je hodnota v poli zkopírována na typ hodnoty.

Sjednocený Typový systém v jazyce C# znamená, že typy hodnot jsou považovány za `object` odkazy na vyžádání. Z důvodu sjednocení, knihovny pro obecné účely, které používají typ, `object` lze použít se všemi typy odvozenými z `object` , včetně typů odkazů a typů hodnot.

V jazyce C# existuje několik druhů *proměnných* , včetně polí, prvků pole, místních proměnných a parametrů. Proměnné reprezentují umístění úložiště a každá proměnná má typ, který určuje, jaké hodnoty mohou být uloženy v proměnné, jak je znázorněno níže.

- Typ hodnoty, která není null
  - Hodnota, která má přesný typ
- Typ hodnoty s možnou hodnotou null
  - `null`Hodnota nebo hodnota daného přesného typu
- odkazy objektů
  - `null`Odkaz, odkaz na objekt libovolného typu odkazu, nebo odkaz na zabalenou hodnotu libovolného typu hodnoty
- Typ třídy
  - `null`Odkaz, odkaz na instanci tohoto typu třídy nebo odkaz na instanci třídy odvozené z tohoto typu třídy
- Typ rozhraní
  - `null`Odkaz, odkaz na instanci typu třídy, která implementuje tento typ rozhraní, nebo odkaz na zabalenou hodnotu typu hodnoty, který implementuje tento typ rozhraní
- Typ pole
  - `null`Odkaz, odkaz na instanci tohoto typu pole nebo odkaz na instanci kompatibilního typu pole
- Typ delegáta
  - `null`Odkaz nebo odkaz na instanci kompatibilního typu delegáta

> [!div class="step-by-step"]
> [Předchozí](program-structure.md) 
>  [Další](expressions.md)

---
title: Přetížení operátoru
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- operators [.NET Framework], overloads
- names [.NET Framework], overloaded operators
- member design guidelines, operators
- overloaded operators
ms.assetid: 37585bf2-4c27-4dee-849a-af70e3338cc1
ms.openlocfilehash: 893b7d1f76dfb059a0ddca77dfd8654812e9ae12
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289730"
---
# <a name="operator-overloads"></a>Přetížení operátoru
Přetížení operátorů umožňují, aby se typy rozhraní zobrazovaly, jako kdyby byly předdefinované jazykové primitivy.

 I když je v některých situacích povolená a užitečná, je nutné přetížení operátorů používat obezřetně. Existuje mnoho případů, ve kterých je přetížení operátoru zneužití, například když návrháři architektury začali používat operátory pro operace, které by měly být jednoduché metody. Následující pokyny by vám měly pomáhat při rozhodování, kdy a jak používat přetížení operátoru.

 ❌Vyhněte se definování přetížení operátoru, s výjimkou typů, které by se měly cítit jako primitivní (předdefinované) typy.

 ✔️ Zvažte definování přetížení operátoru v typu, který by se měl cítit jako primitivní typ.

 Například <xref:System.String?displayProperty=nameWithType> má a je `operator==` `operator!=` definován.

 ✔️ definovat přetížení operátoru ve strukturách, které reprezentují čísla (například <xref:System.Decimal?displayProperty=nameWithType> ).

 ❌Není roztomilá při definování přetížení operátoru.

 Přetížení operátoru je užitečné v případech, kdy je okamžitě zřejmé, jaký výsledek operace bude. Proto má smysl, aby bylo možné odečíst jeden <xref:System.DateTime> od druhého `DateTime` a získat <xref:System.TimeSpan> . Není však vhodné použít operátor logického sjednocení pro sjednocení dvou databázových dotazů nebo k zápisu do datového proudu pomocí operátoru Shift.

 ❌Neposkytněte přetížení operátoru, pokud alespoň jeden z operandů není typu, který definuje přetížení.

 ✔️ operátory přetížení způsobem symetricky.

 Například při přetížení `operator==` , byste měli také přetížit `operator!=` . Podobně pokud převedete `operator<` , měli byste také přetížit `operator>` a tak dále.

 ✔️ Zvažte poskytnutí metod s popisnými názvy, které odpovídají každému přetíženému operátoru.

 Mnoho jazyků nepodporuje přetížení operátorů. Z tohoto důvodu se doporučuje, aby typy, které přetěžují operátory obsahují sekundární metodu s vhodným názvem domény, který poskytuje ekvivalentní funkce.

 Následující tabulka obsahuje seznam operátorů a odpovídající popisné názvy metod.

|Symbol operátoru C#|Název metadat|Popisný název|
|-------------------------|-------------------|-------------------|
|`N/A`|`op_Implicit`|`To<TypeName>/From<TypeName>`|
|`N/A`|`op_Explicit`|`To<TypeName>/From<TypeName>`|
|`+ (binary)`|`op_Addition`|`Add`|
|`- (binary)`|`op_Subtraction`|`Subtract`|
|`* (binary)`|`op_Multiply`|`Multiply`|
|`/`|`op_Division`|`Divide`|
|`%`|`op_Modulus`|`Mod or Remainder`|
|`^`|`op_ExclusiveOr`|`Xor`|
|`& (binary)`|`op_BitwiseAnd`|`BitwiseAnd`|
|<code>&#124;</code>|`op_BitwiseOr`|`BitwiseOr`|
|`&&`|`op_LogicalAnd`|`And`|
|<code>&#124;&#124;</code>|`op_LogicalOr`|`Or`|
|`=`|`op_Assign`|`Assign`|
|`<<`|`op_LeftShift`|`LeftShift`|
|`>>`|`op_RightShift`|`RightShift`|
|`N/A`|`op_SignedRightShift`|`SignedRightShift`|
|`N/A`|`op_UnsignedRightShift`|`UnsignedRightShift`|
|`==`|`op_Equality`|`Equals`|
|`!=`|`op_Inequality`|`Equals`|
|`>`|`op_GreaterThan`|`CompareTo`|
|`<`|`op_LessThan`|`CompareTo`|
|`>=`|`op_GreaterThanOrEqual`|`CompareTo`|
|`<=`|`op_LessThanOrEqual`|`CompareTo`|
|`*=`|`op_MultiplicationAssignment`|`Multiply`|
|`-=`|`op_SubtractionAssignment`|`Subtract`|
|`^=`|`op_ExclusiveOrAssignment`|`Xor`|
|`<<=`|`op_LeftShiftAssignment`|`LeftShift`|
|`%=`|`op_ModulusAssignment`|`Mod`|
|`+=`|`op_AdditionAssignment`|`Add`|
|`&=`|`op_BitwiseAndAssignment`|`BitwiseAnd`|
|<code>&#124;=</code>|`op_BitwiseOrAssignment`|`BitwiseOr`|
|`,`|`op_Comma`|`Comma`|
|`/=`|`op_DivisionAssignment`|`Divide`|
|`--`|`op_Decrement`|`Decrement`|
|`++`|`op_Increment`|`Increment`|
|`- (unary)`|`op_UnaryNegation`|`Negate`|
|`+ (unary)`|`op_UnaryPlus`|`Plus`|
|`~`|`op_OnesComplement`|`OnesComplement`|

### <a name="overloading-operator-"></a>Operátor přetížení = =
 Přetížení `operator ==` je poměrně komplikované. Sémantika operátoru musí být kompatibilní s několika ostatními členy, například <xref:System.Object.Equals%2A?displayProperty=nameWithType> .

### <a name="conversion-operators"></a>Operátory převodu
 Operátory převodu jsou unární operátory, které umožňují převod z jednoho typu na jiný. Operátory musí být definovány jako statické členy buď na operandu, nebo na návratový typ. Existují dva typy operátorů převodu: implicitní a explicitní.

 ❌Nezadávejte operátor převodu, Pokud koncoví uživatelé tyto převody jasně neočekávají.

 ❌Nedefinujte operátory převodu mimo doménu typu.

 Například,, <xref:System.Int32> <xref:System.Double> a <xref:System.Decimal> jsou všechny číselné typy, zatímco <xref:System.DateTime> není. Proto by neměl být žádný operátor převodu pro převod typu `Double(long)` na `DateTime` . V takovém případě je upřednostňován konstruktor.

 ❌Neposkytněte implicitní operátor převodu, pokud je převod potenciálně ztrátový.

 Například by neměl být implicitní převod z `Double` na na, `Int32` protože `Double` má širší rozsah než `Int32` . Explicitní operátor převodu lze zadat i v případě, že je převod potenciálně ztrátný.

 ❌Nevyvolává výjimky z implicitních přetypování.

 Koncovým uživatelům je velmi obtížné pochopit, co se děje, protože nemusí vědět, že probíhá převod.

 ✔️ vyvolat, <xref:System.InvalidCastException?displayProperty=nameWithType> Pokud volání operátoru přetypování má za následek ztrátový převod a kontrakt operátora nepovoluje ztrátové převody.

 *Části © 2005, 2009 Microsoft Corporation. Všechna práva vyhrazena.*

 *Přetištěno oprávněním Pearsonova vzdělávání, Inc. z [pokynů pro návrh rozhraní: konvence, idiomy a vzory pro opakovaně použitelné knihovny .NET, druhá edice](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) od Krzysztof Cwalina a Brad Abrams, publikovaly 22. října 2008 Addison-Wesley Professional jako součást sady Microsoft Windows Development Series.*

## <a name="see-also"></a>Viz také

- [Pokyny pro návrh členů](member.md)
- [Pokyny k návrhu architektury](index.md)

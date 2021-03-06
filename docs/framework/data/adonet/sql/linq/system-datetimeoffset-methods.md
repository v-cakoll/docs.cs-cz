---
title: Metody System.DateTimeOffset
ms.date: 03/30/2017
ms.assetid: 25b3e5c0-7603-4a70-b3e5-2149e3da69a2
ms.openlocfilehash: 2e29cf02d4f7e8004782264bf940bb1faf393269
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781545"
---
# <a name="systemdatetimeoffset-methods"></a>Metody System.DateTimeOffset
Po namapování v objektovém modelu nebo v souboru externího mapování vám LINQ to SQL umožňuje volat většinu <xref:System.DateTimeOffset?displayProperty=nameWithType> metod, operátorů a vlastností v rámci vašich LINQ to SQL dotazů.  
  
 Jediné metody nejsou podporovány, jsou zděděny z <xref:System.Object?displayProperty=nameWithType> , které nemají smysl v kontextu LINQ to SQL dotazů, jako jsou například: `Finalize`, `GetHashCode`, `GetType` `MemberwiseClone`a. Tyto metody nejsou podporovány, protože LINQ to SQL je nelze přeložit ke spuštění v SQL Server.  
  
> [!NOTE]
> Struktura modulu CLR (Common Language Runtime <xref:System.DateTimeOffset?displayProperty=nameWithType> ) a schopnost namapovat ji na sloupec SQL `DATETIMEOFFSET` s LINQ to SQL vyžaduje .NET Framework 3,5 SP1 nebo novější. Sloupec SQL `DATETIMEOFFSET` je k dispozici pouze v Microsoft SQL Server 2008 a novějších.  
  
## <a name="sqlmethods-date-and-time-methods"></a>SQLMethods metody data a času  
 Kromě metod, které jsou <xref:System.DateTimeOffset> nabízeny strukturou, LINQ to SQL nabízí metody uvedené v následující tabulce <xref:System.Data.Linq.SqlClient.SqlMethods?displayProperty=nameWithType> z třídy pro práci s datem a časem.  
  
||||  
|-|-|-|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffDay%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMillisecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffNanosecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffHour%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMinute%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffSecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMicrosecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMonth%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffYear%2A>|  
  
## <a name="see-also"></a>Viz také:

- [Koncepty dotazů](query-concepts.md)
- [Vytvoření objektového modelu](creating-the-object-model.md)
- [Mapování typů SQL a CLR](sql-clr-type-mapping.md)

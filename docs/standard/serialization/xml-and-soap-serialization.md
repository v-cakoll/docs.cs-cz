---
title: Serializace XML a SOAP
description: Tento přehled popisuje serializaci XML, která se dá použít k serializaci objektů do datových proudů XML, které odpovídají specifikaci SOAP.
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
- serialization, about serialization
- XML serialization
- serialization
ms.assetid: 832ac524-21bc-419a-a27b-ca8bfc45840f
ms.openlocfilehash: 6b7d6f59694a28207758fa7772781eed073917e4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2020
ms.locfileid: "83379547"
---
# <a name="xml-and-soap-serialization"></a>Serializace XML a SOAP

Serializace XML převede (serializace) Veřejná pole a vlastnosti objektu a parametry a návratové hodnoty metod do datového proudu XML, který odpovídá konkrétnímu dokumentu XSD (XML Schema Definition Language). Serializace XML výsledkem silného typu třídy s veřejné vlastnosti a pole, které jsou převedeny na sériového formátu (v tomto případě XML) pro uložení nebo přenos.

Protože kód XML je otevřený standard, může být zpracována datový proud XML ve všech aplikacích, podle potřeby, bez ohledu na platformu. Můžete například webové služby XML vytvořené pomocí technologie ASP.NET použití <xref:System.Xml.Serialization.XmlSerializer> třídy za účelem vytvoření datové proudy XML, který vkládá data mezi aplikací webové služby XML v rámci Internetu nebo v těchto sítích. Deserializace naopak přebírá takové datový proud XML a rekonstruuje objektu.

Serializace XML lze také použít k serializaci objektů do datových proudů XML, které odpovídají specifikaci protokolu SOAP. Protokol SOAP je protokol založený na formát XML, který je určen speciálně k přenosu volání procedur pomocí jazyka XML.

K serializaci nebo deserializaci objektů, použijte <xref:System.Xml.Serialization.XmlSerializer> třídy. Chcete-li vytvořit třídy k serializaci, použijte nástroj definici schématu XML.

## <a name="see-also"></a>Viz také

- [Binární serializace](binary-serialization.md)
- [Webové služby XML vytvořené pomocí ASP.NET a klientů webové služby XML](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))

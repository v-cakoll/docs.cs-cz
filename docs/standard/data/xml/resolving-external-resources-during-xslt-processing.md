---
title: Překlad externích prostředků během zpracování XSLT
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 3a59d31c-0ec5-4de6-a2a9-558531c8116e
ms.openlocfilehash: d38aea1a54c93b00ec14c6aac7ed11ceba288f7b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291497"
---
# <a name="resolving-external-resources-during-xslt-processing"></a>Překlad externích prostředků během zpracování XSLT
V případě transformace XSLT může být několikrát nutné přeložit externí prostředky.  
  
## <a name="using-the-xmlresolver-class"></a>Použití třídy objekt XmlResolver  
 <xref:System.Xml.XmlResolver>Třída se používá k překladu externích prostředků. Následující tabulka popisuje, kdy se <xref:System.Xml.XmlResolver> během zpracování XSLT stala zahrnuta.  
  
|Úloha XSLT|K čemu se objekt XmlResolver používá|  
|---------------|--------------------------------------|  
|Zkompilujte šablonu stylů.|Vyřešte identifikátor URI pro šablonu stylů.<br /><br /> ani<br /><br /> Přeložit odkazy identifikátoru URI v libovolných `xsl:import` `xsl:include` prvcích nebo.|  
|Spusťte šablonu stylů.|Vyřešte identifikátor URI kontextu dokumentu.<br /><br /> ani<br /><br /> Přeložit odkazy identifikátoru URI v jakýchkoli `document()` funkcích XSLT.|  
  
 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A>Metody a <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> zahrnují přetížení, která přijímají <xref:System.Xml.XmlResolver> objekt jako jeden z argumentů. Pokud <xref:System.Xml.XmlResolver> není zadaný, použije se výchozí nastavení <xref:System.Xml.XmlUrlResolver> bez přihlašovacích údajů.  
  
 Následující seznam popisuje, kdy možná budete chtít zadat <xref:System.Xml.XmlResolver> objekt:  
  
- Pokud proces XSLT potřebuje přístup k síťovému prostředku, který vyžaduje ověření, můžete použít <xref:System.Xml.XmlResolver> s potřebnými přihlašovacími údaji.  
  
- Pokud chcete omezit prostředky, ke kterým může proces XSLT přistupovat, můžete použít <xref:System.Xml.XmlSecureResolver> se správnou sadou oprávnění. Třídu použijte v případě, že <xref:System.Xml.XmlSecureResolver> potřebujete otevřít prostředek, který neovládáte nebo který není důvěryhodný.  
  
- Pokud chcete přizpůsobit chování, můžete implementovat vlastní <xref:System.Xml.XmlResolver> třídu a použít ji k řešení prostředků.  
  
- Pokud chcete zajistit, aby nedošlo k žádnému externímu prostředku, můžete `null` pro <xref:System.Xml.XmlResolver> argument zadat.  
  
## <a name="example"></a>Příklad  
 Následující příklad zkompiluje šablonu stylů uloženou v síťovém prostředku. <xref:System.Xml.XmlUrlResolver>Objekt Určuje pověření nutná pro přístup k šabloně stylů.  
  
 [!code-csharp[XslCompiledTransform.Load#11](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Load/CS/Xslt_Load_v2.cs#11)]
 [!code-vb[XslCompiledTransform.Load#11](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Load/VB/Xslt_Load_v2.vb#11)]  
  
## <a name="see-also"></a>Viz také

- <xref:System.Xml.Xsl.XslCompiledTransform>
- <xref:System.Xml.Xsl.XsltSettings>
- [Transformace XSLT](xslt-transformations.md)

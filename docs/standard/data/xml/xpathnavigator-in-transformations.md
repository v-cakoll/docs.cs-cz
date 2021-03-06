---
title: XPathNavigator v transformacích
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 118f97d1-7110-4d1b-b0bd-4143252c0bb0
ms.openlocfilehash: 59fb399d80e1d4d33d1a3c659d2ff74a37fd367d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84282815"
---
# <a name="xpathnavigator-in-transformations"></a>XPathNavigator v transformacích
<xref:System.Xml.XPath.XPathNavigator>Třída poskytuje náhodný přístup jen pro čtení k datům a je určený pro použití jako vstup pro jazyk XSLT (Extensible Stylesheet Language). Je implementována v systémech <xref:System.Xml.XPath.XPathDocument> , <xref:System.Xml.XmlDataDocument> a <xref:System.Xml.XmlDocument> . <xref:System.Xml.XPath.XPathNavigator>Je založena na datovém modelu konsorcium World Wide Web (W3C), jak je popsáno v části 5 doporučení jazyka XML Path (XPath).  
  
 <xref:System.Xml.XPath.XPathNavigator>Definuje model kurzoru v jakémkoli úložišti a poskytuje rychlé dotazy XPath jen pro čtení v jakémkoli úložišti dat. <xref:System.Xml.XPath.XPathNavigator>Je také třída, která se má použít pro iteraci fragmentů stromu výsledků.  
  
 Rozhraní API umožňuje získat informace z aktuálního uzlu ve Storu a přejít na připojené uzly. <xref:System.Xml.XPath.XPathNavigator>Je model stylu kurzoru, který provádí přecházení přes úložiště pomocí sady metod **Move** . <xref:System.Xml.XPath.XPathNavigator>Je vždy umístěn na uzlu. Všechny metody **přesunutí** , které selžou, nezůstane <xref:System.Xml.XPath.XPathNavigator> beze změny.  
  
 <xref:System.Xml.XPath.XPathNavigator>Je třída, která se má použít pro iteraci fragmentů stromu výsledků. Následující ukázka kódu vytvoří fragment stromu výsledek v rámci předlohy se styly voláním funkce s parametrem, `fragment` , který obsahuje XML.  
  
## <a name="testxsl"></a>test. xsl  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl ="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.adventure-works.com"  
                version="1.0">  
  
<xsl:variable name="fragment">  
    <authorlist>  
       <author>Joe</author>  
    </authorlist>  
</xsl:variable>  
  
<msxsl:script language="C#" implements-prefix="user">  
<![CDATA[  
   string NodeFragment(XPathNavigator nav)  
   {  
      if (nav.HasChildren)  
        return nav.Value;  
      else  
        return "";  
   }  
]]>  
</msxsl:script>  
  
<xsl:template match="/">  
     <xsl:value-of select="user:NodeFragment($fragment)"/>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
## <a name="testxml"></a>test. XML  
  
```xml  
<root>Some text</root>  
```  
  
 Následující kód používá **soubor test. xsl** šablony a **test. XML** Input data.  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Xsl  
Imports System.Xml.XPath  
Imports System.Text  
Public Class sample  
  
    Public Shared Sub Main()  
        Dim xslt As New XslTransform()  
        xslt.Load("test.xsl")  
  
        Dim xd As New XPathDocument("test.xml")  
  
        Dim strmTemp = New FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite)  
        xslt.Transform(xd, Nothing, strmTemp, Nothing)  
    End Sub 'Main  
End Class 'sample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Xsl;  
using System.Xml.XPath;  
using System.Text;  
  
public class sample  
{  
    public static void Main()  
    {  
        XslTransform xslt = new XslTransform();  
        xslt.Load("test.xsl");  
  
        XPathDocument xd = new XPathDocument("test.xml");  
  
        Stream strmTemp = new FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite);  
        xslt.Transform(xd, null, strmTemp, null);  
    }  
}  
```  
  
## <a name="output"></a>Výstup  
 Výsledek transformace se nachází v souboru **out. XML**:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>Joe  
```  
  
## <a name="see-also"></a>Viz také

- [Třída XslTransform implementuje procesor XSLT](xsltransform-class-implements-the-xslt-processor.md)

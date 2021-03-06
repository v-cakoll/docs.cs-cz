---
title: Načítání textu odstavců (C#)
ms.date: 07/20/2015
ms.assetid: 127d635e-e559-408f-90c8-2bb621ca50ac
ms.openlocfilehash: 7c47420045def3fe973169e01143646c0f60a8eb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/14/2020
ms.locfileid: "79168242"
---
# <a name="retrieving-the-text-of-the-paragraphs-c"></a>Načítání textu odstavců (C#)
Tento příklad vychází z předchozího příkladu [Načítání odstavců a jejich styly (C#).](./retrieving-the-paragraphs-and-their-styles.md) Tento nový příklad načte text každého odstavce jako řetězec.  
  
 Chcete-li načíst text, tento příklad přidá další dotaz, který iterates prostřednictvím kolekce anonymních typů a `Text`projekty novou kolekci anonymního typu s přidáním nového člena , . Používá standardní <xref:System.Linq.Enumerable.Aggregate%2A> operátor dotazu zřetězit více řetězců do jednoho řetězce.  
  
 Tato technika (to znamená, že nejprve promítá do kolekce anonymního typu, pak pomocí této kolekce pro projekt na novou kolekci anonymního typu) je běžné a užitečné idiom. Tento dotaz mohl být zapsán bez promítání na první anonymní typ. Však z důvodu opožděné vyhodnocení, přitom nepoužívá mnoho dalšího výpočetního výkonu. Idiom vytvoří více objektů s krátkou životností na haldě, ale to podstatně nesnižuje výkon.  
  
 Samozřejmě by bylo možné napsat jeden dotaz, který obsahuje funkce pro načtení odstavců, styl každého odstavce a text každého odstavce. Často je však užitečné rozdělit složitější dotaz na více dotazů, protože výsledný kód je více modulární a snadněji udržovatelné. Kromě toho pokud potřebujete znovu použít část dotazu, je snazší refaktorovat, pokud dotazy jsou zapsány tímto způsobem.  
  
 Tyto dotazy, které jsou zřetězené dohromady, použijte model zpracování, který je podrobně zkoumán v tématu [Kurz: Řetězení dotazů společně (C#)](deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).  
  
## <a name="example"></a>Příklad  
 Tento příklad zpracovává wordprocessingML dokument, určení uzlu prvku, název stylu a text každého odstavce. Tento příklad vychází z předchozích příkladů v tomto kurzu. Nový dotaz je volán v komentářích v níže uvedeném kódu.  
  
 Pokyny k vytvoření zdrojového dokumentu pro tento příklad naleznete [v tématu Vytvoření dokumentu Open XML (C#) zdrojové sady Office](./creating-the-source-office-open-xml-document.md).  
  
 Tento příklad používá třídy z sestavení WindowsBase. Používá typy v <xref:System.IO.Packaging?displayProperty=nameWithType> oboru názvů.  
  
```csharp  
const string fileName = "SampleDoc.docx";  
  
const string documentRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument";  
const string stylesRelationshipType =  
  "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles";  
const string wordmlNamespace =  
  "http://schemas.openxmlformats.org/wordprocessingml/2006/main";  
XNamespace w = wordmlNamespace;  
  
XDocument xDoc = null;  
XDocument styleDoc = null;  
  
using (Package wdPackage = Package.Open(fileName, FileMode.Open, FileAccess.Read))  
{  
    PackageRelationship docPackageRelationship =  
      wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault();  
    if (docPackageRelationship != null)  
    {  
        Uri documentUri = PackUriHelper.ResolvePartUri(new Uri("/", UriKind.Relative),  
          docPackageRelationship.TargetUri);  
        PackagePart documentPart = wdPackage.GetPart(documentUri);  
  
        //  Load the document XML in the part into an XDocument instance.  
        xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()));  
  
        //  Find the styles part. There will only be one.  
        PackageRelationship styleRelation =  
          documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault();  
        if (styleRelation != null)  
        {  
            Uri styleUri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri);  
            PackagePart stylePart = wdPackage.GetPart(styleUri);  
  
            //  Load the style XML in the part into an XDocument instance.  
            styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()));  
        }  
    }  
}  
  
string defaultStyle =
    (string)(  
        from style in styleDoc.Root.Elements(w + "style")  
        where (string)style.Attribute(w + "type") == "paragraph"&&  
              (string)style.Attribute(w + "default") == "1"  
              select style  
    ).First().Attribute(w + "styleId");  
  
// Find all paragraphs in the document.  
var paragraphs =  
    from para in xDoc  
                 .Root  
                 .Element(w + "body")  
                 .Descendants(w + "p")  
    let styleNode = para  
                    .Elements(w + "pPr")  
                    .Elements(w + "pStyle")  
                    .FirstOrDefault()  
    select new  
    {  
        ParagraphNode = para,  
        StyleName = styleNode != null ?  
            (string)styleNode.Attribute(w + "val") :  
            defaultStyle  
    };  
  
// Following is the new query that retrieves the text of  
// each paragraph.  
var paraWithText =  
    from para in paragraphs  
    select new  
    {  
        ParagraphNode = para.ParagraphNode,  
        StyleName = para.StyleName,  
        Text = para  
               .ParagraphNode  
               .Elements(w + "r")  
               .Elements(w + "t")  
               .Aggregate(  
                   new StringBuilder(),  
                   (s, i) => s.Append((string)i),  
                   s => s.ToString()  
               )  
    };  
  
foreach (var p in paraWithText)  
    Console.WriteLine("StyleName:{0} >{1}<", p.StyleName, p.Text);  
```  
  
 Tento příklad vytvoří následující výstup při použití na dokument popsaný v [části Vytvoření dokumentu Open XML (C#) zdrojové kanceláře](./creating-the-source-office-open-xml-document.md).  
  
```output  
StyleName:Heading1 >Parsing WordprocessingML with LINQ to XML<  
StyleName:Normal ><  
StyleName:Normal >The following example prints to the console.<  
StyleName:Normal ><  
StyleName:Code >using System;<  
StyleName:Code ><  
StyleName:Code >class Program {<  
StyleName:Code >    public static void (string[] args) {<  
StyleName:Code >        Console.WriteLine("Hello World");<  
StyleName:Code >    }<  
StyleName:Code >}<  
StyleName:Normal ><  
StyleName:Normal >This example produces the following output:<  
StyleName:Normal ><  
StyleName:Code >Hello World<  
```  
  
## <a name="next-steps"></a>Další kroky  
 Následující příklad ukazuje, jak použít metodu <xref:System.Linq.Enumerable.Aggregate%2A>rozšíření, nikoli , zřetězit více řetězců do jednoho řetězce.  
  
- [Refaktoring pomocí metody rozšíření (C#)](./refactoring-using-an-extension-method.md)  
  
## <a name="see-also"></a>Viz také

- [Kurz: Manipulace s obsahem v dokumentu WordprocessingML (C#)](shape-of-wordprocessingml-documents.md)
- [Odložené spuštění a opožděné vyhodnocení v LINQ na XML (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)

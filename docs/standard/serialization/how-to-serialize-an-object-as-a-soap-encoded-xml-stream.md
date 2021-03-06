---
title: 'Postupy: Serializace objektu jako XML streamu zakódovaného v protokolu SOAP'
description: Naučte se serializovat objekt jako datový proud XML kódovaný pomocí protokolu SOAP. Třída XmlSerializer se dá použít k serializaci tříd a generování kódovaných zpráv SOAP.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
ms.assetid: af406e0a-fa3a-46dd-a7ba-c80731eba3a0
ms.openlocfilehash: 1d38c4e334439ef41b4d4429e52cff04c6463573
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2020
ms.locfileid: "84291562"
---
# <a name="how-to-serialize-an-object-as-a-soap-encoded-xml-stream"></a>Postupy: Serializace objektu jako XML streamu zakódovaného v protokolu SOAP
  
 Vzhledem k tomu, že zpráva SOAP je sestavena pomocí jazyka XML, <xref:System.Xml.Serialization.XmlSerializer> lze třídu použít k serializaci tříd a generování kódovaných zpráv protokolu SOAP. Výsledný kód XML odpovídá [části 5 dokumentu konsorcium World Wide Web "Simple Object Access Protocol (SOAP) 1,1"](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/#_Toc478383512). Při vytváření XML webové služby, které komunikují prostřednictvím zpráv protokolu SOAP, můžete upravit datový proud XML použitím sadu atributů protokolu SOAP speciální třídy a členy třídy. Seznam atributů naleznete v tématu [atributy, které řídí serializaci kódovaných SOAP](attributes-that-control-encoded-soap-serialization.md).  
  
### <a name="to-serialize-an-object-as-a-soap-encoded-xml-stream"></a>K serializaci objektu jako datový proud XML kódováním protokolu SOAP  
  
1. Vytvořte třídu pomocí [nástroje definice schématu XML (XSD. exe)](xml-schema-definition-tool-xsd-exe.md).  
  
2. Použije jeden nebo více atributů speciální nalezen v `System.Xml.Serialization`. Naleznete v seznamu v "Atributy serializace SOAP kódovaného tohoto ovládacího prvku."  
  
3. Vytvořit `XmlTypeMapping` vytvořením nového `SoapReflectionImporter`a volání `ImportTypeMapping` metoda s typem serializovaná třídy.  
  
     Následující příklad kódu volá `ImportTypeMapping` metodu `SoapReflectionImporter` třídy pro vytvoření `XmlTypeMapping` .  
  
    ```vb  
    ' Serializes a class named Group as a SOAP message.  
    Dim myTypeMapping As XmlTypeMapping =
        New SoapReflectionImporter().ImportTypeMapping(GetType(Group))  
    ```  
  
    ```csharp  
    // Serializes a class named Group as a SOAP message.  
    XmlTypeMapping myTypeMapping =
        new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
    ```  
  
4. Vytvořit instanci `XmlSerializer` třídy předáním `XmlTypeMapping` k <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Xml.Serialization.XmlTypeMapping%29> konstruktor.  
  
    ```vb  
    Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
    ```  
  
    ```csharp  
    XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
    ```  
  
5. Volání `Serialize` nebo `Deserialize` metody.  
  
## <a name="example"></a>Příklad  
  
```vb  
' Serializes a class named Group as a SOAP message.  
Dim myTypeMapping As XmlTypeMapping =
    New SoapReflectionImporter().ImportTypeMapping(GetType(Group))
Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
```  
  
```csharp  
// Serializes a class named Group as a SOAP message.  
XmlTypeMapping myTypeMapping =
    new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
```  
  
## <a name="see-also"></a>Viz také

- [Serializace XML a SOAP](xml-and-soap-serialization.md)
- [Atributy, které řídí kódovanou serializaci SOAP](attributes-that-control-encoded-soap-serialization.md)
- [Serializace XML s webovými službami XML](xml-serialization-with-xml-web-services.md)
- [Postupy: Serializace objektu](how-to-serialize-an-object.md)
- [Postupy: Deserializace objektu](how-to-deserialize-an-object.md)
- [Postupy: Přepsání serializace XML zakódované v protokolu SOAP](how-to-override-encoded-soap-xml-serialization.md)

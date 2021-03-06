---
title: Ukázka DataContractJsonSerializer
ms.date: 03/30/2017
ms.assetid: 3c2c4747-7510-4bdf-b4fe-64f98428ef4a
ms.openlocfilehash: 4aa0ee679ae424251000b14abfbacf0590a6ccd3
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2020
ms.locfileid: "84592018"
---
# <a name="datacontractjsonserializer-sample"></a>Ukázka DataContractJsonSerializer

> [!NOTE]
> Tato ukázka je určena pro <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> . Pro většinu scénářů, které zahrnují serializaci a deserializaci JSON, doporučujeme rozhraní API v [oboru názvů System. text. JSON](../../../standard/serialization/system-text-json-overview.md).

<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>podporuje stejné typy jako <xref:System.Runtime.Serialization.DataContractSerializer> . Formát dat JSON je zvláště užitečný při psaní asynchronních webových aplikací ve stylu JavaScript a XML (AJAX). Podpora AJAX v Windows Communication Foundation (WCF) je optimalizována pro použití s ASP.NET AJAX prostřednictvím ovládacího prvku ScriptManager. Příklady použití Windows Communication Foundation (WCF) s ASP.NET AJAX naleznete v [ukázkách AJAX](ajax.md).  
  
Postup nastavení a pokyny pro sestavení pro tuto ukázku najdete na konci tohoto tématu.  
  
Ukázka používá `Person` kontrakt dat k demonstraci serializace a deserializace.  

```csharp
[DataContract]
class Person
{
    [DataMember]
    internal string name;

    [DataMember]
    internal int age;
}
```

 Chcete-li serializovat instanci `Person` typu na JSON, vytvořte <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> první a použijte `WriteObject` metodu pro zápis dat JSON do datového proudu.  

```csharp
Person p = new Person();
//Set up Person object...
MemoryStream stream1 = new MemoryStream();
DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(Person));
ser.WriteObject(stream1, p);
```

 Proud paměti obsahuje platná data JSON.
  
```json  
{"age":42,"name":"John"}  
```  
  
 Ukázka demonstruje deserializaci z dat JSON do objektu. Pak můžete Stream převinout zpět a zavolat `ReadObject` .  

```csharp
Person p2 = (Person)ser.ReadObject(stream1);
```

 Prozkoumáním `p2` objektu zjistíte, že data JSON byla deserializována správně.  
  
> [!IMPORTANT]
> Ukázky už můžou být na vašem počítači nainstalované. Než budete pokračovat, vyhledejte následující (výchozí) adresář.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Pokud tento adresář neexistuje, přečtěte si [ukázky Windows Communication Foundation (WCF) a programovací model Windows Workflow Foundation (WF) pro .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) ke stažení všech Windows Communication Foundation (WCF) a [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ukázek. Tato ukázka se nachází v následujícím adresáři.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Ajax\JsonSerialization`  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Nastavení, sestavení a spuštění ukázky  
  
1. Sestavte řešení JsonSerialization. sln, jak je popsáno v tématu [sestavování ukázek Windows Communication Foundation](building-the-samples.md).  
  
2. Spusťte výslednou konzolovou aplikaci.  

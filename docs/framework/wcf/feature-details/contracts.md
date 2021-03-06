---
title: Kontrakty
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], contracts
- contracts [WCF]
- Windows Communication Foundation [WCF], contracts
ms.assetid: c8364183-4ac1-480b-804a-c5e6c59a5d7d
ms.openlocfilehash: 1cd7e54d50e7116c71c040df1965674a4fdaff13
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595593"
---
# <a name="contracts"></a>Kontrakty
V této části se dozvíte, jak definovat a implementovat kontrakty Windows Communication Foundation (WCF). Kontrakt služby určuje, co koncový bod komunikuje s vnějším světem. Na přesnější úrovni je to prohlášení o sadě konkrétních zpráv uspořádaných do základních vzorů výměny zpráv (MEPs), jako je například požadavek/odpověď, jednosměrné a duplexní využití. Je-li kontrakt služby logicky spojenou sadou výměn zpráv, je operace služby jediným výměnou zpráv. Například `Hello` operace musí zjevně akceptovat jednu zprávu (takže volající může oznámení pozdravu) a může nebo nemusí vracet zprávu (v závislosti na příchodu operace).  
  
 Další informace o smlouvách a dalších základních konceptech WCF najdete v tématu [základní koncepty Windows Communication Foundation](../fundamental-concepts.md). Toto téma se zaměřuje na porozumění kontraktům služby. Další informace o tom, jak vytvořit klienty, kteří používají kontrakty služeb pro připojení ke službám, najdete v tématu [Přehled klientů WCF](../wcf-client-overview.md). Další informace o klientských kanálech, architektuře klientů a dalších problémech klienta najdete v tématu [klienti](clients.md).  
  
## <a name="overview"></a>Přehled  
 Toto téma obsahuje koncepční koncepční orientaci pro návrh a implementaci služeb WCF. Dílčí témata poskytují podrobnější informace o konkrétních tématech navrhování a implementace. Před návrhem a implementací aplikace WCF doporučujeme:  
  
- Seznamte se s principem kontraktu služby, jak funguje a jak ho vytvořit.  
  
- Seznamte se s minimálními požadavky na stav kontraktů, které konfigurace run-time nebo hostitelské prostředí nemusí podporovat.  
  
## <a name="service-contracts"></a>Kontrakty služeb  
 Kontrakt služby je příkaz, který poskytuje informace o:  
  
- Seskupení operací ve službě.  
  
- Signatura operací v podobě vyměňovaných zpráv.  
  
- Datové typy těchto zpráv.  
  
- Umístění operací.  
  
- Konkrétní protokoly a formáty serializace, které se používají k podpoře úspěšné komunikace se službou.  
  
 Například kontrakt nákupní objednávky může mít `CreateOrder` operaci, která přijímá vstupní typy informací o objednávkách a vrací informace o úspěchu nebo neúspěchu včetně identifikátoru objednávky. Může mít také `GetOrderStatus` operaci, která přijímá identifikátor objednávky a vrací informace o stavu objednávky. Kontrakt služby tohoto řazení by určoval:  
  
- Tato smlouva o nákupu se skládá z `CreateOrder` operací a `GetOrderStatus` .  
  
- Že operace mají zadané vstupní zprávy a výstupní zprávy.  
  
- Data, která tyto zprávy mohou přenášet.  
  
- Kategorií příkazy týkající se komunikační infrastruktury potřebné k úspěšnému zpracování zpráv. Mezi tyto podrobnosti patří například to, jestli a jaké jsou požadavky na zabezpečení, aby bylo možné navázat úspěšnou komunikaci.  
  
 Pokud chcete tento druh informací předat aplikacím na jiných platformách (včetně platforem jiných výrobců než Microsoftu), kontrakty služby XML se veřejně vyjadřují ve standardních formátech XML, jako je [WSDL (Web Services Description Language)](https://www.w3.org/TR/2001/NOTE-wsdl-20010315) a [schématu XML (XSD)](https://www.w3.org/XML/Schema), mimo jiné. Vývojáři pro spoustu platforem můžou tyto informace o veřejné smlouvě využít k vytváření aplikací, které můžou komunikovat se službou, protože rozumí jazyk specifikace a vzhledem k tomu, že tyto jazyky jsou navržené tak, aby umožňovaly vzájemné fungování, a popisují veřejné formuláře, formáty a protokoly, které služba podporuje. Další informace o tom, jak WCF zpracovává tento druh informací, najdete v tématu [metadata](metadata.md).  
  
 Kontrakty je možné vyjádřit mnoha způsoby, ale i když je WSDL a XSD Skvělé jazyky k tomu, aby je bylo možné snadno využít, jsou obtížné použít přímo – v každém případě se jedná o pouze popisy služby, nikoli implementace servisních smluv. Proto aplikace WCF používají spravované atributy, rozhraní a třídy k definování struktury a k implementaci služby.  
  
 Výsledný kontrakt definovaný ve spravovaných typech lze převést (označovaný také jako *exportovaný*) jako metadata – WSDL a XSD – v případě potřeby klienty nebo jiné implementátory služby, zejména na jiných platformách. Výsledkem je přímočarý programovací model, který lze popsat pomocí veřejných metadat pro jakoukoli klientskou aplikaci. Podrobnosti o podkladových zprávách SOAP, jako jsou informace o přenosech a zabezpečení, mohou být ponechány na WCF, což automaticky provádí nezbytné převody na systém typů servisních smluv a ze systému do systému typů XML.  
  
 Další informace o návrhu smluv najdete v tématu [Navrhování kontraktů služeb](../designing-service-contracts.md). Další informace o implementaci smluv najdete v tématu [implementace kontraktů služeb](../implementing-service-contracts.md).  
  
 Kromě toho WCF také umožňuje vyvíjet kontrakty služeb zcela na úrovni zprávy. Další informace o vývoji kontraktů služby na úrovni zpráv najdete v tématu [Použití kontraktů zpráv](using-message-contracts.md). Další informace o vývoji služeb v jiných než SOAP XML najdete v tématu [interoperabilita s aplikacemi POX](interoperability-with-pox-applications.md).  
  
### <a name="understanding-the-hierarchy-of-requirements"></a>Porozumění hierarchii požadavků  
 Servisní smlouva seskupuje operace. Určuje MEP, typy zpráv a datové typy, které tyto zprávy obsahují. a označuje kategorie chování modulu runtime, které musí implementace vyžadovat pro podporu kontraktu (například může vyžadovat, aby zprávy byly šifrované a podepsané). Servisní smlouva ale nespecifikuje přesně to, jak jsou tyto požadavky splněné, jenom to, že musí být. Typ šifrování nebo způsob, jakým je zpráva podepsána, je až do implementace a konfigurace kompatibilní služby.  
  
 Všimněte si, že smlouva vyžaduje určité věci implementace kontraktu služby a konfiguraci modulu runtime pro přidání chování. Sada požadavků, které je nutné splnit k vystavení služby pro použití sestavení na předchozí sadě požadavků. Pokud kontrakt provede požadavky na implementaci, implementace může vyžadovat ještě více konfigurací a vazeb, které umožňují spuštění služby. Nakonec musí hostitelská aplikace podporovat také všechny požadavky, které konfigurace služby a vazby přidávají.  
  
 Tento proces požadavku na doplňkovou látku je důležitý při navrhování, implementaci, konfiguraci a hostování aplikace služby Windows Communication Foundation (WCF). Kontrakt může například určit, že musí podporovat relaci. Pokud ano, musíte nakonfigurovat vazbu na podporu tohoto smluvního požadavku, jinak nebude implementace služby fungovat. Nebo pokud vaše služba vyžaduje integrované ověřování systému Windows a hostuje se ve službě Internetová informační služba (IIS), musí být webová aplikace, ve které je služba umístěná, zapnutá, zapnout integrované ověřování systému Windows a vypnout anonymní podporu. Další informace o funkcích a vlivu různých typů hostitelských aplikací služby najdete v tématu [hostování](hosting.md).  
  
## <a name="see-also"></a>Viz také

- [Koncové body: adresy, vazby a kontrakty](endpoints-addresses-bindings-and-contracts.md)
- [Navrhování kontraktů služby](../designing-service-contracts.md)
- [Implementace kontraktů služeb](../implementing-service-contracts.md)

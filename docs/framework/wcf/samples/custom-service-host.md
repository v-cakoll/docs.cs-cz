---
title: Vlastní hostitel služby
ms.date: 03/30/2017
ms.assetid: fe16ff50-7156-4499-9c32-13d8a79dc100
ms.openlocfilehash: 8302c3c829883da954d200526ca641eb4c169f98
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052023"
---
# <a name="custom-service-host"></a>Vlastní hostitel služby
Tato ukázka předvádí, jak použít vlastní derivát <xref:System.ServiceModel.ServiceHost> třídy pro změnu chování služby za běhu. Tento přístup poskytuje opakovaně použitelnou alternativu ke konfiguraci velkého počtu služeb běžným způsobem. Ukázka také ukazuje, jak použít <xref:System.ServiceModel.Activation.ServiceHostFactory> třídu pro použití vlastní třídy ServiceHost ve službě Internetová informační služba (IIS) nebo v hostitelském prostředí služby WAS (Windows Process Activation Service).  
  
> [!IMPORTANT]
> Ukázky už můžou být na vašem počítači nainstalované. Než budete pokračovat, vyhledejte následující (výchozí) adresář.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Pokud tento adresář neexistuje, přečtěte si [ukázky Windows Communication Foundation (WCF) a programovací model Windows Workflow Foundation (WF) pro .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) ke stažení všech Windows Communication Foundation (WCF) a [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ukázek. Tato ukázka se nachází v následujícím adresáři.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Hosting\CustomServiceHost`  
  
## <a name="about-the-scenario"></a>O scénáři
 Aby nedocházelo k neúmyslnému zveřejnění potenciálně citlivých metadat služby, služba výchozí konfigurace služby Windows Communication Foundation (WCF) zakáže publikování metadat. Ve výchozím nastavení je toto chování zabezpečené, ale také znamená, že nemůžete použít nástroj pro import metadat (například Svcutil.exe) k vygenerování kódu klienta, který je vyžadován pro volání služby, pokud není chování publikování metadat služby explicitně povoleno v konfiguraci.  
  
 Povolení publikování metadat pro velký počet služeb zahrnuje přidání stejných konfiguračních prvků do každé jednotlivé služby, což má za následek velké množství informací o konfiguraci, které jsou v podstatě stejné. Jako alternativu ke konfiguraci jednotlivých služeb je možné napsat imperativní kód, který umožňuje publikování metadat jednou a potom tento kód znovu použít napříč několika různými službami. To je dosaženo vytvořením nové třídy, která je odvozena z <xref:System.ServiceModel.ServiceHost> a Přepisuje `ApplyConfiguration` metodu () pro imperativní přidání chování publikování metadat.  
  
> [!IMPORTANT]
> Pro přehlednost Tato ukázka ukazuje, jak vytvořit nezabezpečený koncový bod publikování metadat. Tyto koncové body jsou možná dostupné anonymním neověřeným příjemcům a před nasazením těchto koncových bodů je nutné zajistit, aby bylo zajištěno, že bude jejich veřejněné zveřejnění metadat služby vhodné.  
  
## <a name="implementing-a-custom-servicehost"></a>Implementace vlastní třídy ServiceHost
 <xref:System.ServiceModel.ServiceHost>Třída zveřejňuje několik užitečných virtuálních metod, které mohou dědit pro změnu chování služby za běhu. Například `ApplyConfiguration` metoda () čte informace o konfiguraci služby z úložiště konfigurace a mění hostitele <xref:System.ServiceModel.Description.ServiceDescription> odpovídajícím způsobem. Výchozí implementace čte konfiguraci z konfiguračního souboru aplikace. Vlastní implementace mohou přepsat `ApplyConfiguration` () pro další změnu <xref:System.ServiceModel.Description.ServiceDescription> pomocí imperativního kódu nebo dokonce nahradit výchozí úložiště konfigurace. Například pro čtení konfigurace koncového bodu služby z databáze místo konfiguračního souboru aplikace.  
  
 V této ukázce chceme vytvořit vlastní třídu ServiceHost, která přidá rozhraní ServiceMetadataBehavior (umožňující publikování metadat) i v případě, že toto chování není explicitně přidáno do konfiguračního souboru služby. K tomu je potřeba vytvořit novou třídu, která dědí z <xref:System.ServiceModel.ServiceHost> a Overrides `ApplyConfiguration` ().  
  
```csharp
class SelfDescribingServiceHost : ServiceHost  
{  
    public SelfDescribingServiceHost(Type serviceType, params Uri[] baseAddresses)  
        : base(serviceType, baseAddresses) { }  
  
    //Overriding ApplyConfiguration() allows us to
    //alter the ServiceDescription prior to opening  
    //the service host.
    protected override void ApplyConfiguration()  
    {  
        //First, we call base.ApplyConfiguration()  
        //to read any configuration that was provided for  
        //the service we're hosting. After this call,  
        //this.Description describes the service  
        //as it was configured.  
        base.ApplyConfiguration();
  
        //(rest of implementation elided for clarity)  
    }  
}  
```  
  
 Vzhledem k tomu, že nechcete ignorovat žádnou konfiguraci, která byla k dispozici v konfiguračním souboru aplikace, první věc `ApplyConfiguration` () je volání základní implementace. Po dokončení této metody můžeme imperativně přidat <xref:System.ServiceModel.Description.ServiceMetadataBehavior> k popisu pomocí následujícího imperativního kódu.  
  
```csharp
ServiceMetadataBehavior mexBehavior = this.Description.Behaviors.Find<ServiceMetadataBehavior>();  
if (mexBehavior == null)  
{  
    mexBehavior = new ServiceMetadataBehavior();  
    this.Description.Behaviors.Add(mexBehavior);  
}  
else  
{  
    //Metadata behavior has already been configured,
    //so we do not have any work to do.  
    return;  
}  
```  
  
 Poslední věc, kterou je `ApplyConfiguration` třeba přepsat, je nutné přidat výchozí koncový bod metadat. Podle konvence je pro každý identifikátor URI v kolekci adres BaseAddresses hostitele služby vytvořen jeden koncový bod metadat.  
  
```csharp
//Add a metadata endpoint at each base address  
//using the "/mex" addressing convention  
foreach (Uri baseAddress in this.BaseAddresses)  
{  
    if (baseAddress.Scheme == Uri.UriSchemeHttp)  
    {  
        mexBehavior.HttpGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeHttps)  
    {  
        mexBehavior.HttpsGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpsBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetPipe)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexNamedPipeBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetTcp)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexTcpBinding(),  
                                "mex");  
    }  
}  
```  
  
## <a name="using-a-custom-servicehost-in-self-host"></a>Použití vlastní ServiceHost v samoobslužném hostování  
 Teď, když jsme dokončili naši vlastní implementaci ServiceHost, ji můžeme použít k přidání chování publikování metadat do jakékoli služby hostováním této služby uvnitř instance našeho `SelfDescribingServiceHost` . Následující kód ukazuje, jak ho použít ve scénáři samostatného hostitele.  
  
```csharp
SelfDescribingServiceHost host =
         new SelfDescribingServiceHost( typeof( Calculator ) );  
host.Open();  
```  
  
 Náš vlastní hostitel pořád čte konfiguraci koncového bodu služby z konfiguračního souboru aplikace, jako kdyby jsme používali výchozí <xref:System.ServiceModel.ServiceHost> třídu pro hostování služby. Vzhledem k tomu, že jsme přidali logiku pro povolení publikování metadat v rámci našeho vlastního hostitele, už nemusíte explicitně povolit chování publikování metadat v konfiguraci. Tento přístup má odlišnou výhodu při vytváření aplikace, která obsahuje několik služeb a chcete povolit publikování metadat na každém z nich, aniž byste museli psát stejné konfigurační prvky.  
  
## <a name="using-a-custom-servicehost-in-iis-or-was"></a>Použití vlastního hostitele ServiceHost ve službě IIS nebo WAS  
 Použití vlastního hostitele služby ve scénářích pro vlastní hostitele je jednoduché, protože se jedná o kód vaší aplikace, který je nakonec zodpovědný za vytvoření a otevření instance hostitele služby. Ve službě IIS nebo se hostující prostředí ale infrastruktura WCF dynamicky vytvoří instanci hostitele vaší služby v reakci na příchozí zprávy. Vlastní hostitelé služby můžete také použít v tomto hostitelském prostředí, ale vyžadují nějaký další kód ve formě ServiceHostFactory. Následující kód ukazuje derivaci <xref:System.ServiceModel.Activation.ServiceHostFactory> , který vrací instance našeho vlastního `SelfDescribingServiceHost` .  
  
```csharp
public class SelfDescribingServiceHostFactory : ServiceHostFactory  
{  
    protected override ServiceHost CreateServiceHost(Type serviceType,
     Uri[] baseAddresses)  
    {  
        //All the custom factory does is return a new instance  
        //of our custom host class. The bulk of the custom logic should  
        //live in the custom host (as opposed to the factory)
        //for maximum  
        //reuse value outside of the IIS/WAS hosting environment.  
        return new SelfDescribingServiceHost(serviceType,
                                             baseAddresses);  
    }  
}  
```  
  
 Jak vidíte, implementace vlastního ServiceHostFactory je jednoduchá. Všechny vlastní logiky se nacházejí v implementaci ServiceHost. objekt pro vytváření vrací instanci odvozené třídy.  
  
 Aby bylo možné používat vlastní továrnu s implementací služby, je nutné do souboru. svc služby přidat další metadata.  
  
```aspx-csharp
<% @ServiceHost Service="Microsoft.ServiceModel.Samples.CalculatorService"
               Factory="Microsoft.ServiceModel.Samples.SelfDescribingServiceHostFactory"
               language=c# Debug="true" %>
```
  
 Do direktivy jsme přidali dodatečný `Factory` atribut `@ServiceHost` a jako hodnotu atributu jste předali název typu CLR naší vlastní továrny. Když služba IIS nebo obdržela zprávu pro tuto službu, hostitelská infrastruktura WCF nejprve vytvoří instanci třídy ServiceHostFactory a potom sama inicializuje hostitele služby voláním `ServiceHostFactory.CreateServiceHost()` .  
  
## <a name="running-the-sample"></a>Spuštění ukázky  
 I když tato ukázka poskytuje plně funkční implementaci klienta a služby, bod ukázky je Ukázat, jak změnit chování služby za běhu pomocí vlastního hostitele. proveďte následující kroky:  
  
### <a name="observe-the-effect-of-the-custom-host"></a>Sledování účinku vlastního hostitele
  
1. Otevřete soubor Web.config služby a sledujte, že není k dispozici žádná konfigurace, která by explicitně povolila metadata služby.  
  
2. Otevřete soubor služby. svc a sledujte, že jeho @ServiceHost Direktiva obsahuje atribut Factory, který určuje název vlastní ServiceHostFactory.  
  
### <a name="set-up-build-and-run-the-sample"></a>Nastavení, sestavení a spuštění ukázky
  
1. Ujistěte se, že jste provedli [postup jednorázového nastavení pro Windows Communication Foundation ukázky](one-time-setup-procedure-for-the-wcf-samples.md).

2. Při sestavování řešení postupujte podle pokynů v tématu [sestavování ukázek Windows Communication Foundation](building-the-samples.md).

3. Po vytvoření řešení spusťte Setup.bat a nastavte aplikaci ServiceModelSamples ve službě IIS 7,0. Adresář ServiceModelSamples by se teď měl zobrazit jako aplikace IIS 7,0.

4. Chcete-li spustit ukázku v konfiguraci s jedním nebo více počítači, postupujte podle pokynů v části [spuštění ukázek Windows Communication Foundation](running-the-samples.md).

5. Pokud chcete odebrat aplikaci IIS 7,0, spusťte *Cleanup.bat*.

## <a name="see-also"></a>Viz také

- [Postupy: Hostování služby WCF v IIS](../feature-details/how-to-host-a-wcf-service-in-iis.md)

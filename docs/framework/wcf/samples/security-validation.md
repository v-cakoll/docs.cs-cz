---
title: Ověřování zabezpečení
ms.date: 03/30/2017
ms.assetid: 48dcd496-0c4f-48ce-8b9b-0e25b77ffa58
ms.openlocfilehash: 70408976469b1cbcf9c4679bd91d81872ec74ae1
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599968"
---
# <a name="security-validation"></a>Ověření zabezpečení
Tato ukázka předvádí, jak pomocí vlastního chování ověřit služby na počítači, abyste měli jistotu, že splňují určitá kritéria. V této ukázce se služby ověřují pomocí vlastního chování tím, že prochází každý koncový bod ve službě a kontroluje, jestli obsahují zabezpečené prvky vazby. Tato ukázka je založena na [Začínáme](getting-started-sample.md).  
  
> [!NOTE]
> Postup nastavení a pokyny pro sestavení pro tuto ukázku najdete na konci tohoto tématu.  
  
## <a name="endpoint-validation-custom-behavior"></a>Vlastní chování ověřování koncového bodu  
 Přidáním uživatelského kódu do `Validate` metody obsažené v <xref:System.ServiceModel.Description.IServiceBehavior> rozhraní může být vlastní chování uděleno službě nebo koncovému bodu pro provádění uživatelem definovaných akcí. Následující kód se používá k procyklení každého koncového bodu obsaženého ve službě, který vyhledává v rámci svých vazeb vazby pro zabezpečené vazby.  
  
```csharp
public void Validate(ServiceDescription serviceDescription,
                                       ServiceHostBase serviceHostBase)  
{  
    // Loop through each endpoint individually, gathering their
    // binding elements.  
    foreach (ServiceEndpoint endpoint in serviceDescription.Endpoints)  
    {  
        secureElementFound = false;  
  
        // Retrieve the endpoint's binding element collection.  
        BindingElementCollection bindingElements =
            endpoint.Binding.CreateBindingElements();  
  
        // Look to see if the binding elements collection contains any
        // secure binding elements. Transport, Asymmetric, and Symmetric
        // binding elements are all derived from SecurityBindingElement.  
        if ((bindingElements.Find<SecurityBindingElement>() != null) || (bindingElements.Find<HttpsTransportBindingElement>() != null) || (bindingElements.Find<WindowsStreamSecurityBindingElement>() != null) || (bindingElements.Find<SslStreamSecurityBindingElement>() != null))  
        {  
            secureElementFound = true;  
        }  
  
    // Send a message to the system event viewer when an endpoint is deemed insecure.  
    if (!secureElementFound)  
        throw new Exception(System.DateTime.Now.ToString() + ": The endpoint \"" + endpoint.Name + "\" has no secure bindings.");  
    }  
}  
```  
  
 Přidáním následujícího kódu do souboru Web. config přidáte `serviceValidate` rozšíření chování služby, které chcete rozpoznat.  
  
```xml  
<system.serviceModel>  
    <extensions>  
        <behaviorExtensions>  
            <add name="endpointValidate" type="Microsoft.ServiceModel.Samples.EndpointValidateElement, endpointValidate, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null" />  
        </behaviorExtensions>  
    </extensions>
    ...
</system.serviceModel>
```  
  
 Jakmile je rozšíření chování přidáno ke službě, je nyní možné přidat `endpointValidate` chování do seznamu chování v souboru Web. config a tedy do služby.  
  
```xml  
<behaviors>  
    <serviceBehaviors>  
        <behavior name="CalcServiceSEB1">  
            <serviceMetadata httpGetEnabled="true" />  
            <endpointValidate />  
        </behavior>  
    </serviceBehaviors>  
</behaviors>  
```  
  
 Chování a jejich rozšíření, která jsou přidána do souboru Web. config, aplikují chování na jednotlivé služby, zatímco když přidáte do souboru Machine. config, použije se chování pro všechny aktivní služby v počítači.  
  
> [!NOTE]
> Při přidávání chování do všech služeb je navrženo zálohování souboru Machine. config před provedením jakékoli změny.  
  
 Nyní spusťte klienta, který je k dispozici v adresáři client\bin této ukázky. Byla vyvolána výjimka s následující zprávou: "požadovanou službu http://localhost/servicemodelsamples/service.svc nelze aktivovat". To se očekává, protože koncový bod se považuje za nezabezpečený pomocí chování při ověřování koncového bodu a zabrání spuštění služby. Chování také vyvolá interní výjimku, která popisuje, který koncový bod je nezabezpečený a zapisuje do systému zprávu Prohlížeč událostí pod zdrojem "System. ServiceModel 4.0.0.0" a "webhost" kategorie. V této ukázce je také možné zapnout trasování pro službu. To uživateli umožňuje zobrazit výjimky vyvolané chováním ověřování koncového bodu otevřením výsledných trasování služby pomocí nástroje Service Trace Viewer.  
  
### <a name="view-failed-endpoint-validation-exception-messages-in-the-event-viewer"></a>Zobrazit zprávy výjimky ověření neúspěšných koncových bodů v Prohlížeč událostí  
  
1. Klikněte na nabídku **Start** a vyberte možnost **Spustit...**.  
  
2. Zadejte `eventvwr` a klikněte na **OK**.  
  
3. V okně Prohlížeč událostí klikněte na možnost **aplikace**.  
  
4. Poklikejte na nedávno přidanou událost System. ServiceModel 4.0.0.0 do kategorie webhost v okně **aplikace** a zobrazte nezabezpečené zprávy koncového bodu.  
  
## <a name="set-up-build-and-run-the-sample"></a>Nastavení, sestavení a spuštění ukázky  
  
1. Ujistěte se, že jste provedli [postup jednorázového nastavení pro Windows Communication Foundation ukázky](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Chcete-li sestavit edici C# nebo Visual Basic .NET, postupujte podle pokynů v tématu [sestavování ukázek Windows Communication Foundation](building-the-samples.md).  
  
3. Chcete-li spustit ukázku v konfiguraci s jedním nebo více počítači, postupujte podle pokynů v části [spuštění ukázek Windows Communication Foundation](running-the-samples.md).  
  
> [!IMPORTANT]
> Ukázky již mohou být nainstalovány v počítači. Než budete pokračovat, vyhledejte následující (výchozí) adresář.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Pokud tento adresář neexistuje, přečtěte si [ukázky Windows Communication Foundation (WCF) a programovací model Windows Workflow Foundation (WF) pro .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) ke stažení všech Windows Communication Foundation (WCF) a [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ukázek. Tato ukázka se nachází v následujícím adresáři.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ServiceValidation`  
  
## <a name="see-also"></a>Viz také

- [Ukázky monitorování technologie AppFabric](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))

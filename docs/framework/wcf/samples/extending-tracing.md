---
title: Rozšíření trasování
ms.date: 03/30/2017
ms.assetid: 2b971a99-16ec-4949-ad2e-b0c8731a873f
ms.openlocfilehash: 59bdfeea41bac812840ffe166895050a6cd1ad2d
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600513"
---
# <a name="extend-tracing"></a>Rozšiřování trasování

Tato ukázka demonstruje, jak lze rozšířenou funkci trasování Windows Communication Foundation (WCF) pomocí zápisu uživatelsky definovaných trasování aktivit v kódu klienta a služby. Zápis uživatelsky definovaných trasování aktivit umožňuje uživateli vytvářet aktivity trasování a seskupovat trasování do logických jednotek práce. Je také možné korelovat aktivity prostřednictvím přenosů (v rámci stejného koncového bodu) a šíření (mezi koncovými body). V této ukázce je povoleno trasování pro klienta i službu. Další informace o tom, jak povolit trasování v konfiguračních souborech klienta a služby, najdete v tématu [trasování a protokolování zpráv](tracing-and-message-logging.md).  
  
 Tato ukázka je založena na [Začínáme](getting-started-sample.md).  
  
> [!NOTE]
> Postup nastavení a pokyny pro sestavení pro tuto ukázku najdete na konci tohoto tématu.  
  
> [!IMPORTANT]
> Ukázky již mohou být nainstalovány v počítači. Než budete pokračovat, vyhledejte následující (výchozí) adresář.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Pokud tento adresář neexistuje, přečtěte si [ukázky Windows Communication Foundation (WCF) a programovací model Windows Workflow Foundation (WF) pro .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) ke stažení všech Windows Communication Foundation (WCF) a [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ukázek. Tato ukázka se nachází v následujícím adresáři.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ExtendingTracing`  
  
## <a name="tracing-and-activity-propagation"></a>Trasování a šíření aktivit  
 Uživatelsky definované trasování aktivit umožňuje uživateli vytvořit vlastní aktivity trasování pro seskupení trasování do logických pracovních jednotek, sladit aktivity prostřednictvím přenosů a šíření a snížit náklady na výkon trasování WCF (například náklady na místo na disku v souboru protokolu).  
  
### <a name="add-custom-sources"></a>Přidat vlastní zdroje  
 Uživatelsky definované trasování lze přidat do kódu klienta i služby. Přidání zdrojů trasování do konfiguračních souborů klienta nebo služby umožňuje zaznamenávat a zobrazovat tato vlastní trasování v [nástroji pro prohlížeč trasování služby (SvcTraceViewer. exe)](../service-trace-viewer-tool-svctraceviewer-exe.md). Následující kód ukazuje, jak přidat zdroj trasování definovaný uživatelem s názvem `ServerCalculatorTraceSource` do konfiguračního souboru.  
  
```xml  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
        <source name="ServerCalculatorTraceSource" switchValue="Information,ActivityTracing">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
       <add initializeData="C:\logs\ServerTraces.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" traceOutputOptions="Callstack">  
            <filter type="" />  
        </add>  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>
....
```  
  
### <a name="correlate-activities"></a>Korelace aktivit  
 Aby bylo možné korelovat aktivity přímo napříč koncovými body, `propagateActivity` musí být atribut nastaven na hodnotu `true` ve `System.ServiceModel` zdroji trasování. Aby bylo možné rozšířit trasování bez průchodu aktivitami WCF, musí být trasování aktivity ServiceModel vypnuto. To lze vidět v následujícím příkladu kódu.  
  
> [!NOTE]
> Vypnutí trasování aktivity ServiceModel není stejné jako úroveň trasování, která je označena `switchValue` vlastností, nastavena na hodnotu OFF.  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
  
    ...  
  
       </source>  
    </sources>  
</system.diagnostics>  
```  
  
### <a name="lessen-performance-cost"></a>Snížit náklady na výkon  
 Nastavením `ActivityTracing` na hodnotu Vypnuto ve `System.ServiceModel` zdroji trasování dojde k vygenerování trasovacího souboru, který obsahuje pouze trasování aktivity definované uživatelem, aniž by bylo zahrnuto trasování aktivity ServiceModel. Vyloučení trasování aktivit ServiceModel má za následek mnohem menší soubor protokolu. Je však ztracena možnost korelace trasování zpracování WCF.  
  
## <a name="set-up-build-and-run-the-sample"></a>Nastavení, sestavení a spuštění ukázky  
  
1. Ujistěte se, že jste provedli [postup jednorázového nastavení pro Windows Communication Foundation ukázky](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Chcete-li sestavit edici C# nebo Visual Basic .NET, postupujte podle pokynů v tématu [sestavování ukázek Windows Communication Foundation](building-the-samples.md).  
  
3. Chcete-li spustit ukázku v konfiguraci s jedním nebo více počítači, postupujte podle pokynů v části [spuštění ukázek Windows Communication Foundation](running-the-samples.md).  
  
## <a name="see-also"></a>Viz také

- [Ukázky monitorování technologie AppFabric](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))

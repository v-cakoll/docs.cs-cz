---
title: <basicHttpContextBinding>
ms.date: 03/30/2017
ms.assetid: 39b16b82-4ec6-4eff-8031-67e026870961
ms.openlocfilehash: 78372970c7dc0f5a29e7fc9fdfc80aa443107b6d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2020
ms.locfileid: "84201166"
---
# \<basicHttpContextBinding>
Zadáním vazby, která poskytuje kontext pro <xref:System.ServiceModel.BasicHttpBinding> vyměňování, povolením souborů cookie protokolu HTTP jako mechanismu výměny.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<basicHttpContextBinding>**  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<basicHttpContextBinding>
  <binding allowCookies="Boolean"
           bypassProxyOnLocal="Boolean"
           closeTimeout="TimeSpan"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           maxBufferPoolSize="Integer"
           maxBufferSize="Integer"
           maxReceivedMessageSize="Integer"
           messageEncoding="Text/Mtom"
           name="String"
           openTimeout="TimeSpan"
           proxyAddress="URI"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
           useDefaultWebProxy="Boolean">
    <security mode="None/Transport/Message/TransportWithMessageCredential/TransportCredentialOnly">
      <transport clientCredentialType="None/Basic/Digest/Ntlm/Windows/Certificate"
                 proxyCredentialType="None/Basic/Digest/Ntlm/Windows"
                 realm="String" />
      <message algorithmSuite="Aes128/Aes192/Aes256/Rsa15Aes128/ Rsa15Aes256/TripleDes"
               clientCredentialType="UserName/Certificate" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</basicHttpContextBinding>
```  
  
## <a name="attributes-and-elements"></a>Atributy a elementy  
 Následující části popisují atributy, podřízené prvky a nadřazené prvky.  
  
### <a name="attributes"></a>Atributy  
  
|Atribut|Popis|  
|---------------|-----------------|  
|`allowCookies`|Logická hodnota určující, zda klient přijímá soubory cookie a šíří je v budoucích požadavcích. Výchozí formát je `false`.<br /><br /> Tuto vlastnost lze použít při práci s webovými službami ASMX, které používají soubory cookie. Tímto způsobem si můžete ověřit, že soubory cookie vrácené ze serveru se automaticky zkopírují do všech budoucích požadavků klientů pro danou službu.|  
|`bypassProxyOnLocal`|Logická hodnota, která označuje, zda se má pro místní adresy obejít proxy server. Výchozí formát je `false`.<br /><br /> Internetový prostředek je místní, pokud má místní adresu. Místní adresa je jedna, která je ve stejném počítači, v místní síti LAN nebo intranetu a je označena syntakticky nedostatečným obdobím (.) jako v identifikátorech URI `http://webserver/` a `http://localhost/` .<br /><br /> Nastavením tohoto atributu určíte, zda jsou koncové body nakonfigurované pomocí BasicHttpBinding používány při přístupu k místním prostředkům proxy server. Pokud je tento atribut `true` , požadavky na místní prostředky sítě Internet nepoužívají proxy server. Použijte název hostitele (nikoli localhost), pokud chcete, aby klienti procházeli prostřednictvím proxy serveru při komunikaci se službami ve stejném počítači, na kterém je tento atribut nastavený `true` .<br /><br /> Pokud je tento atribut `false` , všechny požadavky na Internet se provádí prostřednictvím proxy server.|  
|`closeTimeout`|<xref:System.TimeSpan>Hodnota, která určuje časový interval poskytnutý pro dokončení operace uzavření. Tato hodnota by měla být větší nebo rovna <xref:System.TimeSpan.Zero> . Výchozí hodnota je 00:01:00.|  
|`hostNameComparisonMode`|Určuje režim porovnání názvu hostitele HTTP, který se používá k analýze identifikátorů URI. Tento atribut je typu <xref:System.ServiceModel.HostNameComparisonMode> , který označuje, zda je název hostitele použit pro dosažení služby při shodě s identifikátorem URI. Výchozí hodnota je <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard> , která ignoruje název hostitele v shodě.|  
|`maxBufferPoolSize`|Celočíselná hodnota, která určuje maximální velikost paměti, která je přidělena pro použití správcem vyrovnávacích pamětí zpráv, které přijímají zprávy z kanálu. Výchozí hodnota je 524288 (0x80000) bajtů.<br /><br /> Správce vyrovnávací paměti minimalizuje náklady na používání vyrovnávacích pamětí pomocí fondu vyrovnávacích pamětí. Vyrovnávací paměti jsou požadovány ke zpracování zpráv, když se dostanou z kanálu. Pokud ve fondu vyrovnávací paměti není dostatek paměti pro zpracování zatížení zprávy, Správce vyrovnávací paměti musí přidělit další paměť z haldy CLR, což zvyšuje režii uvolňování paměti. Rozsáhlá alokace z haldy uvolňování CLR je indikace, že velikost fondu vyrovnávací paměti je příliš malá a výkon lze zlepšit větším přidělením zvýšením limitu určeného tímto atributem.|  
|`maxBufferSize`|Celočíselná hodnota, která určuje maximální velikost vyrovnávací paměti v bajtech, která ukládá zprávy, když jsou zpracovávány pro koncový bod nakonfigurovaný pomocí této vazby. Výchozí hodnota je 65 536 bajtů.|  
|`maxReceivedMessageSize`|Kladné celé číslo, které definuje maximální velikost zprávy v bajtech, včetně hlaviček, pro zprávu, která se dá přijmout na kanálu nakonfigurovaném pomocí této vazby. Odesilatel obdrží chybu protokolu SOAP, pokud je zpráva pro příjemce příliš velká. Příjemce zprávu zruší a vytvoří záznam události v protokolu trasování. Výchozí hodnota je 65 536 bajtů.|  
|`messageEncoding`|Definuje kodér použitý ke kódování zprávy SOAP. Platné hodnoty jsou následující:<br /><br /> -Text: Použijte kodér textové zprávy.<br />-MTOM: Použijte kodér 1,0 (Message Transmission Organization mechanism).<br /><br /> Výchozí hodnota je text. Tento atribut je typu <xref:System.ServiceModel.WSMessageEncoding> .|  
|`messageVersion`|Určuje verzi zprávy, kterou používají klienti a služby nakonfigurované s vazbou. Tento atribut je typu <xref:System.ServiceModel.Channels.MessageVersion> .|  
|`name`|Řetězec, který obsahuje název konfigurace vazby. Tato hodnota by měla být jedinečná, protože se používá jako identifikace vazby. Počínaje .NET Framework 4 nejsou vazby a chování nutné mít název. Další informace o výchozích konfiguracích a Nameless vazbách a chování najdete v tématu [zjednodušená konfigurace](../../../wcf/simplified-configuration.md) a [zjednodušená konfigurace pro služby WCF](../../../wcf/samples/simplified-configuration-for-wcf-services.md).|  
|`openTimeout`|<xref:System.TimeSpan>Hodnota, která určuje časový interval poskytnutý pro dokončení operace otevření. Tato hodnota by měla být větší nebo rovna <xref:System.TimeSpan.Zero> . Výchozí hodnota je 00:01:00.|  
|`proxyAddress`|Identifikátor URI, který obsahuje adresu proxy serveru HTTP. Pokud `useSystemWebProxy` je parametr nastaven na hodnotu `true` , musí být toto nastavení `null` . Výchozí formát je `null`.|  
|`receiveTimeout`|<xref:System.TimeSpan>Hodnota, která určuje časový interval poskytnutý pro dokončení operace Receive. Tato hodnota by měla být větší nebo rovna <xref:System.TimeSpan.Zero> . Výchozí hodnota je 00:10:00.|  
|`sendTimeout`|<xref:System.TimeSpan>Hodnota, která určuje časový interval poskytnutý pro dokončení operace odeslání. Tato hodnota by měla být větší nebo rovna <xref:System.TimeSpan.Zero> . Výchozí hodnota je 00:01:00.|  
|`textEncoding`|Nastaví kódování znakové sady, které se má použít pro generování zpráv ve vazbě. Platné hodnoty jsou následující:<br /><br /> -BigEndianUnicode: kódování Unicode BigEndian.<br />-Unicode: 16 bitů kódování.<br />-UTF8:8bitové kódování<br /><br /> Výchozí hodnota je UTF8. Tento atribut je typu <xref:System.Text.Encoding> .|  
|`transferMode`|Platná <xref:System.ServiceModel.TransferMode> hodnota, která určuje, zda jsou zprávy ukládány do vyrovnávací paměti nebo zpracovány v žádosti nebo odpovědi.|  
|`useDefaultWebProxy`|Logická hodnota určující, zda má být k dispozici automaticky konfigurovaný proxy server HTTP systému, je-li k dispozici. Výchozí formát je `true`.|  
  
### <a name="child-elements"></a>Podřízené elementy  
  
|Prvek|Description|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|Definuje nastavení zabezpečení pro vazbu. Tento prvek je typu <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement> .|  
|[\<readerQuotas>](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|Definuje omezení složitosti zpráv SOAP, které mohou být zpracovány koncovými body nakonfigurovanými s touto vazbou. Tento prvek je typu <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement> .|  
  
### <a name="parent-elements"></a>Nadřazené elementy  
  
|Prvek|Description|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|Tento prvek obsahuje kolekci standardních a vlastních vazeb.|  
  
## <a name="remarks"></a>Poznámky  
 Tento prvek vazby poskytuje úroveň ochrany a mechanizmus výměny jako součást kontextu pro `BasicHttpBinding` .  
  
## <a name="see-also"></a>Viz také

- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.BasicHttpContextBinding>
- <xref:System.ServiceModel.Configuration.BasicHttpContextBindingElement>
- <xref:System.ServiceModel.Channels.ContextBindingElement>
- [Vazby](../../../wcf/bindings.md)
- [Konfigurace vazeb poskytovaných systémem](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Používání vazeb ke konfiguraci služeb a klientů](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
- [\<basicHttpBinding>](basichttpbinding.md)

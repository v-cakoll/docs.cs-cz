---
title: Technologie .NET Framework nedostupné v .NET Core
titleSuffix: ''
description: Přečtěte si o .NET Framework technologiích, které nejsou k dispozici v .NET Core
author: cartermp
ms.date: 04/30/2019
ms.openlocfilehash: b75d946b9436b1075a068494b941fbdea5970e42
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795596"
---
# <a name="net-framework-technologies-unavailable-on-net-core"></a>Technologie .NET Framework nedostupné v .NET Core

K dispozici je několik technologií .NET Frameworkch knihoven, které se nedají používat s .NET Core, jako jsou AppDomains, Vzdálená komunikace, zabezpečení přístupu kódu (CAS), transparentnost zabezpečení a System. EnterpriseServices. Pokud se vaše knihovny spoléhají na jednu nebo více těchto technologií, vezměte v úvahu alternativní přístupy uvedené níže. Další informace o kompatibilitě rozhraní API najdete v tématu zásadní [změny .NET Core](../compatibility/breaking-changes.md).

Vzhledem k tomu, že rozhraní API nebo technologie není aktuálně implementováno, neznamená, že je záměrně Nepodporovaná. Prohledejte úložiště GitHub pro .NET Core, abyste zjistili, jestli se k určitému problému setkáte podle návrhu. Pokud tento indikátor nenajdete, založte problém do [úložiště dotnet/runtime](https://github.com/dotnet/runtime/issues) a požádejte ho o konkrétní rozhraní API a technologie.

## <a name="appdomains"></a>Objektů třídy AppDomains

Aplikační domény (AppDomains) izolují aplikace od sebe navzájem. Třídy AppDomains vyžadují podporu modulu runtime a jsou všeobecně nákladné. Vytváření dalších aplikačních domén se nepodporuje a v budoucnu neexistují žádné plány pro přidání této možnosti. Pro izolaci kódu použijte jako alternativu samostatné procesy nebo kontejnery. K dynamickému načítání sestavení použijte <xref:System.Runtime.Loader.AssemblyLoadContext> třídu.

Aby mohla migrace kódu z .NET Framework snazší, rozhraní .NET Core zpřístupňuje některé <xref:System.AppDomain> z ploch rozhraní API. Některá z <xref:System.AppDomain.UnhandledException?displayProperty=nameWithType>funkcí rozhraní API obvykle (například), některé členy nedělají nic (například <xref:System.AppDomain.SetCachePath%2A>) a některé z nich vyvolají <xref:System.PlatformNotSupportedException> (například <xref:System.AppDomain.CreateDomain%2A>). Ověřte typy, které používáte, na [ `System.AppDomain` zdroj odkazů](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Private.CoreLib/src/System/AppDomain.cs) v [úložišti GitHub/runtime](https://github.com/dotnet/runtime). Ujistěte se, že jste vybrali větev, která odpovídá implementované verzi.

## <a name="remoting"></a>Vzdálenou

Vzdálená komunikace .NET byla označena jako problematická architektura. Používá se pro komunikaci mezi doménami, která už není podporovaná. Vzdálená komunikace také vyžaduje běhovou podporu, která je náročná na údržbu. Z těchto důvodů není vzdálená komunikace v .NET podporovaná pro .NET Core a v budoucnu neplánujeme přidat podporu pro IT.

Pro komunikaci mezi procesy zvažte jako alternativu ke vzdálené komunikaci mechanismy mezi procesy (IPC), jako je <xref:System.IO.Pipes> například třída nebo <xref:System.IO.MemoryMappedFiles.MemoryMappedFile> třída.

V různých počítačích použijte jako alternativu řešení založené na síti. Nejlépe použijte protokol s malým režijním textem, jako je například HTTP. [Webový server Kestrel](/aspnet/core/fundamentals/servers/kestrel), který používá ASP.NET Core, je zde možnost. Zvažte také použití <xref:System.Net.Sockets> ve scénářích pro více počítačů využívajících sítě. Další možnosti naleznete v tématu [vývojářské projekty Open Source aplikace .NET: zasílání zpráv](https://github.com/Microsoft/dotnet/blob/master/dotnet-developer-projects.md#messaging).

## <a name="code-access-security-cas"></a>Zabezpečení přístupu kódu (CAS)

Sandboxing, která spoléhá na modul runtime nebo na rozhraní k omezení prostředků, které spravovaná aplikace nebo knihovna používá nebo běží, se [na .NET Framework nepodporuje](../../framework/misc/code-access-security.md) , a proto se v .NET Core nepodporuje. V .NET Framework je příliš mnoho případů a modul runtime, kde se zvýšení oprávnění projeví i v případě, že se CAS považují za hranice zabezpečení. Kromě toho je implementace složitější a často má dopad na výkon aplikací, které ho nemají v úmyslu používat.

Pro spouštění procesů s minimální sadou oprávnění používejte hranice zabezpečení poskytované operačním systémem, jako je virtualizace, kontejnery nebo uživatelské účty.

## <a name="security-transparency"></a>Transparentnost zabezpečení

Podobně jako certifikační autorita, transparentnost zabezpečení odděluje kód v izolovaném prostoru z kódu kritického zabezpečení deklarativním způsobem, ale [již není podporována jako hranice zabezpečení](../../framework/misc/security-transparent-code.md). Tato funkce je silně využívána v Silverlightu.

Pro spouštění procesů s nejmenší sadou oprávnění používejte hranice zabezpečení poskytované operačním systémem, jako je virtualizace, kontejnery nebo uživatelské účty.

## <a name="systementerpriseservices"></a>System. EnterpriseServices

Rozhraní .NET Core nepodporuje System. EnterpriseServices (COM+).

## <a name="see-also"></a>Viz také

- [Přehled přenosů z .NET Framework do .NET Core](index.md)

---
title: Programování s doménami aplikací a sestaveními
description: Získejte informace o programování s aplikačními doménami a sestaveními v .NET. V tématu odkazy na témata s postupy & příklady vytváření aplikačních domén & sestaveních.
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], programming
- programming assemblies
- application domains, programming
- programming application domains
ms.assetid: 96d3b8e3-bef8-4da0-9a81-9841e23a94e9
ms.openlocfilehash: 1c28fe0abeb279a1dbbc6dcf043c1780c72d79df
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903435"
---
# <a name="programming-with-application-domains-and-assemblies"></a>Programování s doménami aplikací a sestaveními

Hostitelé, jako je Microsoft Internet Explorer, ASP.NET a prostředí Windows, načtou modul CLR (Common Language Runtime) do procesu, vytvoří v tomto procesu [doménu aplikace](application-domains.md) a při spuštění aplikace .NET Framework načte a spustí uživatelský kód v této doméně aplikace. Ve většině případů se nemusíte starat o vytváření domén aplikací a načítání sestavení do nich, protože hostitel modulu runtime provádí tyto úlohy.  
  
Pokud však vytváříte aplikaci, která bude hostovat modul CLR (Common Language Runtime), vytváříte nástroje nebo kód, který chcete uvolnit programově, nebo vytváříte zapojitelné součásti, které se dají uvolnit a znovu načíst, budete vytvářet vlastní aplikační domény. I v případě, že nevytváříte hostitele modulu runtime, Tato část poskytuje důležité informace o tom, jak pracovat s doménami aplikací a sestaveními načtenými v těchto doménách aplikace.  
  
## <a name="in-this-section"></a>V tomto oddílu  

[Témata s návody k doménám a sestavením aplikací](application-domains-and-assemblies-how-to-topics.md)  
Obsahuje odkazy na všechna témata s postupy, která najdete v Koncepční dokumentaci pro programování s doménami aplikací a sestaveními.  
  
[Používání domén aplikací](use.md)  
V této části najdete příklady vytváření, konfigurace a používání domén aplikací.  
  
[Programování se sestaveními](../../standard/assembly/index.md)  
Popisuje způsob vytváření, podepisování a nastavení atributů v rámci sestavení.  
  
## <a name="related-sections"></a>Související oddíly  

[Generování dynamických metod a sestavení](../reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)  
Popisuje způsob vytváření dynamických sestavení.  
  
[Sestavení v .NET](../../standard/assembly/index.md)  
Poskytuje koncepční přehled sestavení.  
  
[Aplikační domény](application-domains.md)  
Poskytuje koncepční přehled domén aplikací.  
  
[Přehled reflexe](../reflection-and-codedom/reflection.md)  
Popisuje způsob použití třídy **reflexe** k získání informací o sestavení.

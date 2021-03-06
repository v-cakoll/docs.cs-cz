---
title: Poskytovatel Entity Framework (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: 650b5eb6-c71d-4dc1-8b64-b6beaf752114
ms.openlocfilehash: b6d49f20f72282ac2ce51c26fc4eb941b7ef6734
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75346099"
---
# <a name="entity-framework-provider-wcf-data-services"></a>Poskytovatel Entity Framework (WCF Data Services)
Podobně jako WCF Data Services je Entity Framework ADO.NET založen na model EDM (Entity Data Model), což je typ modelu vztahů mezi entitami. Entity Framework překládá operace proti implementaci model EDM (Entity Data Model), která se nazývá *koncepční model*, do ekvivalentních operací se zdrojem dat. Díky tomu Entity Framework ideálního poskytovatele pro datové služby, který je založený na relačních datech, a všechny databáze, které mají poskytovatele dat, který podporuje Entity Framework, lze použít s WCF Data Services. Seznam zdrojů dat, které aktuálně podporují Entity Framework, najdete v tématu [poskytovatelé Entity Framework](/ef/ef6/fundamentals/providers/).
  
 V koncepčním modelu je kontejner entit kořenem služby. V Entity Framework musíte definovat koncepční model, aby bylo možné data zpřístupnit datovou službou. Další informace najdete v tématu [Postupy: vytvoření datové služby pomocí Entity Framework zdroje dat v ADO.NET](create-a-data-service-using-an-adonet-ef-data-wcf.md).  
  
 WCF Data Services podporuje model souběžného souběžnosti tím, že umožňuje definovat Token souběžnosti pro entitu. Tento token souběžnosti, který obsahuje jednu nebo více vlastností entity, používá datová služba k určení, zda došlo ke změně v datech, která jsou požadována, aktualizována nebo odstraněna. Pokud se hodnoty tokenu získané z eTag v požadavku liší od aktuální hodnoty entity, vyvolá datová služba výjimku. Chcete-li určit, že vlastnost je součástí tokenu souběžnosti, je nutné použít atribut `ConcurrencyMode="Fixed"` v datovém modelu definovaném poskytovatelem Entity Framework. Token souběžnosti nemůže obsahovat vlastnost klíče ani navigační vlastnost. Další informace najdete v tématu [aktualizace datové služby](updating-the-data-service-wcf-data-services.md).  
  
 Další informace o Entity Framework najdete v tématu [Entity Framework Overview](../adonet/ef/overview.md).  
  
## <a name="see-also"></a>Viz také:

- [Zprostředkovatelé datových služeb](data-services-providers-wcf-data-services.md)
- [Zprostředkovatel reflexe](reflection-provider-wcf-data-services.md)
- [Model EDM (Entity Data Model)](../adonet/entity-data-model.md)

---
title: Identifikátory (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d58a5edd-7b5c-48e1-b5d7-a326ff426aa4
ms.openlocfilehash: b467a42ed0a0083b9e72037f437dd70aa6b46390
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833711"
---
# <a name="identifiers-entity-sql"></a>Identifikátory (Entity SQL)
Identifikátory se používají v [!INCLUDE[esql](../../../../../../includes/esql-md.md)] pro reprezentaci aliasů výrazů dotazů, odkazů na proměnné, vlastností objektů, funkcí a tak dále. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] poskytuje dva druhy identifikátorů: jednoduché identifikátory a identifikátory v uvozovkách.  
  
## <a name="simple-identifiers"></a>Jednoduché identifikátory  
 Jednoduchý identifikátor v [!INCLUDE[esql](../../../../../../includes/esql-md.md)] je sekvence alfanumerických a podtržítek znaků. První znak identifikátoru musí být abecední znak (a-z nebo A-Z).  
  
## <a name="quoted-identifiers"></a>Identifikátory v uvozovkách  
 Identifikátor v uvozovkách je libovolná sekvence znaků uzavřená v hranatých závorkách ([]). Identifikátory v uvozovkách umožňují zadat identifikátory se znaky, které nejsou platné v identifikátorech. Všechny znaky mezi hranatými závorkami se stanou součástí identifikátoru, včetně celého prázdného znaku.  
  
 Identifikátor v uvozovkách nesmí obsahovat tyto znaky:  
  
- Nového.  
  
- Znaky konce řádku.  
  
- Listy.  
  
- BACKSPACE.  
  
- Další hranaté závorky (tj. hranaté závorky v hranatých závorkách, které vymezují identifikátor).  
  
 Citovaný identifikátor může obsahovat znaky Unicode.  
  
 Identifikátory v uvozovkách umožňují vytvářet znaky názvů vlastností, které nejsou platné v identifikátorech, jak je znázorněno v následujícím příkladu:  
  
 `SELECT c.ContactName AS [Contact Name] FROM customers AS c`  
  
 Můžete také použít identifikátory v uvozovkách k určení identifikátoru, který je vyhrazeným klíčovým slovem [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Například pokud typ `Email` má vlastnost s názvem "z", můžete ji odstranit z klíčového slova vyhrazeného z pomocí hranatých závorek následujícím způsobem:  
  
 `SELECT e.[From] FROM emails AS e`  
  
 Můžete použít identifikátor v uvozovkách na pravé straně operátoru tečka (.).  
  
 `SELECT t FROM ts as t WHERE t.[property] == 2`  
  
 Chcete-li použít hranatou závorku v identifikátoru, přidejte další hranatou závorku. V následujícím příkladu "`abc]`" je identifikátor:  
  
 `SELECT t from ts as t WHERE t.[abc]]] == 2`  
  
 Sémantika porovnání identifikátorů v uvozovkách naleznete v tématu [vstupní znaková sada](input-character-set-entity-sql.md).  
  
## <a name="aliasing-rules"></a>Pravidla aliasování  
 V případě potřeby doporučujeme zadat aliasy v dotazech [!INCLUDE[esql](../../../../../../includes/esql-md.md)], včetně následujících konstrukcí [!INCLUDE[esql](../../../../../../includes/esql-md.md)]:  
  
- Pole konstruktoru řádku.  
  
- Položky v klauzuli FROM výrazu dotazu.  
  
- Položky v klauzuli SELECT výrazu dotazu.  
  
- Položky v klauzuli GROUP BY výrazu dotazu.  
  
### <a name="valid-aliases"></a>Platné aliasy  
 Platné aliasy v [!INCLUDE[esql](../../../../../../includes/esql-md.md)] jsou jakékoli jednoduché identifikátory nebo identifikátory v uvozovkách.  
  
### <a name="alias-generation"></a>Generování aliasů  
 Pokud ve výrazu dotazu [!INCLUDE[esql](../../../../../../includes/esql-md.md)] není zadaný žádný alias, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] se pokusí vygenerovat alias na základě následujících jednoduchých pravidel:  
  
- Pokud je výraz dotazu (pro který není zadán alias) jednoduchý nebo citovaný identifikátor, je tento identifikátor použit jako alias. Například `ROW(a, [b])` se zobrazí `ROW(a AS a, [b] AS [b])`.  
  
- Pokud je výraz dotazu složitější výraz, ale poslední součást tohoto výrazu dotazu je jednoduchý identifikátor, pak tento identifikátor je použit jako alias. Například `ROW(a.a1, b.[b1])` se zobrazí `ROW(a.a1 AS a1, b.[b1] AS [b1])`.  
  
 Pokud chcete použít název aliasu později, doporučujeme nepoužívat implicitní aliasing. V případě konfliktu s aliasy (implicitní nebo explicitní) nebo se opakuje ve stejném oboru, dojde k chybě kompilace. Implicitní alias bude zkompilován i v případě, že existuje explicitní nebo implicitní alias se stejným názvem.  
  
 Implicitní aliasy jsou automaticky generovány na základě vstupu uživatele. Například následující řádek kódu vygeneruje název jako alias pro oba sloupce a proto bude kolidovat.  
  
```sql  
SELECT product.NAME, person.NAME  
```  
  
 Následující řádek kódu, který používá explicitní aliasy, selže také. V takovém případě však bude chyba zřejmá čtením kódu.  
  
```sql  
SELECT 1 AS X, 2 AS X …  
```  
  
## <a name="scoping-rules"></a>Pravidla oboru  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] definuje pravidla vytváření oborů, která určují, kdy jsou konkrétní proměnné viditelné v dotazovacím jazyce. Některé výrazy nebo příkazy zavádí nové názvy. Pravidla oboru určují, kde lze tyto názvy použít a kdy nebo kde nová deklarace, která má stejný název jako jiný, může skrýt její předchůdce.  
  
 Pokud jsou názvy definovány v dotazu [!INCLUDE[esql](../../../../../../includes/esql-md.md)], jsou označovány jako definované v rámci oboru. Obor pokrývá celou oblast dotazu. Všechny výrazy nebo odkazy na názvy v rámci určitého oboru mohou zobrazovat názvy, které jsou definovány v rámci tohoto oboru. Před začátkem oboru a po jeho ukončení nelze odkazovat na názvy, které jsou definovány v rámci oboru.  
  
 Rozsahy můžou být vnořené. Části [!INCLUDE[esql](../../../../../../includes/esql-md.md)] zavádí nové obory, které pokrývají celé oblasti, a tyto oblasti mohou obsahovat jiné výrazy [!INCLUDE[esql](../../../../../../includes/esql-md.md)], které také zavádí obory. Pokud jsou obory vnořené, lze vytvořit odkazy na názvy, které jsou definovány v nejvnitřnějším oboru, který obsahuje odkaz. Lze také vytvořit odkazy na všechny názvy, které jsou definovány v libovolném vnějším oboru. Všechny dva obory definované v rámci stejného oboru se považují za rozsahy na stejné úrovni. Nelze vytvořit odkazy na názvy, které jsou definovány v rámci oborů na stejné úrovni.  
  
 Pokud název deklarovaný ve vnitřním oboru odpovídá názvu deklarovanému ve vnějším oboru, odkazy v rámci vnitřního oboru nebo v rámci oborů deklarovaných v rámci tohoto oboru odkazují pouze na nově deklarovaný název. Název ve vnějším oboru je skrytý.  
  
 Dokonce i v rámci stejného oboru nelze na jejich definování odkazovat na názvy.  
  
 Globální názvy mohou existovat jako součást spouštěcího prostředí. To může zahrnovat názvy trvalých kolekcí nebo proměnných prostředí. Aby byl název globální, musí být deklarován v nejvzdálenějším oboru.  
  
 Parametry nejsou v oboru. Vzhledem k tomu, že odkazy na parametry zahrnují speciální syntaxi, názvy parametrů nebudou nikdy kolidovat s jinými názvy v dotazu.  
  
### <a name="query-expressions"></a>Výrazy dotazu  
 Výraz dotazu [!INCLUDE[esql](../../../../../../includes/esql-md.md)] zavádí nový obor. Názvy, které jsou definovány v klauzuli FROM, jsou představeny v rozsahu od v pořadí vzhledem k pravé straně. V seznamu spojení můžou výrazy odkazovat na názvy, které byly definovány dříve v seznamu. Veřejné vlastnosti (pole a tak dále) prvků určených v klauzuli FROM nejsou přidány do rozsahu od. Na tyto adresy musí být vždy odkazováno pomocí kvalifikovaného názvu. Obvykle jsou všechny části výrazu SELECT považovány za v rozsahu od.  
  
 Klauzule GROUP BY také zavádí nový obor na stejné úrovni. Každá skupina může mít název skupiny, který odkazuje na kolekci prvků ve skupině. Každý výraz seskupení také zavádí nový název do oboru skupiny. Kromě toho je do oboru přidán také vnořená agregace (nebo pojmenovaná skupina). Vlastní výrazy seskupení jsou v rozsahu od-Scope. Pokud je však použita klauzule GROUP BY, klauzule SELECT-list (projekce), HAVING a ORDER BY jsou považovány za v rámci rozsahu skupiny, a nikoli z oboru. Agregace dostávají zvláštní zacházení, jak je popsáno v následujícím seznamu s odrážkami.  
  
 Následují další poznámky o oborech:  
  
- Příkaz SELECT-list může do oboru zavést nové názvy, a to v uvedeném pořadí. Výrazy projekce vpravo mohou odkazovat na názvy, které jsou promítnuty vlevo.  
  
- Klauzule ORDER BY se může vztahovat na názvy (aliasy) zadané v seznamu SELECT.  
  
- Pořadí vyhodnocení klauzulí v rámci výrazu SELECT určuje pořadí, ve kterém jsou názvy představeny do oboru. Klauzule FROM je vyhodnocena jako první, následuje klauzule WHERE, klauzule GROUP by, HAVING, klauzule SELECT a nakonec klauzule ORDER BY.  
  
### <a name="aggregate-handling"></a>Agregované zpracování  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] podporuje dva formy agregací: agregace založené na kolekcích a agregace založené na skupinách. Agregace založené na kolekcích jsou upřednostňovanou konstrukcí v [!INCLUDE[esql](../../../../../../includes/esql-md.md)] a agregace založené na skupinách jsou podporovány pro kompatibilitu s SQL.  
  
 Při překladu agregované [!INCLUDE[esql](../../../../../../includes/esql-md.md)] se nejprve pokusí ho považovat za agregaci založenou na kolekcích. Pokud se to nepovede, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] transformuje agregovaný vstup na odkaz na vnořenou agregaci a pokusí se tento nový výraz vyřešit, jak je znázorněno v následujícím příkladu.  
  
 `AVG(t.c) becomes AVG(group..(t.c))`  
  
## <a name="see-also"></a>Viz také:

- [Reference k Entity SQL](entity-sql-reference.md)
- [Přehled Entity SQL](entity-sql-overview.md)
- [Vstupní znaková sada](input-character-set-entity-sql.md)

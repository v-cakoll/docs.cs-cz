---
title: Vytváření vlastních součástí naslouchajících protokolům
ms.date: 07/20/2015
helpviewer_keywords:
- custom log listeners
- My.Application.Log object, custom log listeners
ms.assetid: 0e019115-4b25-4820-afb1-af8c6e391698
ms.openlocfilehash: 5a140607a4fe7e1e13de54e8d56cab53e52aaa2a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398263"
---
# <a name="walkthrough-creating-custom-log-listeners-visual-basic"></a>Návod: Vytváření vlastních součástí naslouchajících protokolům (Visual Basic)

Tento návod ukazuje, jak vytvořit vlastní naslouchací proces protokolu a nakonfigurovat ho tak, aby naslouchal výstupu `My.Application.Log` objektu.

## <a name="getting-started"></a>začínáme

Naslouchací procesy protokolu musí dědit od <xref:System.Diagnostics.TraceListener> třídy.

#### <a name="to-create-the-listener"></a>Vytvoření naslouchacího procesu

- V aplikaci vytvořte třídu s názvem `SimpleListener` , která dědí z <xref:System.Diagnostics.TraceListener> .

     [!code-vb[VbVbalrMyApplicationLog#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#16)]

     <xref:System.Diagnostics.TraceListener.Write%2A>Metody a <xref:System.Diagnostics.TraceListener.WriteLine%2A> , které jsou požadovány pro základní třídu, volají `MsgBox` pro zobrazení jejich vstupu.

     <xref:System.Security.Permissions.HostProtectionAttribute>Atribut se aplikuje na <xref:System.Diagnostics.TraceListener.Write%2A> metody a <xref:System.Diagnostics.TraceListener.WriteLine%2A> , aby jejich atributy odpovídaly metodám základní třídy. <xref:System.Security.Permissions.HostProtectionAttribute>Atribut umožňuje hostiteli, který spouští kód, určit, že kód zveřejňuje synchronizaci hostitele.

    > [!NOTE]
    > <xref:System.Security.Permissions.HostProtectionAttribute>Atribut je platný pouze v nespravovaných aplikacích, které jsou hostiteli modulu CLR (Common Language Runtime) a které implementují ochranu hostitele, například SQL Server.

Chcete-li zajistit, aby `My.Application.Log` používala naslouchací proces protokolu, měli byste silně pojmenovat sestavení, které obsahuje váš naslouchací proces protokolu.

Další postup poskytuje několik jednoduchých kroků pro vytvoření silně pojmenovaného sestavení naslouchacího procesu protokolu. Další informace naleznete v tématu [vytváření a používání sestavení se silným názvem](../../../../standard/assembly/create-use-strong-named.md).

#### <a name="to-strongly-name-the-log-listener-assembly"></a>Pro silně pojmenování sestavení naslouchacího procesu protokolu

1. Máte projekt vybraný v **Průzkumník řešení**. V nabídce **projekt** klikněte na příkaz **vlastnosti**.

2. Klikněte na kartu **podepisování** .

3. Vyberte pole **podepsat sestavení** .

4. **\<New>** V rozevíracím seznamu vyberte **soubor klíče se silným názvem** vyberte.

     Otevře se dialogové okno **vytvořit klíč se silným názvem** .

5. Zadejte název souboru klíče do pole **název souboru klíče** .

6. Do polí **Zadejte** heslo a **potvrďte heslo** zadejte heslo.

7. Klikněte na tlačítko **OK**.

8. Znovu sestavte aplikaci.

## <a name="adding-the-listener"></a>Přidání naslouchacího procesu

Nyní, když má sestavení silný název, je nutné určit silný název naslouchacího procesu tak, aby `My.Application.Log` používal naslouchací proces protokolu.

Formát silně pojmenovaného typu je následující.

\<type name>, \<assembly name>, \<version number>, \<culture>, \<strong name>

#### <a name="to-determine-the-strong-name-of-the-listener"></a>Určení silného názvu naslouchacího procesu

- Následující kód ukazuje, jak určit název silně pojmenovaného typu pro `SimpleListener` .

     [!code-vb[VbVbalrMyApplicationLog#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#17)]

     Silný název typu závisí na vašem projektu.

Se silným názvem můžete přidat naslouchací proces do `My.Application.Log` kolekce log-Listener.

#### <a name="to-add-the-listener-to-myapplicationlog"></a>Přidání naslouchacího procesu do My. Application. log

1. V **Průzkumník řešení** klikněte pravým tlačítkem na soubor App. config a vyberte **otevřít**.

     -nebo-

     Pokud existuje soubor App. config:

    1. V nabídce **projekt** klikněte na příkaz **Přidat novou položku**.

    2. V dialogovém okně **Přidat novou položku** vyberte možnost **konfigurační soubor aplikace**.

    3. Klikněte na tlačítko **Add** (Přidat).

2. Vyhledejte `<listeners>` část v části `<source>` s `name` atributem "DefaultSource", který se nachází v `<sources>` části. `<sources>`Oddíl je umístěný v části `<system.diagnostics>` v části nejvyšší úrovně `<configuration>` .

3. Přidejte tento element do `<listeners>` oddílu:

    ```xml
    <add name="SimpleLog" />
    ```

4. Vyhledejte část v části v `<sharedListeners>` `<system.diagnostics>` sekci nejvyšší úrovně `<configuration>` .

5. Přidejte tento element do této `<sharedListeners>` části:

    ```xml
    <add name="SimpleLog" type="SimpleLogStrongName" />
    ```

     Změňte hodnotu na se `SimpleLogStrongName` silným názvem naslouchacího procesu.

## <a name="see-also"></a>Viz také

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [Práce s protokoly aplikací](working-with-application-logs.md)
- [Postupy: Protokolování výjimek](how-to-log-exceptions.md)
- [Postupy: Zápis zpráv protokolu](how-to-write-log-messages.md)
- [Návod: Změna místa, kam objekt My.Application.Log zapisuje informace](walkthrough-changing-where-my-application-log-writes-information.md)

---
title: 'Postupy: Volání procedury vlastnosti'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- Visual Basic code, properties
- procedures [Visual Basic], calling
- properties [Visual Basic], property procedures
- procedure calls [Visual Basic], property procedures
ms.assetid: 96bc4d74-d9c3-4b7a-954d-58ac8553cd94
ms.openlocfilehash: 006961a0f1d4be6b0d52be5bc273dad9733bfe56
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388696"
---
# <a name="how-to-call-a-property-procedure-visual-basic"></a>Postupy: Volání procedury vlastnosti (Visual Basic)
Proceduru vlastnosti zavoláte uložením hodnoty do vlastnosti nebo načtením její hodnoty. K vlastnosti přistupujete stejným způsobem jako při přístupu k proměnné.  
  
 `Set`Procedura vlastnosti ukládá hodnotu a její `Get` procedura tuto hodnotu načítá. Nevolejte ale explicitně tyto procedury podle názvu. Vlastnost použijete v příkazu přiřazení nebo výrazu stejně, jako byste ukládali nebo načetli hodnotu proměnné. Visual Basic provede volání procedur vlastností.  
  
### <a name="to-call-a-propertys-get-procedure"></a>Volání procedury Get vlastnosti  
  
1. Použijte název vlastnosti ve výrazu stejným způsobem, jako byste použili název proměnné. Vlastnost můžete použít všude, kde můžete použít proměnnou nebo konstantu.  
  
     -nebo-  
  
     Použijte název vlastnosti za znaménkem EQUAL ( `=` ) v příkazu přiřazení.  
  
     Následující příklad přečte hodnotu <xref:Microsoft.VisualBasic.DateAndTime.Now%2A> vlastnosti, implicitně volá její `Get` proceduru.  
  
     [!code-vb[VbVbalrDateProperties#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDateProperties/VB/Module1.vb#4)]  
  
2. Pokud vlastnost přebírá argumenty, uveďte seznam argumentů tak, že postupujete podle názvu vlastnosti s závorkami. Pokud neexistují žádné argumenty, můžete volitelně vynechat závorky.  
  
3. Argumenty umístěte do seznamu argumentů v závorkách a oddělte je čárkami. Ujistěte se, že jste zadali argumenty ve stejném pořadí, v jakém vlastnost definuje odpovídající parametry.  
  
 Hodnota vlastnosti se účastní ve výrazu stejně jako proměnná nebo konstanta nebo je uložena v proměnné nebo vlastnosti na levé straně příkazu přiřazení.  
  
### <a name="to-call-a-propertys-set-procedure"></a>Volání procedury set vlastnosti  
  
1. Použijte název vlastnosti na levé straně příkazu přiřazení.  
  
     Následující příklad nastaví hodnotu <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A> vlastnosti implicitním voláním `Set` procedury.  
  
     [!code-vb[VbVbcnProcedures#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#11)]  
  
2. Pokud vlastnost přebírá argumenty, uveďte seznam argumentů tak, že postupujete podle názvu vlastnosti s závorkami. Pokud neexistují žádné argumenty, můžete volitelně vynechat závorky.  
  
3. Argumenty umístěte do seznamu argumentů v závorkách a oddělte je čárkami. Ujistěte se, že jste zadali argumenty ve stejném pořadí, v jakém vlastnost definuje odpovídající parametry.  
  
 Hodnota vygenerovaná na pravé straně příkazu přiřazení je uložena ve vlastnosti.  
  
## <a name="see-also"></a>Viz také

- [Procedury vlastnosti](./property-procedures.md)
- [Parametry a argumenty procedury](./procedure-parameters-and-arguments.md)
- [Property – příkaz](../../../language-reference/statements/property-statement.md)
- [Rozdíly mezi vlastnostmi a proměnnými v jazyce Visual Basic](./differences-between-properties-and-variables.md)
- [Postupy: Vytvoření vlastnosti](./how-to-create-a-property.md)
- [Postupy: Deklarace vlastnosti se smíšenými úrovněmi přístupu](./how-to-declare-a-property-with-mixed-access-levels.md)
- [Postupy: Deklarace a volání výchozí vlastnosti v jazyce Visual Basic](./how-to-declare-and-call-a-default-property.md)
- [Postupy: Vložení hodnoty do vlastnosti](./how-to-put-a-value-in-a-property.md)
- [Postupy: Získání hodnoty z vlastnosti](./how-to-get-a-value-from-a-property.md)
- [Get – příkaz](../../../language-reference/statements/get-statement.md)
- [Set – příkaz](../../../language-reference/statements/set-statement.md)

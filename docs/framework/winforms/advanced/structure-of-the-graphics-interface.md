---
title: Struktura rozhraní grafiky
ms.date: 03/30/2017
helpviewer_keywords:
- GDI+, using managed interface
- graphics [Windows Forms], class structure
ms.assetid: 010a1e46-656b-40a1-8d5d-87aa05ee1243
ms.openlocfilehash: d3b16249b6bae4a113661f5a3a47097046ba20f1
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505279"
---
# <a name="structure-of-the-graphics-interface"></a>Struktura rozhraní grafiky
Spravované třídy rozhraní GDI + obsahuje přibližně 60 třídy, 50 výčty a struktury 8. <xref:System.Drawing.Graphics> Třída je základní funkce rozhraní GDI +; je třída, která ve skutečnosti kreslí řádky, křivek, obrázky, obrázky a text.  
  
## <a name="important-classes"></a>Důležité třídy  
 Mnoho tříd pracovat společně <xref:System.Drawing.Graphics> třídy. Například <xref:System.Drawing.Graphics.DrawLine%2A> metoda přijímá <xref:System.Drawing.Pen> objektu, který obsahuje atributy (barvu, šířku, zpřístupní Styl přerušování a podobně) chcete kreslit čáry. <xref:System.Drawing.Graphics.FillRectangle%2A> Metoda může přijímat ukazatel <xref:System.Drawing.Drawing2D.LinearGradientBrush> objektu, který funguje s <xref:System.Drawing.Graphics> objektu tak, aby vyplnil obdélník postupně měnící barvou. <xref:System.Drawing.Font> a <xref:System.Drawing.StringFormat> objekty ovlivňují způsob <xref:System.Drawing.Graphics> objektu kreslení textu. A <xref:System.Drawing.Drawing2D.Matrix> objekt ukládá a manipuluje s Světové transformace <xref:System.Drawing.Graphics> objektu, který se používá k otočení, škálování a překlopit bitové kopie.  
  
 Rozhraní GDI + poskytuje několik struktury (například <xref:System.Drawing.Rectangle>, <xref:System.Drawing.Point>, a <xref:System.Drawing.Size>) pro uspořádání dat grafiky. Také určité třídy slouží především strukturované datové typy. Například <xref:System.Drawing.Imaging.BitmapData> třída je pomocné rutiny pro <xref:System.Drawing.Bitmap> třídy a <xref:System.Drawing.Drawing2D.PathData> třída je pomocné rutiny pro <xref:System.Drawing.Drawing2D.GraphicsPath> třídy.  
  
 Rozhraní GDI + definuje několik výčty, které jsou kolekce související s konstantami. Například <xref:System.Drawing.Drawing2D.LineJoin> výčet obsahuje prvky <xref:System.Drawing.Drawing2D.LineJoin.Bevel>, <xref:System.Drawing.Drawing2D.LineJoin.Miter>, a <xref:System.Drawing.Drawing2D.LineJoin.Round>, která zadejte stylů, které je možné připojit dva řádky.  
  
## <a name="see-also"></a>Viz také:

- [Přehled grafiky](graphics-overview-windows-forms.md)
- [Informace o spravovaném kódu GDI+](about-gdi-managed-code.md)
- [Použití spravovaných grafických tříd](using-managed-graphics-classes.md)

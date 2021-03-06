---
title: 'Postupy: Dlaždicové vyplnění obrazce pomocí obrázku'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- texture brushes [Windows Forms], tiling images with
- images [Windows Forms], filling shapes with
- shapes [Windows Forms], tiling with images
- bitmaps [Windows Forms], filling shapes with
ms.assetid: 6d407891-6e5c-4495-a546-3da5604e9fb8
ms.openlocfilehash: a906db44a548361df2822efa24d1dd1849cb5a24
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65063741"
---
# <a name="how-to-tile-a-shape-with-an-image"></a>Postupy: Dlaždicové vyplnění obrazce pomocí obrázku
Stejně jako dlaždice mohou být umístěny vedle sebe k pokrytí a podlaží, obdélníkové imagí umístěny vedle sebe na hodnotu fill (dlaždice) tvaru. Na dlaždici vnitřní část obrazce pomocí textury štětce. Při sestavování <xref:System.Drawing.TextureBrush> objekt, jeden z argumentů předat konstruktoru je <xref:System.Drawing.Image> objektu. Když Vymalovat vnitřní část obrazce pomocí textury štětce, tvar je vyplněn opakovaného kopírování tohoto obrázku.  
  
 Vlastnost režim zalamování řádků <xref:System.Drawing.TextureBrush> objekt určuje, jak je na obrázku orientovaný jako se opakuje obdélníkové mřížky. Zkontrolujte všechny dlaždice v mřížce mají stejnou orientaci nebo můžete vytvořit image Převrátit na ose z jedné mřížce pozice na další. Překlopení může být vodorovné, svislé nebo obojí. Následující příklady ukazují dělení do bloků s různými typy překlopení.  
  
### <a name="to-tile-an-image"></a>Na dlaždici bitovou kopii  
  
- Tento příklad používá na dlaždici 200 x 200 obdélníku na následujícím obrázku 75 × 75.  
  
 ![Dlaždice obrázku, který se zobrazí červený house a stromu.](./media/how-to-tile-a-shape-with-an-image/rectangle-tile-200x200.gif)  
  
- Následující obrázek znázorňuje, jak je obdélník tiled v obrázku. Všimněte si, že všechny dlaždice mají stejnou orientaci; neexistuje žádné překlopení.  
  
 ![Obdélník tiled image pomocí stejné orientace pro všemi dlaždicemi.](./media/how-to-tile-a-shape-with-an-image/rectangle-tiled-image-no-flip.gif)  
  
 [!code-csharp[System.Drawing.UsingABrush#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingABrush#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#31)]  
  
### <a name="to-flip-an-image-horizontally-while-tiling"></a>Chcete-li Převrátit obrázek vodorovně při dělení do bloků  
  
- Tento příklad používá stejnou bitovou kopii 75 × 75 tak, aby vyplnil 200 x 200 obdélník. Režim zalamování nastavena na Převrátit obrázek vodorovně. Následující obrázek znázorňuje, jak je obdélník tiled v obrázku. Všimněte si, že při přesunu z jedné dlaždice na další na daném řádku, je obrázek vodorovně obráceně.  
  
 ![Obdélník vedle sebe s imagí obráceně vodorovně.](./media/how-to-tile-a-shape-with-an-image/rectangle-tiled-image-horizontal-flip.gif)  
  
 [!code-csharp[System.Drawing.UsingABrush#32](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.UsingABrush#32](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#32)]  
  
### <a name="to-flip-an-image-vertically-while-tiling"></a>Chcete-li Převrátit obrázek svisle při dělení do bloků  
  
- Tento příklad používá stejnou bitovou kopii 75 × 75 tak, aby vyplnil 200 x 200 obdélník. Režim zalamování nastavena na Převrátit obrázek svisle.  
  
     [!code-csharp[System.Drawing.UsingABrush#33](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#33)]
     [!code-vb[System.Drawing.UsingABrush#33](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#33)]  
  
### <a name="to-flip-an-image-horizontally-and-vertically-while-tiling"></a>Chcete-li Převrátit obrázek vodorovně a svisle při dělení do bloků  
  
- Tento příklad používá stejnou bitovou kopii 75 × 75 na dlaždici 200 x 200 obdélník. Režim zalamování nastavena na Převrátit obrázek vodorovně i svisle. Následující obrázek znázorňuje, jak je obdélník rozložen formou dlaždic imagí. Všimněte si, že při přesunu z jedné dlaždice na další na daném řádku, je obrázek vodorovně překlopení a při přesunu z jedné dlaždice na další v daném sloupci, obrázek svisle obráceně.  
  
 ![Obdélník s použitím image obráceně vodorovně a svisle vedle sebe.](./media/how-to-tile-a-shape-with-an-image/rectangle-tiled-image-horizontal-vertical-flip.gif)  
  
 [!code-csharp[System.Drawing.UsingABrush#34](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#34)]
 [!code-vb[System.Drawing.UsingABrush#34](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#34)]  
  
## <a name="see-also"></a>Viz také:

- [Použití štětce k vyplnění obrazců](using-a-brush-to-fill-shapes.md)

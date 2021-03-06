---
title: 'Postupy: Zaoblení rohů RectangleGeometry'
ms.date: 03/30/2017
helpviewer_keywords:
- corners [WPF], rounding
- RectangleGeometry class [WPF], rounding corners
- graphics [WPF], rounding corners of RectangleGeometry objects [WPF]
- rounding corners of RectangleGeometry objects [WPF]
ms.assetid: 926644bc-1357-4c0b-ac81-694bd090ae87
ms.openlocfilehash: eb2f173bedb903e12b2795264c684524cfa09825
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "61651400"
---
# <a name="how-to-round-the-corners-of-a-rectanglegeometry"></a>Postupy: Zaoblení rohů RectangleGeometry
K Zakulacení rohů <xref:System.Windows.Media.RectangleGeometry>, nastavte jeho <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> a <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> vlastnosti na hodnotu větší než nula. Čím větší hodnoty, rohů udává větší zaoblení obdélníku.  
  
## <a name="example"></a>Příklad  
 Následující příklad ukazuje několik <xref:System.Windows.Media.RectangleGeometry> objekty s různými <xref:System.Windows.Media.RectangleGeometry.RadiusX%2A> a <xref:System.Windows.Media.RectangleGeometry.RadiusY%2A> nastavení. <xref:System.Windows.Media.RectangleGeometry> Objekty jsou zobrazeny pomocí <xref:System.Windows.Shapes.Path> elementy.  
  
 [!code-xaml[GeometryOverviewSamples_snip#GraphicsMMRoundedRectangleGeometryExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometryOverviewSamples_snip/CS/RectangleGeometryRoundedCornerExample.xaml#graphicsmmroundedrectanglegeometryexamplewholepage)]  
  
 ![Obdélníků pomocí různých RadiusX&#47;RadiusY nastavení](./media/graphicsmm-rounded.png "graphicsmm_rounded")  
Obdélníky zaoblené rohy  
  
## <a name="see-also"></a>Viz také:

- [Přehled geometrie](geometry-overview.md)
- [Vytvoření složeného tvaru](how-to-create-a-composite-shape.md)
- [Vytvoření tvaru pomocí PathGeometry](how-to-create-a-shape-by-using-a-pathgeometry.md)

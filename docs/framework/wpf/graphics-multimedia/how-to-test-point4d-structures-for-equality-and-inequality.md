---
title: 'Postupy: Testování struktur Point4D na rovnost a nerovnost'
ms.date: 03/30/2017
helpviewer_keywords:
- inequality [WPF], testing Point4D structures for
- equality [WPF], testing Point4D structures for
- testing [WPF], Point4D structures for equality
- Point4D structures [WPF], testing for inequality
- testing [WPF], Point4D structures for inequality
- Point4D structures [WPF], testing for equality
ms.assetid: e004a67e-db7f-4af8-a31f-e6b2a44ccf34
ms.openlocfilehash: ce1188e99ef2b0682427cc2e227aaccd27f7c4f4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2019
ms.locfileid: "62050633"
---
# <a name="how-to-test-point4d-structures-for-equality-and-inequality"></a>Postupy: Testování struktur Point4D na rovnost a nerovnost
Tento příklad ukazuje, jak otestovat <xref:System.Windows.Media.Media3D.Point4D> struktury rovnost a nerovnost.  
  
 Následující kód ukazuje, jak otestovat <xref:System.Windows.Media.Media3D.Point4D> struktur rovnost a nerovnost pomocí <xref:System.Windows.Media.Media3D.Point4D> rovnosti metody.  <xref:System.Windows.Media.Media3D.Point4D> Struktury jsou testovány z hlediska rovnosti pomocí přetížených rovnosti (`==`) operátor, pak pro nerovnost pomocí přetížených nerovnosti (`!=`) operátor a nakonec <xref:System.Windows.Media.Media3D.Point3D> strukturu a <xref:System.Windows.Media.Media3D.Point4D> Struktura nebyly zvoleny na rovnost pomocí statické <xref:System.Windows.Media.Media3D.Point4D.Equals%2A> metody.  
  
## <a name="example"></a>Příklad  
 [!code-csharp[3DGallery_procedural_snip#Point4DEqualityExample_csharp](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Misc3DOperationsExample.cs#point4dequalityexample_csharp)]  
  
## <a name="see-also"></a>Viz také:

- <xref:System.Windows.Media.Media3D.Point4D.op_Equality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.op_Inequality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>

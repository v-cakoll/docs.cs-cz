---
title: <c>– Průvodce programováním v C#
ms.date: 07/20/2015
f1_keywords:
- c
- <c>
helpviewer_keywords:
- text, marking as code [C#]
- code, marking text as [C#]
- c C# XML tag
- <c> C# XML tag
ms.assetid: aad5b16e-a29e-445e-bd0d-eea0b138d7b2
ms.openlocfilehash: a09bcd069e2f85f4a21736cb218c42c0e481d70b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287464"
---
# <a name="c-c-programming-guide"></a>\<c>(Průvodce programováním v C#)

## <a name="syntax"></a>Syntaxe

```xml
<c>text</c>
```

## <a name="parameters"></a>Parametry

- `text`

  Text, který chcete označit jako kód.

## <a name="remarks"></a>Poznámky

`<c>`Značka poskytuje způsob, jak označit, že text v rámci popisu by měl být označen jako kód. Slouží [\<code>](./code.md) k označení více řádků jako kódu.

Zkompilujte s [-doc](../../language-reference/compiler-options/doc-compiler-option.md) a zpracujte komentáře k dokumentaci do souboru.

## <a name="example"></a>Příklad

[!code-csharp[csProgGuideDocComments#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#2)]
  
## <a name="see-also"></a>Viz také

- [Průvodce programováním v C#](../index.md)
- [Doporučené značky pro komentáře dokumentace](./recommended-tags-for-documentation-comments.md)

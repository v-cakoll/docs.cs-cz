---
title: Kódování souborů
ms.date: 07/20/2015
helpviewer_keywords:
- character encodings
- files [Visual Basic], encoding
- Unicode, file encoding
- file encoding
ms.assetid: ea2c5f5f-bbb1-4150-9928-b9951fa6bc57
ms.openlocfilehash: f906b2f2d747a7950c70a24549bbf5423e5b87b4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401742"
---
# <a name="file-encodings-visual-basic"></a>Kódování souborů (Visual Basic)

Kódování souborů, označovaná také jako kódování znaků, určují způsob reprezentace znaků při zpracování textu. Jedno kódování může být vhodnější než jiné, a to z toho smyslu, které znaky jazyka může nebo nemůže zpracovat, i když je obvykle upřednostňovaný Unicode.

Při čtení nebo zapisování do souborů může nesprávně odpovídat kódování souborů způsobit výjimky nebo nesprávné výsledky.

## <a name="types-of-encodings"></a>Typy kódování

Unicode je preferované kódování při práci se soubory. Unicode je celosvětový standard kódování znaků, který používá 16bitové hodnoty kódu pro reprezentaci všech znaků používaných v moderních výpočetních prostředích, včetně technických symbolů a speciálních znaků používaných při publikování.

Předchozí standardy kódování znaků se skládají z tradičních znakových sad, jako je například znaková sada Windows ANSI, která používá 8bitové hodnoty kódu, nebo kombinace 8 bitových hodnot, které reprezentují znaky používané v konkrétním jazyce nebo geografické oblasti.

## <a name="encoding-class"></a>Encoding – třída

<xref:System.Text.Encoding>Třída představuje kódování znaků. Tato tabulka uvádí typy dostupných kódování a popisuje je.

|Name|Description|
|---|---|
|<xref:System.Text.ASCIIEncoding>|Představuje kódování znaků ASCII znaků Unicode.|
|<xref:System.Text.UnicodeEncoding>|Představuje kódování UTF-16 znaků Unicode.|
|<xref:System.Text.UTF32Encoding>|Představuje kódování UTF-32 znaků Unicode.|
|<xref:System.Text.UTF7Encoding>|Představuje kódování UTF-7 znaků Unicode.|
|<xref:System.Text.UTF8Encoding>|Představuje kódování UTF-8 znaků Unicode.|

## <a name="see-also"></a>Viz také

- [Čtení ze souborů](reading-from-files.md)
- [Zápis do souborů](writing-to-files.md)

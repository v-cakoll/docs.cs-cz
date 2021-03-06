---
title: příkaz pro seznam nástrojů dotnet
description: Příkaz pro výpis seznamu nástrojů dotnet obsahuje seznam nástrojů .NET Core, které jsou nainstalovány na vašem počítači.
ms.date: 02/14/2020
ms.openlocfilehash: 4035c5be233232e53c6d7150485f737108c1e18d
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925459"
---
# <a name="dotnet-tool-list"></a>dotnet tool list

**Tento článek se týká:** ✔️ .net Core 2,1 SDK a novějších verzí

## <a name="name"></a>Název

`dotnet tool list`– Zobrazí seznam všech [nástrojů .NET Core](global-tools.md) zadaného typu, které jsou aktuálně nainstalované na vašem počítači.

## <a name="synopsis"></a>Stručný obsah

```dotnetcli
dotnet tool list -g|--global

dotnet tool list --tool-path <PATH>

dotnet tool list --local

dotnet tool list

dotnet tool list -h|--help
```

## <a name="description"></a>Popis

`dotnet tool list`Příkaz umožňuje zobrazit seznam všech nástrojů .NET Core Global, Tool-Path nebo místních nástrojů, které jsou nainstalovány na vašem počítači. Příkaz vypíše název balíčku, nainstalovanou verzi a příkaz nástroje.  Chcete-li použít příkaz, zadejte jednu z následujících možností:

* Pokud chcete zobrazit seznam globálních nástrojů nainstalovaných ve výchozím umístění, použijte `--global` možnost.
* Pokud chcete zobrazit seznam globálních nástrojů nainstalovaných ve vlastním umístění, použijte `--tool-path` možnost.
* Chcete-li zobrazit seznam místních nástrojů, použijte `--local` možnost nebo vynechejte `--global` `--tool-path` Možnosti, a `--local` .

**K dispozici jsou místní nástroje od .NET Core SDK 3,0.**

## <a name="options"></a>Možnosti

- **`-g|--global`**

  Obsahuje seznam globálních nástrojů pro všechny uživatele. Nelze kombinovat s `--tool-path` možností. Vynechání obou `--global` a `--tool-path` seznam místních nástrojů.

- **`-h|--help`**

  Vypíše krátkou nápovědu k příkazu.

- **`--local`**

  Zobrazí seznam místních nástrojů pro aktuální adresář. Nelze kombinovat s `--global` `--tool-path` možnostmi nebo. Vynechání obou `--global` a `--tool-path` seznam místních nástrojů, i když není `--local` zadaný.

- **`--tool-path <PATH>`**

  Určuje vlastní umístění, kde se mají najít globální nástroje. Cesta může být absolutní nebo relativní. Nelze kombinovat s `--global` možností. Vynechání obou `--global` a `--tool-path` seznam místních nástrojů.

## <a name="examples"></a>Příklady

- **`dotnet tool list -g`**

  Zobrazí seznam všech globálních nástrojů nainstalovaných v celém počítači (aktuální profil uživatele).

- **`dotnet tool list --tool-path c:\global-tools`**

  Zobrazí seznam globálních nástrojů z konkrétního adresáře Windows.

- **`dotnet tool list --tool-path ~/bin`**

  Zobrazí seznam globálních nástrojů z konkrétního adresáře Linux/macOS.

- **`dotnet tool list`** ani**`dotnet tool list --local`**

  Zobrazí seznam všech místních nástrojů dostupných v aktuálním adresáři.

## <a name="see-also"></a>Viz také

- [Nástroje .NET Core](global-tools.md)
- [Kurz: instalace a použití globálního nástroje .NET Core pomocí .NET Core CLI](global-tools-how-to-use.md)
- [Kurz: instalace a použití místního nástroje .NET Core pomocí .NET Core CLI](local-tools-how-to-use.md)

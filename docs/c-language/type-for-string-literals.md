---
title: 文字列リテラルの型
ms.date: 11/04/2016
helpviewer_keywords:
- string literals, type
- types [C], string literals
ms.assetid: f50a28af-20c1-4440-bdc6-564c86a309c8
ms.openlocfilehash: 7e832ac7aa08ad80ab395baa59eabbabb486b46f
ms.sourcegitcommit: 0ab61bc3d2b6cfbd52a16c6ab2b97a8ea1864f12
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62344851"
---
# <a name="type-for-string-literals"></a>文字列リテラルの型

文字列リテラルは、`char` の型配列 (つまり、**char[ ]** ) を持ちます  (ワイド文字列は、`wchar_t` の型配列 (つまり、**wchar_t[ ]** ) を持ちます)。これは、文字列が型 `char` の要素の配列であることを意味しています。 配列の要素の数は、文字列の文字の数に 1 (終端の null 文字) を足した数と同じです。

## <a name="see-also"></a>関連項目

[C 文字列リテラル](../c-language/c-string-literals.md)

---
title: 式エバリュエーター エラー CXX0036
ms.date: 11/04/2016
f1_keywords:
- CXX0036
helpviewer_keywords:
- CXX0036
- CAN0036
ms.assetid: 383404be-df5b-4eec-b113-df21bb5d269d
ms.openlocfilehash: 164fd9ee00071e218e5bb4f3ab00febc618725a7
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80195501"
---
# <a name="expression-evaluator-error-cxx0036"></a>式エバリュエーター エラー CXX0036

コンテキストが正しくありません {...} specification

このメッセージは、コンテキスト演算子 ( **{}** ) の使用におけるいくつかのエラーのいずれかによって生成できます。

- コンテキスト演算子 ( **{}** ) の構文が正しく指定されていませんでした。

   コンテキスト演算子の構文は次のとおりです。

     {*function*,*module*,*dll*}*式*

   これにより、*式*のコンテキストが指定されます。 コンテキスト演算子は、型キャストと同じ優先順位と使用法を持ちます。

   末尾のコンマは省略できます。 *関数*、*モジュール*、または*dll*のいずれかにリテラルコンマが含まれている場合は、名前全体をかっこで囲む必要があります。

- 関数名のスペルが間違っているか、指定されたモジュールまたはダイナミックリンクライブラリに存在しません。

   C は大文字と小文字が区別される言語であるため、*関数*は、ソースで定義されている場合とまったく同じように指定する必要があります。

- モジュールまたは DLL が見つかりませんでした。

   指定されたモジュールまたは DLL の完全なパス名を確認してください。

このエラーは CAN0036 と同じです。

---
title: ドット ディレクティブ
ms.date: 11/04/2016
helpviewer_keywords:
- NMAKE program, dot directives
- dot directives in NMAKE
ms.assetid: ab35da65-30b6-48b7-87d6-61503d7faf9f
ms.openlocfilehash: 2c21e8a18c76331f86a4e8966b4f67c9c9bc9b7d
ms.sourcegitcommit: c6f8e6c2daec40ff4effd8ca99a7014a3b41ef33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "64342824"
---
# <a name="dot-directives"></a>ドット ディレクティブ

行の先頭の記述ブロックの外側のドット ディレクティブを指定します。 ドット ディレクティブの先頭にピリオド (します。 )、コロン (:) が続きます。 スペースとタブが許可されます。 ドット ディレクティブの名前は、大文字と小文字、大文字。

|ディレクティブ|目的|
|---------------|-------------|
|**.無視します。**|メイクファイルの末尾に指定されている場所からのコマンドによって返されるゼロ以外の終了コードは無視されます。 既定では、(nmake の) は、コマンドが 0 以外の終了コードを返す場合を停止します。 エラー チェックを復元する **!CMDSWITCHES**します。 1 つのコマンドの終了コードを無視するには、ダッシュ (-) 修飾子を使用します。 ファイル全体の終了コードを無視するには使用/しました。|
|**.貴重:** *ターゲット*|保持*ターゲット*ディスクの場合、それらを更新するコマンドが停止しました。 影響を与えませんコマンドは、ファイルを削除することによって、割り込みを処理する場合。 スペースまたはタブの 1 つまたは複数のターゲットの名前を区切ります。 既定では、CTRL キーを押しながら C キーまたは CTRL + BREAK によってビルドが中断された場合、ターゲットは削除します。 各使用**します。貴重な**メイクファイル全体に適用されます複数の仕様は累積されます。|
|**.SILENT :**|メイクファイルの末尾に指定されている場所から、実行されたコマンドの表示を抑制します。 既定では、(nmake の) には、起動したコマンドが表示されます。 使用してエコーを復元する **!CMDSWITCHES**します。 1 つのコマンドのエコーを抑制するのには、使用、 **@** 修飾子。 ファイル全体のエコーを抑制するのには、使用/参照してください。|
|**.サフィックス:** `list`|推論規則に一致する; 用の拡張機能を一覧表示されます。次の拡張機能を含める定義済み: .exe .obj .asm .c .cpp .cxx .bas .cbl 対して .pas .res .rc .f .f90|

変更する、**します。サフィックス**リストの順序、または新しいリストを指定する一覧をクリアし、新しい設定を指定します。 一覧を消去するには、拡張子を指定しないコロンの後。

```
.SUFFIXES :
```

リストの末尾には、追加のサフィックスを追加するに次のように指定します。

```
.SUFFIXES : suffixlist
```

場所*suffixlist* 、1 つ以上のスペースまたはタブで区切られた追加のサフィックスの一覧を示します。 現在の設定を確認する**します。サフィックス**/P. と NMAKE の実行

## <a name="see-also"></a>関連項目

[NMAKE リファレンス](nmake-reference.md)

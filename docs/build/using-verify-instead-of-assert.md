---
title: ASSERT に代わる VERIFY の使用
ms.date: 11/04/2016
f1_keywords:
- assert
helpviewer_keywords:
- ASSERT statements
- debugging [MFC], ASSERT statements
- VERIFY macro
- assertions, troubleshooting ASSERT statements
- debugging assertions
- assertions, debugging
ms.assetid: 4c46397b-3fb1-49c1-a09b-41a72fae3797
ms.openlocfilehash: e6903616f8b4250b3d67db333be4fc17e8328952
ms.sourcegitcommit: 8105b7003b89b73b4359644ff4281e1595352dda
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57826333"
---
# <a name="using-verify-instead-of-assert"></a>ASSERT に代わる VERIFY の使用

MFC アプリケーションのデバッグ バージョンを実行するときに問題がないとします。 ただし、同じアプリケーションのリリース バージョンがクラッシュした不適切な結果を返します。 または他のいくつかの異常な動作を示します。

この問題は、正しく動作することを確認する ASSERT ステートメントで重要なコードを配置するときに発生することができます。 ASSERT ステートメントは、MFC プログラムのリリース ビルドでコメント アウト、ので、コードは、リリース ビルドでは実行されません。

ASSERT 関数呼び出しが成功したことを確認するを使用している場合は、使用を検討して[確認](../mfc/reference/diagnostic-services.md#verify)代わりにします。 VERIFY マクロは、両方のデバッグでは、その引数を評価し、アプリケーションのリリース ビルドをします。

別の手法は、一時変数に関数の戻り値を代入し、ASSERT ステートメントで変数をテスト (推奨)。

次のコード フラグメントを確認します。

```
enum {
    sizeOfBuffer = 20
};
char *buf;
ASSERT(buf = (char *) calloc(sizeOfBuffer, sizeof(char) ));
strcpy_s( buf, sizeOfBuffer, "Hello, World" );
free( buf );
```

このコードは、MFC アプリケーションのデバッグ バージョンで完全に実行されます。 場合に呼び出し`calloc( )`が失敗したファイルと行番号を含む診断メッセージが表示されます。 ただしでは、MFC アプリケーションの製品版ビルド。

- 呼び出し`calloc( )`しないまま発生`buf`初期化されていない、または

- `strcpy_s( )` コピー"`Hello, World`"に、メモリ、場合によって、アプリケーションがクラッシュまたは応答を停止する原因のランダムなのか

- `free()` 割り当てられていないメモリを解放しようとします。

ASSERT を正しく使用するには、次のコード サンプルを変更する必要があります。

```
enum {
    sizeOfBuffer = 20
};
char *buf;
buf = (char *) calloc(sizeOfBuffer, sizeof(char) );
ASSERT( buf != NULL );
strcpy_s( buf, sizeOfBuffer, "Hello, World" );
free( buf );
```

または、代わりに検証を使用することができます。

```
enum {
    sizeOfBuffer = 20
};
char *buf;
VERIFY(buf = (char *) calloc(sizeOfBuffer, sizeof(char) ));
strcpy_s( buf, sizeOfBuffer, "Hello, World" );
free( buf );
```

## <a name="see-also"></a>関連項目

[リリース ビルドの問題の解決](fixing-release-build-problems.md)
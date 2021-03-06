---
title: コンパイラの警告 (レベル 3) C4101
ms.date: 11/04/2016
f1_keywords:
- C4101
helpviewer_keywords:
- C4101
ms.assetid: d98563cd-9dce-4aae-8f12-bd552a4ea677
ms.openlocfilehash: 0ac34fbaf4cbb54583394dff5b8645fe56b8b9cd
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80199046"
---
# <a name="compiler-warning-level-3-c4101"></a>コンパイラの警告 (レベル 3) C4101

' identifier ': 参照できないローカル変数です

ローカル変数は使用されません。 この警告は、明らかに次のような状況で発生します。

```cpp
// C4101a.cpp
// compile with: /W3
int main() {
int i;   // C4101
}
```

ただし、この警告は、クラスのインスタンスを使用して**静的**メンバー関数を呼び出す場合にも発生します。

```cpp
// C4101b.cpp
// compile with:  /W3
struct S {
   static int func()
   {
      return 1;
   }
};

int main() {
   S si;   // C4101, si is never used
   int y = si.func();
   return y;
}
```

この場合、コンパイラは、**静的**関数にアクセスするために `si` に関する情報を使用しますが、**静的**関数を呼び出すためにクラスのインスタンスは必要ありません。そのため、警告が出てきます。 この警告を解決するには、次のようにします。

- コンストラクターを追加します。コンパイラは、`func`への呼び出しで `si` のインスタンスを使用します。

- `func`の定義から**static**キーワードを削除します。

- **静的**関数を明示的に呼び出す: `int y = S::func();`します。

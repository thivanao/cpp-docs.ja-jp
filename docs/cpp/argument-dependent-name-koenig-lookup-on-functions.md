---
title: 関数の引数依存名の参照 (Koenig 参照)
ms.date: 11/04/2016
helpviewer_keywords:
- Koenig lookup
- argument-dependent lookup [C++]
ms.assetid: c0928401-da2c-4658-942d-9ba4df149c35
ms.openlocfilehash: 88811e8070fdfe398bc12734221dee772515d8bc
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80190538"
---
# <a name="argument-dependent-name-koenig-lookup-on-functions"></a>関数の引数依存名の参照 (Koenig 参照)

コンパイラは、引数依存の名前検索を使用して、非限定の関数呼び出しの定義を検索できます。 引数依存の名前検索は Koenig 検索とも呼ばれます。 関数呼び出しの各引数の型は、名前空間、クラス、構造体、共用体、またはテンプレートの階層内で定義されます。 修飾されていない[後置](../cpp/postfix-expressions.md)関数呼び出しを指定すると、コンパイラは、各引数の型に関連付けられている階層内の関数定義を検索します。

## <a name="example"></a>例

このサンプルでは、`f()` 関数は `x` 引数を受け取ります。 `x` 引数は `A::X` 型であり、これは `A` 名前空間で定義されています。 コンパイラは `A` 名前空間を検索し、`f()` 型の引数を受け取る `A::X` 関数の定義を見つけます。

```cpp
// argument_dependent_name_koenig_lookup_on_functions.cpp
namespace A
{
   struct X
   {
   };
   void f(const X&)
   {
   }
}
int main()
{
// The compiler finds A::f() in namespace A, which is where
// the type of argument x is defined. The type of x is A::X.
   A::X x;
   f(x);
}
```

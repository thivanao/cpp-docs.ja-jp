---
title: コンパイラの警告 (レベル 1) C4364
ms.date: 11/04/2016
f1_keywords:
- C4364
helpviewer_keywords:
- C4364
ms.assetid: 1477634c-d60f-4570-ad16-1aaeae24ac7f
ms.openlocfilehash: 79c8809b4de9d6853aaacec4283bf01d0e89305e
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80187103"
---
# <a name="compiler-warning-level-1-c4364"></a>コンパイラの警告 (レベル 1) C4364

as_friend 属性のない場所 (line_number) で以前に検出されたアセンブリ ' file ' に対してを使用して \#。as_friend 適用されていません

指定されたメタデータファイルに対して `#using` ディレクティブが繰り返されましたが、`as_friend` 修飾子が最初に出現するときに使用されませんでした。コンパイラは、2番目の `as_friend`を無視します。

詳細については、「 [FriendC++Assemblies ()](../../dotnet/friend-assemblies-cpp.md)」を参照してください。

## <a name="example"></a>例

コンポーネントを作成する例を次に示します。

```cpp
// C4364.cpp
// compile with: /clr /LD
ref class A {};
```

## <a name="example"></a>例

次の例では、C4364 が生成されます。

```cpp
// C4364_b.cpp
// compile with: /clr /W1 /c
#using " C4364.dll"
#using " C4364.dll" as_friend   // C4364
```

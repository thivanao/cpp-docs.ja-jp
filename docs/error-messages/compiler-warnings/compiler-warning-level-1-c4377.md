---
title: コンパイラの警告 (レベル 1) C4377
ms.date: 11/04/2016
f1_keywords:
- C4377
helpviewer_keywords:
- C4377
ms.assetid: a1c797b8-cd5e-4a56-b430-d07932e811cf
ms.openlocfilehash: b75b6bee88d0b72e77b32e58ae2f4634a9c30fa0
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80186999"
---
# <a name="compiler-warning-level-1-c4377"></a>コンパイラの警告 (レベル 1) C4377

ネイティブ型は、既定ではプライベートです。-d1PrivateNativeTypes は非推奨です

以前のリリースでは、アセンブリ内のネイティブ型は既定でパブリックになっており、非公開にするためにドキュメントに記載されていないコンパイラオプション ( **/d1PrivateNativeTypes**) が使用されていました。

ネイティブと CLR のすべての型は、アセンブリで既定でプライベートになったため、 **/d1PrivateNativeTypes**は不要になりました。

## <a name="example"></a>例

次の例では、C4377 が生成されます。

```cpp
// C4377.cpp
// compile with: /clr /d1PrivateNativeTypes /W1
// C4377 warning expected
int main() {}
```

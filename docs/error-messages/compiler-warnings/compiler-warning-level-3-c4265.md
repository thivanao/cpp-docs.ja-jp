---
title: コンパイラの警告 (レベル 3) C4265
ms.date: 11/04/2016
f1_keywords:
- C4265
helpviewer_keywords:
- C4265
ms.assetid: 20547159-6f30-4cc4-83aa-927884c8bb4c
ms.openlocfilehash: cfcbd9d9268785b87e45a833b332c276eec01522
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80161543"
---
# <a name="compiler-warning-level-3-c4265"></a>コンパイラの警告 (レベル 3) C4265

' class ': クラスは仮想関数を含んでいますが、デストラクターは仮想ではありません

クラスに仮想関数があり、非仮想デストラクターがある場合、基底クラスポインターを使用してクラスが破棄されたときに、型のオブジェクトが正しく破棄されない可能性があります。

既定では、この警告はオフに設定されています。 詳細については、「 [既定で無効になっているコンパイラ警告](../../preprocessor/compiler-warnings-that-are-off-by-default.md) 」を参照してください。

次の例では、C4265 が生成されます。

```cpp
// C4265.cpp
// compile with: /W3 /c
#pragma warning(default : 4265)
class B
{
public:
   virtual void vmf();

   ~B();
   // try the following line instead
   // virtual ~B();
};   // C4265

int main()
{
   B b;
}
```

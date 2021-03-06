﻿---
title: reinterpret_cast 演算子
ms.date: 11/04/2016
f1_keywords:
- reinterpret_cast_cpp
helpviewer_keywords:
- reinterpret_cast keyword [C++]
ms.assetid: eb3283c7-7f88-467e-affd-407d37b46d6c
ms.openlocfilehash: 34c2fcb0e1f7f4df4e207d1737afc9c42e011feb
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80188286"
---
# <a name="reinterpret_cast-operator"></a>reinterpret_cast 演算子

ポインターが他のポインター型に変換されることを許可します。 また、整数型から任意のポインター型への変換およびその逆の変換を許可します。

## <a name="syntax"></a>構文

```
reinterpret_cast < type-id > ( expression )
```

## <a name="remarks"></a>解説

**Reinterpret_cast**演算子の誤用は、簡単に安全でない場合があります。 必要な変換が本質的に低レベルでない限り、他のキャスト演算子の 1 つを使用する必要があります。

**Reinterpret_cast**演算子は、`char*` から `int*`への変換や、本質的に安全ではない `Unrelated_class*`への `One_class*` などの変換に使用できます。

**Reinterpret_cast**の結果は、元の型にキャストする以外のものには安全に使用できません。 その他の使用方法は、最高でも非ポータブルです。

**Reinterpret_cast**演算子は、 **const**、 **volatile**、 **__unaligned**の各属性をキャストできません。 これらの属性を削除する方法については、「 [Const_cast 演算子](../cpp/const-cast-operator.md)」を参照してください。

**Reinterpret_cast**演算子は、null ポインター値を変換先の型の null ポインター値に変換します。

**Reinterpret_cast**の実際の使用方法の1つは、2つの個別の値が同じインデックスで終了することがほとんどないように、値をインデックスにマップするハッシュ関数です。

```cpp
#include <iostream>
using namespace std;

// Returns a hash code based on an address
unsigned short Hash( void *p ) {
   unsigned int val = reinterpret_cast<unsigned int>( p );
   return ( unsigned short )( val ^ (val >> 16));
}

using namespace std;
int main() {
   int a[20];
   for ( int i = 0; i < 20; i++ )
      cout << Hash( a + i ) << endl;
}

Output:
64641
64645
64889
64893
64881
64885
64873
64877
64865
64869
64857
64861
64849
64853
64841
64845
64833
64837
64825
64829
```

**Reinterpret_cast**を使用すると、ポインターを整数型として扱うことができます。 結果は、一意のインデックス (高レベルの発生確率で一意) を生成するためにビット シフトされ、XOR されます。 インデックスは、関数の戻り値の型への標準 C 形式のキャストにより切り捨てられます。

## <a name="see-also"></a>参照

[キャスト演算子](../cpp/casting-operators.md)<br/>
[キーワード](../cpp/keywords-cpp.md)

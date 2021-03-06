---
title: コピー コンストラクターとコピー代入演算子 (C++)
ms.date: 11/04/2016
helpviewer_keywords:
- = operator [C++], copying objects
- assignment statements [C++], copying objects
- assignment operators [C++], for copying objects
- objects [C++], copying
- initializing objects, by copying objects
- copying objects
- assigning values to copy objects
ms.assetid: a94fe1f9-0289-4fb9-8633-77c654002c0d
ms.openlocfilehash: beabe4c6219975d33c7af98a94498188c9abfa55
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80189533"
---
# <a name="copy-constructors-and-copy-assignment-operators-c"></a>コピー コンストラクターとコピー代入演算子 (C++)

> [!NOTE]
> C++ 11 以降では、*コピー代入*と*移動代入*の2種類の代入がサポートされています。 この記事では、特に明示的に記載しない限り、"代入" はコピーの代入を意味します。 移動代入の詳細については、「[移動コンストラクターと移動C++代入演算子 ()](move-constructors-and-move-assignment-operators-cpp.md)」を参照してください。
>
> 代入演算と初期化操作では、いずれもオブジェクトがコピーされます。

- **割り当て**: あるオブジェクトの値が別のオブジェクトに割り当てられると、最初のオブジェクトが2番目のオブジェクトにコピーされます。 そのため、次のようになります。

    ```cpp
    Point a, b;
    ...
    a = b;
    ```

   の場合、`b` の値が `a` にコピーされます。

- **初期化**: 初期化は、新しいオブジェクトが宣言されたとき、引数が値によって関数に渡されたとき、または値によって関数から値が返されたときに発生します。

クラス型のオブジェクトに「コピー」の意味を定義できます。 たとえば、次のコードを検討してみましょう。

```cpp
TextFile a, b;
a.Open( "FILE1.DAT" );
b.Open( "FILE2.DAT" );
b = a;
```

前のコードは、「FILE1.DAT から FILE2.DAT に内容をコピーする」を意味する場合もありますが、「FILE2.DAT を無視して `b` を FILE1.DAT への 2 番目のハンドルにする」という意味もあります。 各クラスには、次のように適切なコピーのセマンティクスを割り当てる必要があります。

- 戻り値の型としてのクラス型への参照と、 **const**参照によって渡されるパラメーター (`ClassName& operator=(const ClassName& x);`など) と共に代入演算子**演算子 =** を使用する。

- コピー コンストラクターを使用する。

コピー コンストラクターを宣言していない場合、コンパイラはメンバーごとのコピー コンストラクターを生成します。  コピー代入演算子を宣言していない場合、コンパイラはメンバーごとのコピー代入演算子を生成します。 コピー コンストラクターを宣言しても、コンパイラで生成されるコピー代入演算子は抑制されません。また、その逆も同様です。 いずれか 1 つを実装する場合、コードの意味を明確にするために、もう 1 つも実装することをお勧めします。

コピーコンストラクターは、<em>クラス名</em><strong>&</strong>型の引数を受け取ります。ここで、*クラス*名は、コンストラクターが定義されているクラスの名前です。 次に例を示します。

```cpp
// spec1_copying_class_objects.cpp
class Window
{
public:
    Window( const Window& ); // Declare copy constructor.
    // ...
};

int main()
{
}
```

> [!NOTE]
> 可能な限り、コピーコンストラクターの引数**const** <em>クラス名</em><strong>&</strong>の型を作成します。 これによって、コピー コンストラクターが誤ってコピー元のオブジェクトを変更しないようにすることができます。 また、 **const**オブジェクトからコピーすることもできます。

## <a name="compiler-generated-copy-constructors"></a>コンパイラによって生成されたコピー コンストラクター

コンパイラによって生成されるコピーコンストラクターは、ユーザー定義のコピーコンストラクターと同様に、"*クラス名*への参照" 型の引数を1つ持ちます。 例外は、すべての基底クラスとメンバークラスに、 **const** <em>クラス名</em><strong>&</strong>型の単一の引数を取得するように宣言されたコピーコンストラクターがある場合です。 このような場合、コンパイラによって生成されるコピーコンストラクターの引数も**const**です。

コピーコンストラクターへの引数の型が**const**ではない場合、 **const**オブジェクトをコピーして初期化すると、エラーが発生します。 逆は true ではありません。引数が**const**の場合は、 **const**ではないオブジェクトをコピーすることによって初期化できます。

コンパイラによって生成された代入演算子は、const に関して同じパターンに従い**ます。** すべての基本クラスとメンバークラスの代入演算子が**const** <em>クラス名</em><strong>&</strong>型の引数を受け取る場合を除き、<em>クラス名</em><strong>&</strong>型の引数を1つ受け取ります。 この場合、クラスで生成された代入演算子は、 **const**引数を受け取ります。

> [!NOTE]
> コピー コンストラクターによって初期化されるか、コンパイラによって生成されるか、またはユーザーによって定義される場合、仮想基底クラスは構築される時点で 1 回だけ初期化されます。

影響はコピー コンストラクターの影響と似ています。 引数の型が**const**ではない場合、 **const**オブジェクトからの割り当てでエラーが発生します。 逆は true ではありません。 const 値が**const**で**ない値に**割り当てられている場合、代入は成功します。

オーバーロードされた代入演算子の詳細については、「[代入](../cpp/assignment.md)」を参照してください。

---
title: Array と WriteOnlyArray (C++/CX)
ms.date: 01/22/2017
ms.assetid: ef7cc5f9-cae6-4636-8220-f789e5b6aea4
ms.openlocfilehash: e050fad38d4f70c651fc0ebfddb51a33e31da6f3
ms.sourcegitcommit: 89d9e1cb08fa872483d1cde98bc2a7c870e505e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82032409"
---
# <a name="array-and-writeonlyarray-ccx"></a>Array と WriteOnlyArray (C++/CX)

C++/CX プログラムでは通常の C スタイルの配列または[std::array](../standard-library/array-class-stl.md)を自由に使用できますが[(std::vector](../standard-library/vector-class.md)が多くの場合、メタデータで公開されている API では、C スタイルの配列またはベクターを[プラットフォーム::配列](../cppcx/platform-array-class.md)または[プラットフォーム::WriteOnlyArray](../cppcx/platform-writeonlyarray-class.md)型に変換する必要があります)。 [Platform::Array](../cppcx/platform-array-class.md) 型は、 [std::vector](../standard-library/vector-class.md)ほどには効率的でも強力でもありません。そのため、一般的なガイドラインとして、配列要素で多くの操作を実行する内部コードでは使用を避ける必要があります。

次の配列型は、ABI を介して渡すことができます。

1. const Platform::Array^

1. Platform::Array^*

1. Platform::WriteOnlyArray

1. Platform::Array^ の戻り値

これらの配列型を使用して、Windows ランタイムで定義される 3 種類の配列パターンを実装します。

呼び出し元がメソッドに配列を渡すときに使用します。 C++ 入力パラメーターの型`const`は[、プラットフォーム::配列](../cppcx/platform-array-class.md)\<T>です。

FillArray メソッドが埋める配列を呼び出し元が渡すときに使用します。 C++ 入力パラメーターの型は[、プラットフォーム::WriteOnlyArray](../cppcx/platform-writeonlyarray-class.md)\<T>です。

メソッドが割り当てた配列を呼び出し元が受け取ったときに使用します。 C++/CX では、配列を Array^ として戻り値で返すことも、型 Array^* として Out パラメーターとして返すこともできます。

## <a name="passarray-pattern"></a>PassArray パターン

クライアント コードが配列を C++ メソッドに渡し、メソッドがその配列を変更しない場合、メソッドはその配列を定数 Array^ として受け入れます。 Windows ランタイム アプリケーション バイナリ インターフェイス (ABI) レベルでは、これは PassArray と呼ばれます。 次の例は、JavaScript に割り当てられた配列を、読み取り側の C++ 関数に渡す方法を示しています。

[!code-javascript[cx_arrays#101](../cppcx/codesnippet/JavaScript/array-and-writeonlyarray-c-_1.js)]

次のスニペットは、C++ メソッドを示します。

[!code-cpp[cx_arrays#01](../cppcx/codesnippet/CPP/js-array/class1.cpp#01)]

## <a name="receivearray-pattern"></a>ReceiveArray パターン

ReceiveArray パターンでは、クライアント コードは配列を宣言し、それにメモリを割り当てて初期化するメソッドに渡します。 C++ 入力パラメーターの型は、ポインターをハット:`Array<T>^*`にします。 次の例は、JavaScript で配列オブジェクトを宣言し、それを、メモリを割り当て、要素を初期化して JavaScript に返す C++ 関数に渡す方法を示しています。 JavaScript は、割り当てられた配列を戻り値として扱いますが、C++ 関数は出力パラメーターとして扱います。

[!code-javascript[cx_arrays#102](../cppcx/codesnippet/JavaScript/array-and-writeonlyarray-c-_3.js)]

次のスニペットは、C++ メソッドを実装する 2 通りの方法を示します。

[!code-cpp[cx_arrays#02](../cppcx/codesnippet/CPP/js-array/class1.cpp#02)]

## <a name="fill-arrays"></a>Fill 配列

配列を呼び出し元で割り当て、呼び出し先で初期化または変更する場合は、 `WriteOnlyArray`を使用します。 次の例は、 `WriteOnlyArray` を使用する C++ 関数を実装して、JavaScript から呼び出す方法を示しています。

[!code-javascript[cx_arrays#103](../cppcx/codesnippet/JavaScript/array-and-writeonlyarray-c-_5.js)]

次のスニペットは、C++ メソッドを実装する方法を示します。

[!code-cpp[cx_arrays#03](../cppcx/codesnippet/CPP/js-array/class1.cpp#03)]

## <a name="array-conversions"></a>配列変換

この例では、 [Platform::Array](../cppcx/platform-array-class.md) を使用して、その他の種類のコレクションを構築する方法を示しています。

[!code-cpp[cx_arrays#05](../cppcx/codesnippet/CPP/js-array/class1.cpp#05)]

次の例は、 [Platform::Array](../cppcx/platform-array-class.md) を C スタイル配列から構築して、パブリック メソッドから返す方法を示しています。

[!code-cpp[cx_arrays#06](../cppcx/codesnippet/CPP/js-array/class1.cpp#06)]

## <a name="jagged-arrays"></a>ジャグ配列

Windows ランタイムの型システムは、ジャグ配列の概念をサポートしていないため、パブリック メソッドで `IVector<Platform::Array<T>>` を戻り値またはメソッド パラメーターとして使用することはできません。 ABI を通じてジャグ配列またはシーケンスのシーケンスを渡すには、 `IVector<IVector<T>^>`を使用します。

## <a name="use-arrayreference-to-avoid-copying-data"></a>ArrayReference 使用による、データ コピーの回避

データが ABI を介して [Platform::Array](../cppcx/platform-array-class.md)に渡されており、最終的にはそのデータを C スタイル配列で処理して効率性を追求するシナリオでは、 [Platform::ArrayReference](../cppcx/platform-arrayreference-class.md) を使用して、不要なコピー操作を回避できます。 [を受け取るパラメーターに引数として](../cppcx/platform-arrayreference-class.md) Platform::ArrayReference `Platform::Array`が渡されると、 `ArrayReference` は、そのデータを指定された C スタイル配列に直接格納します。 `ArrayReference` にソース データへのロック オンがないため、呼び出しが完了する前に別のスレッドでそのデータが変更されるかまたは削除された場合、結果は不確定になることに注意してください。

次のコード スニペットは、 [DataReader](/uwp/api/windows.storage.streams.datareader) 操作の結果を `Platform::Array` にコピーする方法 (通常のパターン) と、 `ArrayReference` を代わりに使用してデータを C スタイル配列に直接コピーする方法を示します。

[!code-cpp[cx_arrays#07](../cppcx/codesnippet/CPP/js-array/class1.h#07)]

## <a name="avoid-exposing-an-array-as-a-property"></a>配列をプロパティとして公開することを回避する方法

一般に、ref クラスで `Platform::Array` 型をプロパティとして公開することは避ける必要があります。これは、クライアント コードが単一要素にアクセスしようとしている場合でも、配列全体が返されるためです。 パブリック ref クラスでシーケンス コンテナーをプロパティとして公開する必要があるときは、 [Windows::Foundation::IVector](/uwp/api/windows.foundation.collections.ivector-1) の方が適切です。 プライベートまたは内部 API (メタデータに発行されません) では、 [std::vector](../standard-library/vector-class.md)などの標準 C++ コンテナーの使用を検討してください。

## <a name="see-also"></a>関連項目

[型システム](../cppcx/type-system-c-cx.md)<br/>
[C++/CX 言語リファレンス](../cppcx/visual-c-language-reference-c-cx.md)<br/>
[名前空間参照](../cppcx/namespaces-reference-c-cx.md)

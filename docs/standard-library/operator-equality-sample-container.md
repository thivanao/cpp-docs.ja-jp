---
title: operator== (&lt;sample container&gt;)
ms.date: 11/04/2016
f1_keywords:
- std.==
- std::==
- operator==
- std.operator==
- std::operator==
- ==
helpviewer_keywords:
- operator ==, containers
- operator==, containers
- == operator, with specific standard C++ objects
ms.assetid: d3d8754e-5157-4b8b-bf9c-da41856f5eed
ms.openlocfilehash: 08adfcc770551d3050daa46c870b950e468c95b3
ms.sourcegitcommit: eff68e4e82be292a5664616b16a526df3e9d1cda
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80150643"
---
# <a name="operator-ltsample-containergt"></a>operator== (&lt;sample container&gt;)

> [!NOTE]
> このトピックは、 C++ C++標準ライブラリで使用されているコンテナーの非機能例として、Microsoft ドキュメントに記載されています。 詳しくは、「[C++ 標準ライブラリのコンテナー](../standard-library/stl-containers.md)」をご覧ください。

オーバーロード `operator==` クラステンプレート[コンテナー](../standard-library/sample-container-class.md)の2つのオブジェクトを比較します。

## <a name="syntax"></a>構文

```cpp
template <class Ty>
bool operator==(
    const Container <Ty>& left,
    const Container <Ty>& right);
```

## <a name="return-value"></a>戻り値

`, right.begin)`[終了](../standard-library/container-class-end.md)`, left.`[開始](../standard-library/container-class-begin.md)`== right.size && equal(left.``left.`[サイズ](../standard-library/container-class-size.md)を返します。

## <a name="see-also"></a>参照

[\<sample container>](../standard-library/sample-container.md)

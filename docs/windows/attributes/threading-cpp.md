---
title: スレッド処理C++ (COM 属性)
ms.date: 10/02/2018
f1_keywords:
- vc-attr.threading
helpviewer_keywords:
- threading attribute
ms.assetid: 9b558cd6-fbf0-4602-aed5-31c068550ce3
ms.openlocfilehash: b249eaf61266ed9964e44f6f0ad1c2f12a1b1067
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80214501"
---
# <a name="threading-c"></a>threading (C++)

COM オブジェクトのスレッド処理モデルを指定します。

## <a name="syntax"></a>構文

```cpp
[ threading(model=enumeration) ]
```

### <a name="parameters"></a>パラメーター

*model*<br/>
Optional次のいずれかのスレッドモデル:

- `apartment` (アパートメントスレッド)

- `neutral` (ユーザーインターフェイスを持たないコンポーネントの .NET Framework)

- `single` (単純なスレッド処理)

- `free` (フリースレッド)

- `both` (アパートメントおよびフリースレッド)

既定値は `apartment` です。

## <a name="remarks"></a>解説

**スレッド** C++属性は、生成された .idl ファイルには表示されませんが、COM オブジェクトの実装で使用されます。

ATL プロジェクトでは、 [coclass](coclass.md)属性も存在する場合、*モデル*で指定されたスレッドモデルは、`coclass` 属性によって挿入される[CComObjectRootEx](../../atl/reference/ccomobjectrootex-class.md)クラスにテンプレートパラメーターとして渡されます。

**スレッド**属性は、 [event_source](event-source.md)へのアクセスも保護します。

## <a name="example"></a>例

**スレッド処理**の使用例については、[ライセンス](licensed.md)の例を参照してください。

## <a name="requirements"></a>必要条件

### <a name="attribute-context"></a>属性コンテキスト

|||
|-|-|
|**対象**|**クラス**、**構造体**|
|**反復可能**|いいえ|
|**必要な属性**|**coclass**|
|**無効な属性**|なし|

属性コンテキストの詳細については、「 [属性コンテキスト](cpp-attributes-com-net.md#contexts)」を参照してください。

## <a name="see-also"></a>参照

[COM 属性](com-attributes.md)<br/>
[Typedef、Enum、Union、および Struct 型の属性](typedef-enum-union-and-struct-attributes.md)<br/>
[クラス属性](class-attributes.md)<br/>
[旧形式のコードのためのマルチスレッド サポート (Visual C++)](../../parallel/multithreading-support-for-older-code-visual-cpp.md)<br/>
[ニュートラルアパートメント](/windows/win32/cossdk/neutral-apartments)
